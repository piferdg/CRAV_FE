<template>
  <div class="restaurantCard">
    <h1>Name: {{restaurantName}}</h1>
    <h2>Address: {{restaurantAddress}}</h2>
        <iframe
            width="250"
            height="250"
            frameborder="0" style="border:0"
            src="https://www.google.com/maps/embed/v1/view?key=AIzaSyCHy2l3K0UCngroR59ogIe6dYUgcpo_uuc&center=39.7392,-104.9903&zoom=10&maptype=satellite">
        </iframe>
  </div>
</template>

<script>
  export default {
    name: "BasicCard",
    
    props: {
      restaurantName: String,
      restaurantAddress: String
    }
}



</script>

<style>
.restaurantCard{
  border: 1px solid black;
  margin: 5px;
  background-color: lightgray;
  width: 300px
}
</style>
