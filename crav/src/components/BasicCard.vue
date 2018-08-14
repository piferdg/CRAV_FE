<template>
  <div>
    <h1>Restaurant Name is: {{restaurantName}}</h1>
  </div>
</template>

<script>
  export default {
    name: "BasicCard",
    
    props: {
      restaurantName: String
    }
}



</script>

<style>
</style>
