<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="user.image" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ user.name }}</h5>
          <p class="card-text">{{ user.email }}</p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{ user.commentLength }}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{ user.favoritedLength }}</strong> 收藏的餐廳
            </li>
            <li>
              <strong>{{ user.followerLength }}</strong> followings (追蹤者)
            </li>
            <li>
              <strong>{{ user.followingLength }}</strong> followers (追隨者)
            </li>
          </ul>
          <p v-if="user.id === currentUser.id">
            <a href="/users/1/edit"
              ><button type="submit" class="btn btn-primary">edit</button></a
            >
          </p>
          <p v-if="user.id !== currentUser.id">
            <button
              v-if="user.isFollowed"
              @click.stop.prevent="deleteFollowing"
              type="button"
              class="btn btn-danger"
            >
              取消追蹤
            </button>
            <button
              v-else
              type="button"
              @click.stop.prevent="addFollowing"
              class="btn btn-primary"
            >
              追蹤
            </button>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    UserProfile: {
      type: Object,
      require: true,
    },
    currentUser: {
      type: Object,
      require: true,
    },
  },
  data() {
    return {
      user: {},
    };
  },
  created() {
    this.user = this.UserProfile;
  },
  methods: {
    addFollowing() {
      this.user = {
        ...this.user,
        isFollowed: true,
      };
    },

    deleteFollowing() {
      this.user = {
        ...this.user,
        isFollowed: false,
      };
    },
  },
};
</script>
