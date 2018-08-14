<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    // Our app components here
  },

  data() {
    return {
      // this is our 'state', app data
      apiUrl: '',
      currentGenre: '',
      genreList: [],
      queriedResturants: [],
      queriedFoods: [],
      resturantList: [],
      foodList: [],
    };
  },

  methods: {
    populateGenre() {
      this.genreList = ['Italian', 'American', 'Mexican'];
    },
    populateFoods() {
      this.foodList = ['tacos', 'hamburgers', 'pizza', 'burritos'];
    },
    populateResturants() {
      this.resturantList = ['Taco Bell', 'McDonalds', 'Fazolis', 'Piccolos', 'Pizza Hut'];
    },
    getResturantByGenre() {

    },
    getFoodByGenre() {

    },
    getFoodByResturant() {

    },
  },

  mounted() {
    this.populateGenre();
    this.populateFoods();
    this.populateResturants();
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
