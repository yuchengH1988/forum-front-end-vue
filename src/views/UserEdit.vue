<template>
  <div class="container py-5">
    <form @submit.stop.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          v-model="name"
          id="name"
          type="text"
          name="name"
          class="form-control"
          placeholder="Enter Name"
          required
        />
      </div>

      <div class="form-group">
        <label for="image">Image</label>
        <img
          v-if="image"
          :src="image"
          class="d-bloc img-thumbnail"
          width="200"
          height="200"
        />
        <input
          id="image"
          type="file"
          name="image"
          accept="image/*"
          class="form-control-file"
          @change="handleFileChange"
        />
      </div>

      <button :disabled="isProcessing" type="submit" class="btn btn-primary">
        {{ isProcessing ? "處理中..." : "Submit" }}
      </button>
    </form>
  </div>
</template>
<script>
import { mapState } from "vuex";
import { Toast } from "./../utils/helpers";
import usersAPI from "./../apis/users";
export default {
  name: "UserEdit",
  data() {
    return {
      id: 0,
      image: "",
      name: "",
      isProcessing: false,
    };
  },
  created() {
    if (this.currentUser.id === -1) return;
    const { id } = this.$route.params;
    this.setUser(id);
  },
  watch: {
    currentUser(user) {
      if (user.id === -1) return;
      const { id } = this.$route.params;
      this.setUser(id);
    },
  },
  beforeRouteUpdate(to, from, next) {
    if (this.currentUser.id === -1) return;
    const { id } = to.params;
    this.setUser(id);
    next();
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    setUser(userId) {
      const { id, image, name } = this.currentUser;
      if (id.toString() !== userId.toString()) {
        this.$router.push({
          name: "not-found",
        });
        return;
      }
      this.id = id;
      this.name = name;
      this.image = image;
    },
    handleFileChange(e) {
      const { files } = e.target;
      if (!files.length) return;
      const imageURL = window.URL.createObjectURL(files[0]);
      this.user.image = imageURL;
    },
    async handleSubmit(e) {
      try {
        //當使用者沒輸入名稱
        if (!this.name.trim()) {
          Toast.fire({
            icon: "warning",
            title: "請輸入名稱",
          });
          return;
        }
        this.isProcessing = true;
        const form = e.target;
        const formData = new FormData(form);
        const { data } = await usersAPI.update({
          userId: this.id,
          formData,
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.$router.push({
          name: "user",
          params: { id: this.id },
        });
      } catch (error) {
        this.isProcessing = false;
        Toast.fire({
          icon: "error",
          title: "無法更新使用者資料，請稍後再試",
        });
      }
    },
  },
};
</script>