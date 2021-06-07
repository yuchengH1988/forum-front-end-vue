<template>
  <div class="card">
    <div class="card-header">最新餐廳</div>
    <div class="card-body">
      <div v-for="rest in restaurants" :key="rest.id">
        <h4>
          <router-link :to="{ name: 'restaurant', params: { id: rest.id } }">{{
            rest.name
          }}</router-link>
          <small>{{ rest.Category ? rest.Category.name : "未分類" }}</small>
        </h4>
        <p>
          {{ rest.description }}
        </p>
        {{ rest.createdAt | fromNow }}
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import { fromNowFilter } from "./../utils/mixins";
export default {
  mixins: [fromNowFilter],
  props: {
    restaurants: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
small {
  font-size: 10px;
}
</style>