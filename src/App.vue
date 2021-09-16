<template>
  <div id="app">
    <Products/>
  </div>
</template>

<script>
// components
import Products from "./components/Products.vue"

export default {
  name: 'App',
  components: {
    Products,
  }
}
</script>

<style>

  *{
    box-sizing: border-box;
  }
  
  body{
    margin: 0
  }

  html, body, #app{
    height: 100%;
  }
</style>
