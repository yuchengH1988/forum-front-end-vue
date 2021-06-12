<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>
    <hr />
    <TopRestaurant
      v-for="restaurant in restaurants"
      :key="restaurant.id"
      :initial-restaurant="restaurant"
    />
  </div>
</template>
<script>
import NavTabs from "./../components/NavTabs";
import TopRestaurant from "./../components/TopRestaurant.vue";
import restaurantsAPI from "./../apis/restaurants";
import { Toast } from "./../utils/helpers";

export default {
  name: "RestaurantsTop",
  data() {
    return {
      restaurants: [],
    };
  },
  methods: {
    async fetchRestaurants() {
      try {
        const { data } = await restaurantsAPI.getRestaurantsTop();
        this.restaurants = data.restaurants;
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法成功載入人氣餐廳，請稍後再試",
        });
      }
    },
  },
  components: {
    NavTabs,
    TopRestaurant,
  },
  created() {
    this.fetchRestaurants();
  },
};
</script>