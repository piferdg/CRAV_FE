<template>
  <div id="app">
    <div class="main">
      <div class="logo-text">
        <div class="logo">CRāV</div>
        <h3>Find a restaurant by selecting a food genre!</h3>   
        <select v-model="selected" :required="true">
          <option :value= null>Select a genre</option>
          <option v-for='genreObject in genreList.genre' 
            v-bind:value="genreObject.id"  
            :key='genreObject.id'  
            >{{genreObject.genre}}
          </option>
        </select>
      </div>
      <div class="cardList">
        <BasicCard v-for= "restaurant in queriedRestaurants.genre" 
          :restaurantName='restaurant.name' 
          :restaurantAddress='restaurant.address' 
          :phoneNumber='restaurant.phoneNumber' 
          :key='restaurant.name'/> 
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
  },

  data() {
    return {
      currentGenre: "",
      genreList: [],
      queriedRestaurants: []
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
        });
      }
    }
  },

  methods: {
    populateGenre() {
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
  },

  mounted() {
    this.populateGenre();
  }
};
</script>

<style>

body {
  background-image: url("./assets/background_image.png");
  background-repeat: no-repeat;
  background-size: cover;

  /* margin-left: 280px;
  margin-right: 280px; */

  margin-left: 10vw;
  margin-right: 10vw;
  background-attachment: fixed;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  /* height: 80vw; */
}


.logo {
  color: blue;
  font-size: 50px;
  background: whitesmoke;
  border-radius: 25px;

  text-shadow: 3px 3px 3px #888888;
  box-shadow:  7px 7px 8px #888888, 7px 7px 8px #888888 inset;
  font-weight: bolder;
  border: 5px double blue;
}

.logo-text{
  margin: 10px;
  padding: 10px;    
}

.main {
  background: rgba(255, 255, 255, 0.699); 
  border-radius: 25px; 
}

.cardList {
  display: flex;
  justify-content: center;
  margin: 5px;
  flex-wrap: wrap;
}

.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  color: white;

  background-color: rgba(71, 129, 238, 0.37);
  font-weight: bolder;
  padding: 10px;
  animation: colors 10s infinite;
}

select {
  box-shadow: 5px 5px 5px #888888;
  font-size: larger;
}

h1{
  margin: 7px;
  padding: 0;
}

h2{
  margin: 7px;
  padding: 0;
}

</style>

