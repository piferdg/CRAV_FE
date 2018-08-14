<template>
  <div id="app">
    <p class="logo">CRāV</p>
    <h3>Find a restaurant by selecting a food genre!</h3>
    <!-- <form> -->
    <select v-model="selected">
      <option :value= null></option>
      <option v-for='genre in genreList' :key='genre'>{{genre}}</option>
    </select>
  <div class="cardList">
      <BasicCard v-for="restaurant in queriedRestaurants" :restaurantName='restaurant.name' :restaurantAddress='restaurant.address' :key='restaurant'/> 
  </div>
  </div>
</template>


<script>
import BasicCard from './components/BasicCard'
export default {
  name: "App",
  components: {
    BasicCard
    // Our app components here
  },

  data() {
    return {
      // this is our 'state', app data
      apiUrl: "",
      currentGenre: "",
      genreList: [],
      queriedRestaurants: [],
      queriedFoods: [],
      restaurantList: [],
      foodList: [], 
    };
  },

  computed: {
    selected: {
      get () {
        return null
      },
      set (optionValue) {
        this.currentGenre = optionValue
        this.queriedRestaurants = [{name: 'pizza hut', address:"123 here place"},{name: 'McDonalds', address:"1 way street"}]
        console.log(this.queriedRestaurants)
      }
    }
  },

  methods: {
    populateGenre() {
      this.genreList = ["Italian", "American", "Mexican"];
    },
    populateFoods() {
      this.foodList = ["tacos", "hamburgers", "pizza", "burritos"];
    },
    populateRestaurants() {
      this.restaurantList = [
        "Taco Bell",
        "McDonalds",
        "Fazolis",
        "Piccolos",
        "Pizza Hut"
      ];
    },
    getRestaurantByGenre(event) {
      console.log('CLICK', event)
    },
    getFoodByGenre() {},
    getFoodByRestaurant() {}
  },

  mounted() {
    this.populateGenre();
    this.populateFoods();
    this.populateRestaurants();
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo{
  color: blue;
  font-size: 50px;
}

.cardList{
  display:flex;
  justify-content: center;
  margin: 10px;
}
</style>

