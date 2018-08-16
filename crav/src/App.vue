<template>
  <div id="app">
    <div class="main">
      <div class="logo-text">
        <div class="logo">CRāV</div>
	      <button v-on:click="collapsed = !collapsed">About Us</button>
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
        <BasicCard v-for="restaurant in queriedRestaurants.genre" :restaurantName='restaurant.name' :restaurantAddress='restaurant.address' :phoneNumber='restaurant.phoneNumber' :key='restaurant.name' />
      </div>
    </div>
    <div id="About-us" v-bind:class= "{'is-collapsed' : collapsed }">
      <h2>Kim Hermosillo</h2>
        <p>Why do hamburgers go to the gym?..... To get better buns.🏋🏼🍔‍</p>
      <h2>Danny Pifer</h2>
        <p>Is a hotdog a sandwich? 🌭 === 🥪?</p>
      <h2>Michael Coons</h2>
        <p>I just bought a cured ham, I wonder what it had? 🤒 🐷</p>
      <h2>Jeff Strunk</h2>
        <p>What was Ludwig van Beethoven's favorite fruit?... Ba-na-na-na! 🍌🎼</p>
    </div>
    <div class="footer">
      <Footer />
    </div>
  </div>
</template>

<script>
import BasicCard from "./components/BasicCard";
import Footer from "./components/Footer";
import AboutUs from "./components/AboutUs";
export default {
  name: "App",
  components: {
    BasicCard,
    Footer,
    AboutUs
  },

  data() {
    return {
      currentGenre: "",
      genreList: [],
      queriedRestaurants: [],
      collapsed: true
    };
  },

  computed: {
    selected: {
      get() {
        return null;
      },
      set(optionValue) {
        this.currentGenre = optionValue;

        fetch("https://crav.herokuapp.com/genre/" + optionValue)
          .then(resp => resp.json())
          .then(resp => {
            this.queriedRestaurants = resp;
          });
      }
    }
  },

  methods: {
    populateGenre() {
      fetch("https://crav.herokuapp.com/genre")
        .then(resp => resp.json())
        .then(resp => {
          this.genreList = resp;
        });
    }
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
}

.logo {
  color: blue;
  font-size: 50px;
  background: whitesmoke;
  border-radius: 25px;
  text-shadow: 3px 3px 3px #888888;
  box-shadow: 7px 7px 8px #888888, 7px 7px 8px #888888 inset;
  font-weight: bolder;
  border: 5px double blue;
}

.logo-text {
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
}

select {
  box-shadow: 5px 5px 5px #888888;
  font-size: larger;
}

h1 {
  margin: 7px;
  padding: 0;
}

h2 {
  margin: 7px;
  padding: 0;
}

#About-us {
  border-top: 1px solid rgb(201, 201, 201);
  border-bottom: 1px solid rgb(100, 100, 100);
  border-left: 1px solid rgb(201, 201, 201);
  border-right: 1px solid rgb(100, 100, 100);
  margin: 15px;
  background: linear-gradient(
    to bottom right,
    rgb(235, 244, 255),
    rgb(192, 220, 255)
  );
  width: 290px;
  margin-bottom: 25px;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 7px 7px 8px #888888, 7px 7px 8px #ffffff inset,
    -5px -5px 6px #7796b3 inset;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 80px;
}

.is-collapsed {
  display: none;
}
</style>