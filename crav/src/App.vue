<template>
  <div id="app">
    <div class="main">
      <div class="logo-text">
        <p class="logo">CRāV</p>
        <h3>Find a restaurant by selecting a food genre!</h3>   
        <select v-model="selected">
          <option :value= null></option>
          <option v-for='genreObject in genreList.genre' :key='genreObject.id'  v-bind:value="genreObject.id" >{{genreObject.genre}}</option>
        </select>
      </div>
      <div class="cardList">
        <BasicCard v-for= "restaurant in queriedRestaurants.genre" :restaurantName='restaurant.name' :restaurantAddress='restaurant.address' :key='restaurant'/> 
      </div>
    </div>
    <div class="footer">
      <Footer />
    </div>
  </div>
</template>


<script>
import BasicCard from "./components/BasicCard";
import Footer from "./components/Footer"
export default {
  name: "App",
  components: {
    BasicCard,
    Footer
    // Our app components here
  },

  data() {
    return {
      // this is our 'state', app data
      apiUrl: "",
      currentGenre: "",
      genreList: [],
      queriedRestaurants: [],
      restaurantList: []
    };
  },






  computed: {
    selected: {
      get() {
        return null;
      },
      set(optionValue) {
        this.currentGenre = optionValue;



       fetch("https://cors-anywhere.herokuapp.com/https://crav.herokuapp.com/genre/"+optionValue, {
      method: "get",
      // mode: "cors",
      credentials: "same-origin",
      headers: new Headers({ "Content-Type": "application/json" })
    })
      .then(resp => resp.json())
      .then(resp => {
        this.queriedRestaurants = resp;
        console.log(resp);
      });
   



        // this.queriedRestaurants = [
        //   { name: "pizza hut", address: "123 here place" },
        //   { name: "McDonalds", address: "1 way street" }
        // ];




        console.log(this.queriedRestaurants);
      }
    }
  },

  methods: {
    populateGenre() {
      // this.genreList = ["Italian", "American", "Mexican"];
   
   
       fetch("https://cors-anywhere.herokuapp.com/https://crav.herokuapp.com/genre", {
      method: "get",
      // mode: "cors",
      credentials: "same-origin",
      headers: new Headers({ "Content-Type": "application/json" })
    })
      .then(resp => resp.json())
      .then(resp => {
        this.genreList = resp;
        console.log(resp);
      });
   
   
   },

    // populateRestaurants() {
    //   this.restaurantList = [
    //     "Taco Bell",
    //     "McDonalds",
    //     "Fazolis",
    //     "Piccolos",
    //     "Pizza Hut"
    //   ];
    // },
    getRestaurantByGenre(event) {
      console.log("CLICK", event);
    },
    getFoodByGenre() {},
    getFoodByRestaurant() {}
  },

  mounted() {
    this.populateGenre();
    // this.populateRestaurants();
  }
};
</script>

<style>

body {
  background-image: url("./assets/background_image.png");
  background-repeat: no-repeat;
  background-size: cover;
  margin-left: 300px;
  margin-right: 300px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  height: 80vw;
}

.logo {
  color: blue;
  font-size: 50px;
  background: whitesmoke;
  border-radius: 25px;
}

.main {
  background: rgb(255, 255, 255, 0.8); 
  border-radius: 25px; 
}

.cardList {
  display: flex;
  justify-content: center;
  margin: 10px;
}

.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  color: white;
}

</style>

