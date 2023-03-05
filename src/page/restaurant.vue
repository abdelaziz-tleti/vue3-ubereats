<template>
    <RouterLink to="/">
        <div id="return">Retour à la Home</div>
    <br>
    </RouterLink>
   
  <!-- <p>{{ $route.params.name }}</p> -->
  <img :src="restaurant.image">
  <p>{{ restaurant.name }}</p>
  <p>note du restaurant {{ restaurant.note }}</p>
  <p>temps de livraison {{ restaurant.drive_time }}</p>

</template>

<script>
// import { onMounted } from "vue";
import { useRoute } from "vue-router";
import BDD from "../BDD";
export default {
  name: "RestaurantPage",
  setup() {
    const route = useRoute();
    const restaurant =  BDD.find((restaurant) => 
        restaurant.name === route.params.name
      );

      return{
        restaurant
      }
    // onMounted(() => {
    //     console.log(restaurant);  
    // //   console.log(
    // //   BDD.find((restaurant) => {
    // //     if (restaurant.name === route.params.name) {
    // //       return restaurant;
    // //     }
    // //   }));
    // });
  },
};
</script>

<style lang="scss" scoped>
#return{
    margin: 25px 45px;
    font-weight: 600;
    cursor: pointer;
    &:hover{
        font-weight: 1000;
        color:rgb(60, 0, 255);
    }
}
</style>