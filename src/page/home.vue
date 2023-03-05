<template>
  <div class="home">
    <div class="header">
      <img
        src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
      />
      <div class="wrapper--input">
        <input
          v-model="user_searchrestaurant"
          type="text"
          placeholder="De quoi vous avez envie? "
        />
        <div class="search">
          <div v-for="(restaurant,i) in search_restaurant" :key="i" class="container--restaurant-search">
            <div class="wrapper-img">
              <img :src="restaurant.image" />
            </div>
            <p>{{  restaurant.name }}</p>
          </div>
        </div>
      </div>
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
import { onMounted, ref, watch } from "vue";

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
    let all_restaurant = [];
    let three_restaurant = [];

    const makeDataRestaurant = () => {
      for (const restaurant of BDD) {
        const new_restaurant = new Restaurant(
          restaurant.name,
          restaurant.note,
          restaurant.image,
          restaurant.drive_time
        );

        all_restaurant.push(new_restaurant);
        if (three_restaurant.length === 2) {
          three_restaurant.push(new_restaurant);
          data_restaurant.value.push(three_restaurant);
          three_restaurant = [];
        } else {
          three_restaurant.push(new_restaurant);
        }
      }
    };

    ///////// USER SEARCH RESTAURANT
    let user_searchrestaurant = ref("");
    let search_restaurant = ref([]);
    watch(user_searchrestaurant, (newValue) => {
      let regex = RegExp(newValue.toLowerCase());
      
      let new_search_restaurant = all_restaurant.filter((restarant) =>
        regex.test(restarant.name.toLowerCase())
      );


      newValue == 0  ? search_restaurant.value = [] : search_restaurant.value = new_search_restaurant; 

    //   if(newValue ==0 ){
    //     search_restaurant.value = [];
    //   }else{
    //     search_restaurant.value = new_search_restaurant;
    //   }
    //   //console.log(search_restaurant);
    });
    //
    onMounted(makeDataRestaurant);

    //return
    return {
      data_restaurant,
      user_searchrestaurant,
      search_restaurant,
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
    .wrapper--input {
      position: realtive;
      input {
        background: color #f6f6f6;
        border: none;
        height: 60px;
        width: 400px;
        outline: none;
        padding-left: 20px;
      }
      .search {
        position: absolute;
        // top:100%;
        width: 100%;
        background: hsl(0, 0%, 94%);
        .container--restaurant-search {
          display: flex;
          align-items: center;
          padding: 10px;
          &:hover{
            background: #f5f5f5;
          }
          .wrapper-img{
            height: 40px;
            width: 40px;
            border-radius: 50%;
            overflow: hidden;
            margin-right: 25px;
            img{
                height: 100%;
            width: auto; 
            }
          }
        }
      }
    }
  }
  .bannier {
    height: 200px;
    width: 100%;
    background-image: url("https://blog.studentsville.it/wp-content/uploads/2018/12/UberEATS-il-food-delivery-travolge-la-sharing-economy-_.jpg");
    background-size: cover;
    background-position: center center;
  }
}
</style>