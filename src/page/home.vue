<template>
  <div class="home">
    <RestaurantRow toto="toto"/>
  </div>
</template>

<script>
// IMPORT
import BDD from "../BDD";
import { onMounted } from "vue";

// COMPONENTS
import RestaurantRow from "@/components/RestaurantRow.vue";

export default {
  name: "HomePage",
  components: {
    RestaurantRow,
  },
  setup() {
    class Restaurant {
      constructor(name, note, image, drive_time) {
        this.name = name;
        this.note = note;
        this.image = image;
        this.drive_time = drive_time;
      }
    }
    //var resto = new Restaurant('resto', 4.5, 'img', '45');
    let data_restaurant = [];
    let three_restaurant = [];

    const makeDataRestaurant = () => {
      for (const restaurant of BDD) {
        const new_restaurant = new Restaurant(
          restaurant.name,
          restaurant.note,
          restaurant.image,
          restaurant.drive_time
        );

        if (three_restaurant.length === 2) {
          three_restaurant.push(new_restaurant);
          data_restaurant.push(three_restaurant);
          three_restaurant = [];
        } else {
          three_restaurant.push(new_restaurant);
        }
      }
    };

    onMounted(makeDataRestaurant);
  },
};
</script>

<style>
</style>