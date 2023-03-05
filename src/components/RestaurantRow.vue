<template>
  <div class="restaurant--row">
    <h2 class="title">Nos restaurants
      <!-- {{ toto }} -->
    </h2>
    <div class="wrapper--card">
    <Router-link class="restaurant--wrapper" v-for="(restaurant, i) in three_restaurant" :key="i" :to="{name:'Restaurant', params: {name: restaurant.name}}">
      <restaurant-card  :info_restaurant="restaurant"/>

    </Router-link>


</div>
</div>
</template>

<script>
import RestaurantCard from "./RestaurantCard.vue";
export default {
  name: "RestaurantRow",
  components: {
    RestaurantCard,
  },
  props:{
    three_restaurant: Array,
  }
};
</script>

<style lang="scss">
.restaurant--row{

  .restaurant--wrapper{
    width:35%;
  }
    .wrapper--card{
       display: flex; 
        align-items: center;
        justify-content: space-between;
    }
}
</style>