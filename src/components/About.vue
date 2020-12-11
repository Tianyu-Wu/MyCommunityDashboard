<template>
  <div class="h-full w-full">
      <div class="flex flex-col p-6 shadow-lg m-4 rounded-lg">
        <h1 class="px-6 py-3 text-blue-400 text-3xl font-bold">
        About the project
        </h1>
        <div class="h-px w-full bg-blue-100 mt-4 mb-4"></div>
        <h3 class="text-dark text-base font-light p-3"> {{project1}}</h3>
        <h3 class="text-dark text-base font-light p-3"> {{project2}}</h3>
        <!-- image -->
        <div class="flex justify-center">
            <div v-for="tool in tools" :key="tool.name" :href="`http://${tool.link}`" class="flex flex-col p-3 m-2 justify-center items-center">
                <img class="h-24" :src="require(`../assets/${tool.logo}`)" alt="">
                <div class="text-2xl font-bold bg-dark">{{tool.name}}</div>
            </div>
        </div>
      </div>
          
    <div class="flex flex-col p-6 shadow-lg m-4 rounded-lg">
        <h1 class="px-6 py-3 text-blue-400 text-3xl font-bold">
            About Me
        </h1>
        <div class="h-px w-full bg-blue-100 mt-4 mb-4"></div>
        <h3 class="text-dark text-base font-light p-3"> {{me}}</h3>
      </div>

      
  </div>
</template>

<script>
export default {
    name: "About",
    data: () => ({
        project1: "The weather and air condition are always important factors that affect people’s living quality. During the Corona situation, people now spend most of their time at home and hang around mostly close to the community. Therefore, it may be interesting to create a responsive web app that can inform users about the weather and air conditions about their community. With this regard, I decided to define my neighbourhood (i.e. Kreis Seebach) as my primary study area. As the app aim to provide users with detailed measurement of temperature, PM 2.5, and PM 10 in different timeframe, a dashboard is a good option for a concise and effective visualization. ",
        project2: "This project is in fullfill the assiginemnt 2 of GIS III with SenseBox, ETH Zurich. The web app is made with the following tools.",
        me: "I am Tianyu Wu, a master student in Geomatic Engineering at ETH Zurich.",
        tools: [
            {name:"Vue.js", link:"https://vuejs.org", logo:"logo.png"},
            {name:"Tailwind.css", link:"https://tailwindcss.com", logo:"tailwind-css-logo.svg"},
            {name:"SenseBox", link:"https://sensebox.github.io", logo:"sensebox_logo_raute.png"},
            {name:"ArcGIS JS", link:"https://developers.arcgis.com/javascript/", logo:"ArcGIS_logo.png"}
        ]
    
    })
}
</script>