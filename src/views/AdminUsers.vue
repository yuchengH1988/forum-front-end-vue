<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />
    <Spinner v-if="isLoading" />
    <table v-else class="table">
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
          <td>{{ user.isAdmin ? "Admin" : "Users" }}</td>
          <td>
            <button
              v-if="user.id !== currentUser.id"
              @click.stop.prevent="
                toggleUserRole({ userId: user.id, isAdmin: user.isAdmin })
              "
              type="button"
              class="btn btn-link"
            >
              {{ user.isAdmin ? "set as user" : "set as admin" }}
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import AdminNav from "../components/AdminNav";
import adminAPI from "./../apis/admin";
import Spinner from "./../components/Spinner.vue";
import { Toast } from "./../utils/helpers";
import { mapState } from "vuex";
export default {
  components: {
    AdminNav,
    Spinner,
  },
  computed: {
    ...mapState(["currentUser"]),
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
        this.isLoading = true;
        const { data } = await adminAPI.users.get();
        this.users = data.users;
        this.isLoading = false;
      } catch (error) {
        this.isLoading = false;
        Toast.fire({
          icon: "error",
          title: "無法取得使用者資料，請稍後再試",
        });
      }
    },
    async toggleUserRole({ userId, isAdmin }) {
      try {
        const { data } = await adminAPI.users.toggleAdmin({
          userId,
          isAdmin: (!isAdmin).toString(),
        });
        if (data.status !== "success") {
          throw new Error(data.message);
        }
        this.users = this.users.map((user) => {
          if (user.id === userId) {
            return {
              ...user,
              isAdmin: !user.isAdmin,
            };
          }
          return user;
        });
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法更改此使用者權限，請稍後再試",
        });
      }
    },
  },
  created() {
    this.fetchUsers();
  },
};
</script>