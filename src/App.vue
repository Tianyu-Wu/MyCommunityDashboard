<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <web-map/>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import WebMap from './components/WebMap.vue'

export default {
  name: 'App',
  components: {
    WebMap,
    // HelloWorld
  }
}
</script>

<style src="./assets/tailwind.css">

