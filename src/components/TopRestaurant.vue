<template>
  <div class="card mb-3" style="max-width: 540px; margin: auto">
    <div class="row no-gutters">
      <div class="col-md-4">
        <a :href="restaurant.image">
          <img class="card-img" :src="restaurant.image" />
        </a>
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ restaurant.name }}</h5>
          <span class="badge badge-secondary bg-secondary text-white"
            >收藏數：{{ restaurant.FavoriteCount }}</span
          >
          <p class="card-text">
            {{ restaurant.description }}
          </p>
          <router-link
            :to="{ name: 'restaurant', params: { id: restaurant.id } }"
            class="btn btn-primary mr-2"
            >Show</router-link
          >

          <button
            v-if="restaurant.isFavorited"
            @click.stop.prevent="deleteFavorite"
            type="button"
            class="btn btn-danger mr-2"
          >
            移除最愛
          </button>
          <button
            v-else
            @click.stop.prevent="addFavorite"
            type="button"
            class="btn btn-primary"
          >
            加到最愛
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    initialRestaurant: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      restaurant: {
        id: this.initialRestaurant.id,
        name: this.initialRestaurant.name,
        image: this.initialRestaurant.image,
        openingHours: this.initialRestaurant.openingHours,
        tel: this.initialRestaurant.tel,
        address: this.initialRestaurant.address,
        description: this.initialRestaurant.description,
        createdAt: this.initialRestaurant.createdAt,
        isFavorited: this.initialRestaurant.isFavorited,
        FavoriteCount: this.initialRestaurant.FavoriteCount,
      },
    };
  },
  methods: {
    addFavorite() {
      this.restaurant = {
        ...this.restaurant, // 保留餐廳內原有資料
        isFavorited: true,
        FavoriteCount: this.restaurant.FavoriteCount + 1,
      };
    },
    deleteFavorite() {
      this.restaurant = {
        ...this.restaurant, // 保留餐廳內原有資料
        isFavorited: false,
        FavoriteCount: this.restaurant.FavoriteCount - 1,
      };
    },
  },
};
</script>