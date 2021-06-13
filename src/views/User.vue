<template>
  <div class="container py-5">
    <UserProfileCard :UserProfile="UserProfile" :currentUser="currentUser" />
    <div class="row">
      <div class="col-md-4">
        <UserFollowingsCard :UserFollowings="UserFollowings" />
        <br />
        <UserFollowersCard :UserFollowers="UserFollowers" />
      </div>
      <div class="col-md-8">
        <UserCommentsCard :UserComments="UserComments" />

        <br />
        <UserFavoritedRestaruantsCards
          :FavoritedRestaurants="FavoritedRestaurants"
        />
      </div>
    </div>
  </div>
</template>
<script>
import UserProfileCard from "./../components/UserProfileCard";
import UserFollowingsCard from "./../components/UserFollowingsCard.vue";
import UserFollowersCard from "./../components/UserFollowersCard.vue";
import UserCommentsCard from "./../components/UserCommentsCard.vue";
import UserFavoritedRestaruantsCards from "./../components/UserFavoritedRestaurantsCard.vue";
import usersAPI from "./../apis/users";
import { Toast } from "./../utils/helpers";
import { mapState } from "vuex";

export default {
  components: {
    UserProfileCard,
    UserFollowingsCard,
    UserFollowersCard,
    UserCommentsCard,
    UserFavoritedRestaruantsCards,
  },
  created() {
    const { id: userId } = this.$route.params;
    this.fetchData(userId);
  },
  beforeRouteUpdate(to, from, next) {
    const { id } = to.params;
    this.fetchData(id);
    next();
  },
  computed: {
    ...mapState(["currentUser"]),
  },
  data() {
    return {
      UserProfile: {
        id: -1,
        name: "",
        image: "",
        email: "",
        commentLength: 0,
        favoritedLength: 0,
        followerLength: 0,
        followingLength: 0,
      },
      UserFollowings: [],
      UserFollowers: [],
      UserComments: [],
      FavoritedRestaurants: [],
    };
  },
  methods: {
    async fetchData(userId) {
      try {
        const { data } = await usersAPI.get({ userId });
        //讓已評論的餐廳不重複
        const commentSet = new Set();
        this.UserComments = data.profile.Comments.filter(
          (comment) =>
            comment.Restaurant &&
            !commentSet.has(comment.Restaurant.id) &&
            commentSet.add(comment.Restaurant.id)
        );

        this.UserProfile = {
          id: data.profile.id,
          name: data.profile.name,
          image: data.profile.image,
          email: data.profile.email,
          commentLength: this.UserComments.length,
          favoritedLength: data.profile.FavoritedRestaurants.length,
          followerLength: data.profile.Followers.length,
          followingLength: data.profile.Followings.length,
          isFollowed: data.isFollowed,
        };
        this.UserFollowings = data.profile.Followings;
        this.UserFollowers = data.profile.Followers;
        this.FavoritedRestaurants = data.profile.FavoritedRestaurants;
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取得使用者資料，請稍後再試",
        });
      }
    },
  },
};
</script>

<style>
</style>