<template>
  <div id="app">
    <h3>Find a resturant by selecting a food genre!</h3>
    <!-- <form> -->
    <select v-model="selected">
      <option :value= null></option>
      <option v-for= 'genre in genreList'>{{genre}}</option>
    </select>
    <p v-for="resturant in queriedResturants">{{resturant}}</p>
    <!-- <button v-on:click= getResturantByGenre>Submit</button> -->
    <!-- </form> -->
  </div>
</template>


<script>
import BasicCard from './components/BasicCard'
export default {
  name: "App",
  components: {
    // Our app components here
  },

  data() {
    return {
      // this is our 'state', app data
      apiUrl: "",
      currentGenre: "",
      genreList: [],
      queriedResturants: [],
      queriedFoods: [],
      resturantList: [],
      foodList: []
    };
  },

  computed: {
    selected: {
      get () {
        return null
      },
      set (optionValue) {
        this.currentGenre = optionValue
        this.queriedResturants = ['pizza hut']
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
    populateResturants() {
      this.resturantList = [
        "Taco Bell",
        "McDonalds",
        "Fazolis",
        "Piccolos",
        "Pizza Hut"
      ];
    },
    getResturantByGenre(event) {
      console.log('CLICK', event)
    },
    getFoodByGenre() {},
    getFoodByResturant() {}
  },

  mounted() {
    this.populateGenre();
    this.populateFoods();
    this.populateResturants();
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
</style>

