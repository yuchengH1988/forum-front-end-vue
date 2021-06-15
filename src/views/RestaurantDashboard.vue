<template>
  <div class="container py-5">
    <Spinner v-if="isLoading" />
    <template v-else>
      <div>
        <h1>{{ restaurant.name }}</h1>
        <span class="badge badge-secondary bg-secondary text-white mt-1 mb-3">
          {{ restaurant.categoryName }}
        </span>
      </div>

      <hr />

      <ul>
        <li>評論數： {{ restaurant.commentsLength }}</li>
        <li>瀏覽次數： {{ restaurant.viewCounts }}</li>
      </ul>

      <button type="button" class="btn btn-link" @click="$router.back()">
        回上一頁
      </button>
    </template>
  </div>
</template>
<script>
import restaurantsAPI from "./../apis/restaurants";
import Spinner from "./../components/Spinner";
import { Toast } from "./../utils/helpers";
export default {
  name: "RestaurantDashboard",
  components: {
    Spinner,
  },
  data() {
    return {
      restaurant: {
        name: "",
        categoryName: "",
        commentsLength: -1,
        viewCounts: -1,
      },
      isLoading: true,
    };
  },
  methods: {
    async fetchRestaurant(restaurantId) {
      try {
        this.isLoading = true;
        const { data } = await restaurantsAPI.getDashboard({ restaurantId });
        const { restaurant } = data;
        this.restaurant = {
          id: restaurant.id,
          name: restaurant.name,
          categoryName: restaurant.Category.name,
          commentsLength: restaurant.Comments.length,
          viewCounts: restaurant.viewCounts,
        };
        this.isLoading = false;
      } catch (error) {
        this.isLoading = false;
        Toast.fire({
          icon: "error",
          title: "無法載入餐廳Dashboard，請稍後再試",
        });
      }
    },
  },
  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchRestaurant(restaurantId);
  },
};
</script>

