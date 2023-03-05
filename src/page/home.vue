<template>
  <div class="home">
    <div class="header">
      <img
        src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
      />
      <input type="text" placeholder="De quoi vous avez envie? " />
    </div>
    <div class="bannier"></div>
    <RestaurantRow
      v-for="(data, i) in data_restaurant"
      :key="i"
      :three_restaurant="data"
    />
  </div>
</template>

<script>
// IMPORT
import BDD from "../BDD";
import { onMounted, ref } from "vue";

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
    let data_restaurant = ref([]);
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
          data_restaurant.value.push(three_restaurant);
          three_restaurant = [];
        } else {
          three_restaurant.push(new_restaurant);
        }
      }
    };

    onMounted(makeDataRestaurant);

    //return
    return {
      data_restaurant,
    };
  },
};
</script>

<style lang="scss">
.home {
  .header {
    height: 120px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    img {
      width: 200px;
    }
    input {
      background: color #f6f6f6;
      border: none;
      height: 60px;
      width: 400px;
      outline: none;
      padding-left: 20px;
    }
  }
  .bannier{
    height:200px;
    width: 100%;
    background-image: url("https://blog.studentsville.it/wp-content/uploads/2018/12/UberEATS-il-food-delivery-travolge-la-sharing-economy-_.jpg");
    background-size: cover;
    background-position: center center;
  }
}
</style>