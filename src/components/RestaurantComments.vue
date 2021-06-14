<template>
  <div>
    <h2 class="my-4">所有評論：</h2>

    <div v-for="comment in restaurantComments" :key="comment.id">
      <blockquote class="blockquote mb-0">
        <button
          v-if="currentUser.isAdmin"
          @click.stop.prevent="handleDeleteBtnClick(comment.id)"
          type="button"
          class="d-flex btn btn-danger float-right"
        >
          Delete
        </button>
        <h3>
          <router-link :to="{ name: 'user', params: { id: comment.User.id } }">
            {{ comment.User.name }}
          </router-link>
        </h3>
        <p>{{ comment.text }}</p>
        <footer class="blockquote-footer">
          {{ comment.createdAt | fromNow }}
        </footer>
      </blockquote>
      <hr />
    </div>
  </div>
</template>
<script>
import { fromNowFilter } from "./../utils/mixins";
import commentsAPI from "./../apis/comments";
import { Toast } from "./../utils/helpers";

export default {
  mixins: [fromNowFilter],
  props: {
    restaurantComments: {
      type: Array,
      require: true,
    },
    currentUser: {
      type: Object,
      require: true,
    },
  },
  methods: {
    async handleDeleteBtnClick(commentId) {
      try {
        const { data } = await commentsAPI.delete({ commentId });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法刪除評論，請稍號再試",
        });
      }

      this.$emit("after-delete-comment", commentId);
    },
  },
};
</script>
