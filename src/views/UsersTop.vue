<template>
  <div class="container py-5">
    <NavTabs />
    <Spinner v-if="isLoading" />
    <template v-else>
      <h1 class="mt-5">美食達人</h1>
      <hr />
      <div class="row text-center">
        <UserCard v-for="user in users" :key="user.id" :initialUser="user" />
      </div>
    </template>
  </div>
</template>
<script>
import NavTabs from "./../components/NavTabs";
import Spinner from "./../components/Spinner";
import UserCard from "./../components/UserCard";
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helpers";

export default {
  name: "UsersTop",
  components: {
    NavTabs,
    UserCard,
    Spinner,
  },
  data() {
    return {
      users: [],
      isLoading: true,
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const { data } = await usersAPI.getTopUsers();
        this.users = data.users.map((user) => ({
          id: user.id,
          name: user.name,
          image: user.image,
          followerCount: user.FollowerCount,
          isFollowed: user.isFollowed,
        }));
        this.isLoading = false;
      } catch (error) {
        this.isLoading = false;
        Toast.fire({
          icon: "error",
          title: "無法取得美食達人，請稍後再試",
        });
      }
    },
  },
  created() {
    this.fetchUsers();
  },
};
</script>