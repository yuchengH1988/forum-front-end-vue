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
const dummyData = {
  restaurants: [
    {
      id: 5,
      name: "Isabelle Emmerich",
      tel: "642.420.1404 x4385",
      address: "34249 Volkman Grove",
      opening_hours: "08:00",
      description: "non ea illo",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=36.36127013737524",
      viewCounts: 3,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-30T04:31:01.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 5,
            createdAt: "2021-05-30T07:56:31.000Z",
            updatedAt: "2021-05-30T07:56:31.000Z",
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
          Favorite: {
            UserId: 11,
            RestaurantId: 5,
            createdAt: "2021-05-30T07:56:50.000Z",
            updatedAt: "2021-05-30T07:56:50.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 2,
    },
    {
      id: 3,
      name: "Aglae Gulgowski",
      tel: "114.568.9420 x031",
      address: "43362 Noel Turnpike",
      opening_hours: "08:00",
      description: "At commodi ut veritatis et velit est quis. Ut laud",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=79.91299846538044",
      viewCounts: 5,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-31T11:23:34.000Z",
      CategoryId: 4,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 3,
            createdAt: "2021-05-27T15:40:21.000Z",
            updatedAt: "2021-05-27T15:40:21.000Z",
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
          Favorite: {
            UserId: 11,
            RestaurantId: 3,
            createdAt: "2021-05-30T07:56:48.000Z",
            updatedAt: "2021-05-30T07:56:48.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 2,
    },
    {
      id: 1,
      name: "Keely BogisichDa",
      tel: "119.568.4472 x714",
      address: "9991 Dorothy Canyon",
      opening_hours: "08:00",
      description: "Beatae et sit aut velit sed minus esse est est. Cu",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=43.31238337743435",
      viewCounts: 14,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-06-05T14:20:16.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 1,
            createdAt: "2021-05-22T01:39:25.000Z",
            updatedAt: "2021-05-22T01:39:25.000Z",
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
          Favorite: {
            UserId: 11,
            RestaurantId: 1,
            createdAt: "2021-05-30T07:56:47.000Z",
            updatedAt: "2021-05-30T07:56:47.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 2,
    },
    {
      id: 48,
      name: "Dr. Angelita Cassin",
      tel: "(934) 446-1520 x790",
      address: "6463 Dach Parkway",
      opening_hours: "08:00",
      description: "A perferendis doloremque quae alias officiis ea. E",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=57.07047964964713",
      viewCounts: 0,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-17T05:11:05.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 11,
            RestaurantId: 48,
            createdAt: "2021-05-29T11:29:30.000Z",
            updatedAt: "2021-05-29T11:29:30.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 34,
      name: "Christina Wilderman",
      tel: "994-533-6732 x683",
      address: "781 Manuel Corner",
      opening_hours: "08:00",
      description: "corrupti",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=17.92886995776586",
      viewCounts: 0,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-17T05:11:05.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 11,
            RestaurantId: 34,
            createdAt: "2021-05-29T11:29:29.000Z",
            updatedAt: "2021-05-29T11:29:29.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 13,
      name: "Erna Cassin PhD",
      tel: "642-685-6113",
      address: "902 Maegan Inlet",
      opening_hours: "08:00",
      description: "tenetur rerum magnam",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=75.12026971384928",
      viewCounts: 0,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-17T05:11:05.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 1,
            RestaurantId: 13,
            createdAt: "2021-05-30T07:56:36.000Z",
            updatedAt: "2021-05-30T07:56:36.000Z",
          },
        },
      ],
      isFavorited: true,
      FavoriteCount: 1,
    },
    {
      id: 9,
      name: "Cecile Schaden",
      tel: "1-132-261-4174",
      address: "768 Boyle Canyon",
      opening_hours: "08:00",
      description: "Et distinctio commodi reprehenderit omnis. Maxime ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=39.152519630246154",
      viewCounts: 2,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-28T16:31:23.000Z",
      CategoryId: 1,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 11,
            RestaurantId: 9,
            createdAt: "2021-05-29T11:29:28.000Z",
            updatedAt: "2021-05-29T11:29:28.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 6,
      name: "Miss Darrel Funk",
      tel: "1-174-686-9086 x8073",
      address: "11507 Weimann Place",
      opening_hours: "08:00",
      description: "Veniam omnis in iste perferendis quod quia tempora",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=84.47709833016874",
      viewCounts: 0,
      createdAt: "2021-05-17T05:11:05.000Z",
      updatedAt: "2021-05-17T05:11:05.000Z",
      CategoryId: 4,
      FavoritedUsers: [
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
          Favorite: {
            UserId: 11,
            RestaurantId: 6,
            createdAt: "2021-05-30T07:56:52.000Z",
            updatedAt: "2021-05-30T07:56:52.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
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
      FavoritedUsers: [
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
          Favorite: {
            UserId: 11,
            RestaurantId: 2,
            createdAt: "2021-05-30T07:56:47.000Z",
            updatedAt: "2021-05-30T07:56:47.000Z",
          },
        },
      ],
      isFavorited: false,
      FavoriteCount: 1,
    },
    {
      id: 51,
      name: "麥當勞",
      tel: "123",
      address: "694 Schroeder Spurs",
      opening_hours: "21:10",
      description: "555555555",
      image: "https://i.imgur.com/0A5og2G.jpg",
      viewCounts: 0,
      createdAt: "2021-05-29T12:09:30.000Z",
      updatedAt: "2021-05-29T12:15:26.000Z",
      CategoryId: 6,
      FavoritedUsers: [],
      isFavorited: false,
      FavoriteCount: 0,
    },
  ],
};
export default {
  name: "RestaurantsTop",
  data() {
    return {
      restaurants: [],
    };
  },
  methods: {
    fetchRestaurants() {
      this.restaurants = dummyData.restaurants;
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