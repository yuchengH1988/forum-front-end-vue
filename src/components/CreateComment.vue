<template>
  <form @submit.stop.prevent="handleSubmit">
    <div class="form-group mb-4">
      <label for="text">留下評論：</label>
      <textarea v-model="text" class="form-control" rows="3" name="text" />
    </div>
    <div class="d-flex align-items-center justify-content-between">
      <button type="button" class="btn btn-link" @click="$router.back()">
        回上一頁
      </button>
      <button
        :disabled="isProcessing"
        type="submit"
        class="btn btn-primary mr-0"
      >
        {{ isProcessing ? "處理中" : "Submit" }}
      </button>
    </div>
  </form>
</template>
<script>
import commentsAPI from "./../apis/comments";
import { Toast } from "./../utils/helpers";
export default {
  name: "CreateComment",
  props: {
    restaurantId: {
      type: Number,
      require: true,
    },
  },
  data() {
    return {
      text: "",
      isProcessing: false,
    };
  },
  methods: {
    async handleSubmit() {
      try {
        if (!this.text) {
          Toast.fire({
            icon: "warning",
            title: "請填入評論",
          });
          return;
        }
        this.isProcessing = true;
        const { data } = await commentsAPI.create({
          restaurantId: this.restaurantId,
          text: this.text,
        });
        if (data.status === "error") {
          throw new Error(data.messga);
        }
        this.$emit("after-create-comment", {
          commentId: data.commentId,
          restaurantId: this.restaurantId,
          text: this.text,
        });
        this.isProcessing = false;
        this.text = "";
      } catch (error) {
        console.error(error.message);
        this.isProcessing = false;
        Toast.fire({
          icon: "error",
          title: "無法新增評論，請稍後再試",
        });
      }
    },
  },
};
</script>
<style scoped>
.form-group {
  margin: 21px 0 8px;
}
</style>