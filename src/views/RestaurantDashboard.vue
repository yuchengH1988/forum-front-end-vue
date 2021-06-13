<template>
  <div class="container py-5">
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
  </div>
</template>
<script>
const dummyData = {
  restaurant: {
    id: 2,
    name: "Alexandrine McKenzie DVM",
    tel: "(266) 656-0345 x270",
    address: "0142 Smith Gateway",
    opening_hours: "08:00",
    description: "voluptas",
    image:
      "https://loremflickr.com/320/240/restaurant,food/?random=7.1615087469963035",
    viewCounts: 11,
    createdAt: "2021-05-17T05:11:05.000Z",
    updatedAt: "2021-05-31T11:22:40.000Z",
    CategoryId: 5,
    Category: {
      id: 5,
      name: "素食料理",
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-17T05:11:05.000Z",
    },
    Comments: [
      {
        id: 2,
        text: "Et aut voluptate explicabo architecto libero non deserunt qui.",
        UserId: 1,
        RestaurantId: 2,
        createdAt: "2021-05-17T05:11:05.000Z",
        updatedAt: "2021-05-17T05:11:05.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
          isAdmin: true,
          image: "https://i.imgur.com/eVfTIsY.jpg",
          createdAt: "2021-05-17T05:11:05.000Z",
          updatedAt: "2021-05-29T16:22:50.000Z",
        },
      },
      {
        id: 102,
        text: "Nostrum adipisci quia quia saepe quis quasi.",
        UserId: 1,
        RestaurantId: 2,
        createdAt: "2021-05-17T05:11:05.000Z",
        updatedAt: "2021-05-17T05:11:05.000Z",
        User: {
          id: 1,
          name: "root",
          email: "root@example.com",
          password:
            "$2a$10$XaxJSOdUg2/931GxMxcJpOWAB1wmUbW5WUwM1GohFh0SyfUxHNYKG",
          isAdmin: true,
          image: "https://i.imgur.com/eVfTIsY.jpg",
          createdAt: "2021-05-17T05:11:05.000Z",
          updatedAt: "2021-05-29T16:22:50.000Z",
        },
      },
      {
        id: 52,
        text: "Aut et autem nostrum ex veniam a aut amet in.",
        UserId: 3,
        RestaurantId: 2,
        createdAt: "2021-05-17T05:11:05.000Z",
        updatedAt: "2021-05-17T05:11:05.000Z",
        User: {
          id: 3,
          name: "Kugisaki Nobara",
          email: "user2@example.com",
          password:
            "$2a$10$b7E1.cVoAcrTFooTp4tx4eFnxUxKizT8mVr26QYJGuhp4YbRnjB02",
          isAdmin: false,
          image: "https://i.imgur.com/es1gVME.jpeg",
          createdAt: "2021-05-17T05:11:05.000Z",
          updatedAt: "2021-05-29T16:29:30.000Z",
        },
      },
      {
        id: 161,
        text: "Go eating\n",
        UserId: 11,
        RestaurantId: 2,
        createdAt: "2021-05-31T11:22:15.000Z",
        updatedAt: "2021-05-31T11:22:15.000Z",
        User: {
          id: 11,
          name: "Itadori Yuji",
          email: "Da@example.com",
          password:
            "$2a$10$p7b9n0Gg1WNmrhTx.pQfhOtkCcynVowSDNM6BpMORotEz/d6.nA0K",
          isAdmin: false,
          image: "https://i.imgur.com/pIHFJtM.png",
          createdAt: "2021-05-29T07:38:44.000Z",
          updatedAt: "2021-05-29T16:30:20.000Z",
        },
      },
    ],
  },
};
import restaurantsAPI from "./../apis/restaurants";
import { Toast } from "./../utils/helpers";
export default {
  name: "RestaurantDashboard",
  data() {
    return {
      restaurant: {
        name: "",
        categoryName: "",
        commentsLength: -1,
        viewCounts: -1,
      },
    };
  },
  methods: {
    async fetchRestaurant(restaurantId) {
      try {
        const { data } = await restaurantsAPI.getDashboard({ restaurantId });
        const { restaurant } = data;
        this.restaurant = {
          id: restaurant.id,
          name: restaurant.name,
          categoryName: restaurant.Category.name,
          commentsLength: restaurant.Comments.length,
          viewCounts: restaurant.viewCounts,
        };
      } catch (error) {
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
  watch: {},
};
</script>

