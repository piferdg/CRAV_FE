<template>
  <div class="restaurantCard">
    <h1>{{restaurantName}}</h1>
    <h2>{{restaurantAddress}}</h2>
    <h2>{{phoneNumber}}</h2>
    <iframe width="250" 
            height="250" 
            frameborder="50" 
            style="border:5" 
            v-bind:src="'https://www.google.com/maps/embed/v1/place?key=AIzaSyDTfJcR5J2RRCqBnDS571ltEf2KYdao7Uo&q='+restaurantAddress" 
            allowfullscreen>
      </iframe>
  </div>
</template>

<script>
  export default {
    name: "BasicCard",
  
    props: {
      restaurantName: String,
      restaurantAddress: String,
      phoneNumber: String,
    }
  }
</script>

<style>
  .restaurantCard {
    border-top: 1px solid rgb(201, 201, 201);
    border-bottom: 1px solid rgb(100, 100, 100);
    border-left: 1px solid rgb(201, 201, 201);
    border-right: 1px solid rgb(100, 100, 100);
    margin: 15px;
    background: linear-gradient(to bottom right, rgb(235, 244, 255), rgb(192, 220, 255));
    width: 290px;
    margin-bottom: 25px;
    border-radius: 10px;
    padding: 10px;
    box-shadow: 7px 7px 8px #888888, 7px 7px 8px #ffffff inset, -5px -5px 6px #7796b3 inset;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  iframe {
    align-self: center;
    margin-top: 20px;
    margin-bottom: 20px;
  }
</style>
