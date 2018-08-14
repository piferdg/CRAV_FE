<template>
  <div id="app">
    <h1>Resturant Name is: {{key}}</h1>
  </div>
</template>

<script>
export default {
  name: "BasicCard"
};
props: {
  resturantName: String
  key: String
}

</script>

<style>
</style>
