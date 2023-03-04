<template>
  <div class="restautant--row">
    <h2 class="title">Nos restautants</h2>
<div class="wrapper--card">
    <restaurant-card v-for="(card, index) in 3" :key="index" />

</div>
</div>
</template>

<script>
import RestaurantCard from "./RestaurantCard.vue";
export default {
  name: "RestautantRow",
  components: {
    RestaurantCard,
  },
};
</script>

<style lang="scss">
.restautant--row{
    .wrapper--card{
       display: flex; 
        align-items: center;
        justify-content: space-between;
    }
}
</style>