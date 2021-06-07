<template>
  <div class="card">
    <div class="card-header">
      <strong>{{ UserFollowings.length }}</strong> followings (追蹤者)
    </div>
    <div class="card-body">
      <router-link
        v-for="following in UserFollowings"
        :key="following.id"
        :to="{ name: 'user', params: { id: following.id } }"
      >
        <img :src="following.image" width="60" height="60" class="avatar" />
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    UserFollowings: {
      type: Array,
      require: true,
    },
  },
};
</script>
