<template>
  <div id="restaurant-forum">
    <Navbar />
    <main class="mt-5 bg-white">
      <!-- router view 底下顯示 路由組件-->
      <router-view />
    </main>
  </div>
</template>
<script>
import "bootstrap";
import "bootstrap-vue";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import "jquery/src/jquery.js";
import "bootstrap/dist/js/bootstrap.min.js";
import Navbar from "./components/Navbar";
export default {
  name: "app",
  components: {
    Navbar,
  },
};
</script>
<style scoped>
main {
  margin-top: 65px !important;
}
</style>
