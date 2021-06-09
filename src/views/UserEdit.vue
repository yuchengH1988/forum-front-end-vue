<template>
  <div class="container py-5">
    <form @submit.stop.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          v-model="user.name"
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
          v-if="user.image"
          :src="user.image"
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

      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>
<script>
const dummyUser = {
  id: 3,
  name: "Kugisaki Nobara",
  email: "user2@example.com",
  password: "$2a$10$b7E1.cVoAcrTFooTp4tx4eFnxUxKizT8mVr26QYJGuhp4YbRnjB02",
  isAdmin: false,
  image:
    "https://i.pinimg.com/564x/33/94/fd/3394fd5fb7add7640b5d6a2c3cff7318.jpg",
  createdAt: "2021-05-17T05:11:05.000Z",
  updatedAt: "2021-05-29T16:29:30.000Z",
};
export default {
  name: "UserEdit",
  data() {
    return {
      user: {
        name: "",
        image: "",
      },
    };
  },
  methods: {
    fetchUser(id) {
      console.log("fetchUser" + id);
      this.user = {
        ...this.user,
        ...dummyUser,
      };
    },
    handleFileChange(e) {
      const { files } = e.target;
      if (files.length === 0) {
        this.user.image = "";
      } else {
        const imageURL = window.URL.createObjectURL(files[0]);
        this.user.image = imageURL;
      }
    },
    handleSubmit(e) {
      const form = e.target;
      const formData = new FormData(form);
      for (let [name, value] of formData.entries()) {
        console.log(name + ": " + value);
      }
    },
  },
  created() {
    const { id } = this.$route.params;
    this.fetchUser(id);
  },
};
</script>