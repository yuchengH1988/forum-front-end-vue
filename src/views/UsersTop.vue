<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">美食達人</h1>
    <hr />
    <div class="row text-center">
      <UserCard v-for="user in usersTop" :key="user.id" :initialUser="user" />
    </div>
  </div>
</template>
<script>
import NavTabs from "./../components/NavTabs";
import UserCard from "./../components/UserCard";
const usersTop = {
  users: [
    {
      id: 11,
      name: "Itadori Yuji",
      email: "Da@example.com",
      password: "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
      isAdmin: false,
      image: "https://i.imgur.com/pIHFJtM.png",
      createdAt: "2021-05-29T07:38:44.000Z",
      updatedAt: "2021-05-29T16:30:20.000Z",
      Followers: [
        {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
          isAdmin: true,
          image: "https://i.imgur.com/eVfTIsY.jpg",
          createdAt: "2021-05-17T05:11:05.000Z",
          updatedAt: "2021-05-29T16:22:50.000Z",
          Followship: {
            followerId: 1,
            followingId: 11,
            createdAt: "2021-05-29T11:29:59.000Z",
            updatedAt: "2021-05-29T11:29:59.000Z",
          },
        },
        {
          id: 11,
          name: "Itadori Yuji",
          email: "Da@example.com",
          password:
            "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
          isAdmin: false,
          image: "https://i.imgur.com/pIHFJtM.png",
          createdAt: "2021-05-29T07:38:44.000Z",
          updatedAt: "2021-05-29T16:30:20.000Z",
          Followship: {
            followerId: 11,
            followingId: 11,
            createdAt: "2021-05-30T09:37:22.000Z",
            updatedAt: "2021-05-30T09:37:22.000Z",
          },
        },
      ],
      FollowerCount: 2,
      isFollowed: true,
    },
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
      isAdmin: true,
      image: "https://i.imgur.com/eVfTIsY.jpg",
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-29T16:22:50.000Z",
      Followers: [
        {
          id: 11,
          name: "Itadori Yuji",
          email: "Da@example.com",
          password:
            "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
          isAdmin: false,
          image: "https://i.imgur.com/pIHFJtM.png",
          createdAt: "2021-05-29T07:38:44.000Z",
          updatedAt: "2021-05-29T16:30:20.000Z",
          Followship: {
            followerId: 11,
            followingId: 1,
            createdAt: "2021-05-30T03:40:21.000Z",
            updatedAt: "2021-05-30T03:40:21.000Z",
          },
        },
      ],
      FollowerCount: 1,
      isFollowed: false,
    },
    {
      id: 2,
      name: "Fushiguro Megumi",
      email: "user1@example.com",
      password: "$2a$10$A0B7wDm/3dqFAxjH45sXW.2ASFMgKVGKU3DH6O5VpnGSG3Bd6Y9kq",
      isAdmin: false,
      image: "https://i.imgur.com/hSgGs9O.jpg",
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-29T16:25:56.000Z",
      Followers: [
        {
          id: 11,
          name: "Itadori Yuji",
          email: "Da@example.com",
          password:
            "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
          isAdmin: false,
          image: "https://i.imgur.com/pIHFJtM.png",
          createdAt: "2021-05-29T07:38:44.000Z",
          updatedAt: "2021-05-29T16:30:20.000Z",
          Followship: {
            followerId: 11,
            followingId: 2,
            createdAt: "2021-05-29T11:29:18.000Z",
            updatedAt: "2021-05-29T11:29:18.000Z",
          },
        },
      ],
      FollowerCount: 1,
      isFollowed: false,
    },
    {
      id: 3,
      name: "Kugisaki Nobara",
      email: "user2@example.com",
      password: "$2a$10$b7E1.cVoAcrTFooTp4tx4eFnxUxKizT8mVr26QYJGuhp4YbRnjB02",
      isAdmin: false,
      image: "https://i.imgur.com/es1gVME.jpeg",
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-29T16:29:30.000Z",
      Followers: [],
      FollowerCount: 0,
      isFollowed: false,
    },
  ],
};
export default {
  name: "UsersTop",
  components: {
    NavTabs,
    UserCard,
  },
  data() {
    return {
      usersTop: [],
    };
  },
  methods: {
    fetchUsers() {
      this.usersTop = usersTop.users;
    },
    addFollowing() {
      this.restaurant = {
        ...this.restaurant,
        isLiked: true,
      };
    },
    removeFollowing() {},
  },
  created() {
    this.fetchUsers();
  },
};
</script>