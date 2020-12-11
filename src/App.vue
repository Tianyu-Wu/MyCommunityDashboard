<template>
  <div id="app">
    <div class="bg-dark h-screen flex">
      <!-- side nav -->
      <div class="w-60 bg-blue-400 h-full flex-none shadow-lg rounded-r-lg">
        <div class="p-6 text-white font-bold text-3xl">
          Everything-about-my-community
        </div>

        <div class="h-px w-full bg-blue-50 my-3"></div>

        <div class="mx-3">
          <button v-for="page in pages" :key="page.id" @click="setID = page.id" class="w-full rounded px-3 py-3 flex items-center justify-start text-white hover:bg-blue-300" :class="[setID===page.id ? 'bg-blue-300 font-semibold' : '']">{{page.name}}</button>
        </div>
      </div>
      <!-- home screen -->
      <div v-if="setID=='dashboard'" class="w-full h-full relative bg-light">
        <div class="h-3/5 container shadow-lg">
          <web-map/>
        </div>
        <div class="h-2/5">
          <chart-container/>
        </div>
      </div>

      <div v-if="setID=='about'" class="w-full h-full relative bg-light">
        <About/>
      </div>
      <div v-if="setID=='source'" class="w-full h-full relative bg-light">
        <Source/>
      </div>

    </div>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->

    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import WebMap from './components/WebMap.vue'
import ChartContainer from './components/ChartContainer.vue'
import About from './components/About.vue'
import Source from './components/Source.vue'

export default {
  name: 'App',
  components: {
    WebMap,
    // HelloWorld
    ChartContainer,
    About,
    Source
  },
  data: () => ({
    pages: [
      {id: "dashboard", name: "Dashboard"}, 
      {id: "about", name: "About Me"},
      {id: "source", name:"Data & Legal Notice"},
],
    setID: "dashboard"
  })
}
</script>

<style src="./assets/tailwind.css">

