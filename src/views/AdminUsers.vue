<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col" width="140">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <th scope="row">{{ user.id }}</th>
          <td>{{ user.email }}</td>
          <td>{{ user.name }}</td>
          <td>
            <template v-if="user.id !== currentUser.id">
              <button
                v-show="user.isAdmin"
                @click.stop.prevent="toggleUserRole(user.id)"
                type="button"
                class="btn btn-link"
              >
                set as user
              </button>
              <button
                v-show="!user.isAdmin"
                @click.stop.prevent="toggleUserRole(user.id)"
                type="button"
                class="btn btn-link"
              >
                set as admin
              </button>
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
const dummyData = {
  users: [
    {
      id: 1,
      name: "root",
      email: "root@example.com",
      password: "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
      isAdmin: true,
      image: "https://i.imgur.com/eVfTIsY.jpg",
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-29T16:22:50.000Z",
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
    },
    {
      id: 11,
      name: "Itadori Yuji",
      email: "Da@example.com",
      password: "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
      isAdmin: false,
      image: "https://i.imgur.com/pIHFJtM.png",
      createdAt: "2021-05-29T07:38:44.000Z",
      updatedAt: "2021-05-29T16:30:20.000Z",
    },
  ],
};
const dummyUser = {
  id: 1,
  name: "root",
  email: "root@example.com",
  password: "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
  isAdmin: true,
  image: "https://i.imgur.com/eVfTIsY.jpg",
  createdAt: "2021-05-17T05:11:05.000Z",
  updatedAt: "2021-05-29T16:22:50.000Z",
};
import AdminNav from "../components/AdminNav";
export default {
  components: {
    AdminNav,
  },
  data() {
    return {
      users: [],
      currentUser: {},
    };
  },
  methods: {
    fetchUsers() {
      this.users = dummyData.users;
      this.currentUser = dummyUser;
    },
    toggleUserRole(userId) {
      this.users = this.users.map((user) => {
        if (user.id === userId) {
          return {
            ...user,
            isAdmin: !user.isAdmin,
          };
        }
        return user;
      });
    },
  },
  created() {
    this.fetchUsers();
  },
};
</script>