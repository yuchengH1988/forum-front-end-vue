<template>
  <div class="container py-5">
    <Spinner v-if="isLoading" />
    <template v-else>
      <RestaurantDetail :initialRest="restaurant" />
      <!-- 餐廳資訊頁 RestaurantDetail -->
      <hr />
      <!-- 餐廳評論 RestaurantComments -->
      <RestaurantComments
        :restaurantComments="restaurantComments"
        :currentUser="currentUser"
        @after-delete-comment="afterDeleteComment"
      />
      <!-- 新增評論 CreateComment -->
      <CreateComment
        :restaurantId="restaurant.id"
        @after-create-comment="afterCreateComment"
      />
    </template>
  </div>
</template>
<script>
import { mapState } from "vuex";
import RestaurantDetail from "./../components/RestaurantDetail";
import RestaurantComments from "./../components/RestaurantComments";
import CreateComment from "./../components/CreateComment";
import restaurantsAPI from "./../apis/restaurants";
import Spinner from "./../components/Spinner.vue";
import { Toast } from "./../utils/helpers";
export default {
  name: "Restaurant",
  components: {
    RestaurantDetail,
    RestaurantComments,
    CreateComment,
    Spinner,
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryName: "",
        image: "",
        openingHours: "",
        tel: "",
        address: "",
        description: "",
        isFavorited: false,
        isLiked: false,
      },
      restaurantComments: [],
      isLoading: true,
    };
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  beforeRouteUpdate(to, from, next) {
    const { id: restaurantId } = to.params;
    this.fetchRestaurant(restaurantId);
    next();
  },
  created() {
    const { id: restaurantId } = this.$route.params;
    this.fetchRestaurant(restaurantId);
  },
  methods: {
    async fetchRestaurant(restaurantId) {
      try {
        this.isLoading = true;
        // STEP 4: 透過 restaurantsAPI 取得餐廳資訊
        const { data } = await restaurantsAPI.getRestaurant({ restaurantId });

        // STEP 5: 透過 restaurantsAPI 取得餐廳資訊
        const { restaurant, isFavorited, isLiked } = data;
        const {
          id,
          name,
          Category,
          image,
          opening_hours: openingHours,
          tel,
          address,
          description,
          Comments,
        } = restaurant;

        this.restaurant = {
          id,
          name,
          categoryName: Category ? Category.name : "未分類",
          image,
          openingHours,
          tel,
          address,
          description,
          isFavorited,
          isLiked,
        };

        this.restaurantComments = Comments;
        this.isLoading = false;
      } catch (error) {
        this.isLoading = false;
        // STEP 6: 透過 restaurantsAPI 取得餐廳資訊
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳資料，請稍後再試",
        });
      }
    },
    afterDeleteComment(commentId) {
      // 以 filter 保留未被選擇的 comment.id
      this.restaurantComments = this.restaurantComments.filter(
        (comment) => comment.id !== commentId
      );
    },
    afterCreateComment(payload) {
      const { commentId, restaurantId, text } = payload;
      this.restaurantComments.push({
        id: commentId,
        RestaurantId: restaurantId,
        User: {
          id: this.currentUser.id,
          name: this.currentUser.name,
        },
        text,
        createdAt: new Date(),
      });
    },
  },
};
</script>
