<template>
  <div class="h-full w-full">
      <div class="flex flex-row p-6 shadow-lg m-6 rounded-lg justify-items-auto">
          
        <h1 class="px-6 py-3 text-blue-400 text-3xl font-bold text-right">
            Data Sources
        </h1>
        <div class="w-py h-full bg-blue-100 mt-4 mb-4"></div>
        <div class="flex flex-col">
              <h3 class="text-dark text-base font-light p-3"> {{desc}}</h3>
            <p v-for="source in sources" :key="source.name" class="text-dark text-base p-3"> - {{source.name}}: <a :href="source.link" class="text-dark text-base p-3 font-light hover:underline">{{source.link}}</a> <p/>

          </div>
        
      </div>
          
    <div class="flex flex-row p-6 shadow-lg m-6 rounded-lg justify-end">
        
        <h3 class="text-dark text-base font-light p-3"> {{legal}}</h3>
                <div class="w-py h-full bg-blue-100 mt-4 mb-4"></div>

        <h1 class="px-6 py-3 text-blue-400 text-3xl font-bold text-right">
            Legal Notice
        </h1>
      </div>

      <div class="flex flex-row p-6 shadow-lg m-6 rounded-lg">
          
        <h1 class="px-6 py-3 text-blue-400 text-3xl font-bold text-right">
            Privacy
        </h1>
        <div class="w-py h-full bg-blue-100 mt-4 mb-4"></div>
        <div class="flex flex-col">
              <p class="text-dark text-base font-light p-3"> {{privacy}}</p>
          </div>
        
      </div>

      
  </div>
</template>

<script>
export default {
    name: "Source",
    data: () => ({
        desc: "The primary data used is the self-measured SenseBox data, including the air temperature, PM 2.5 and PM 10 measurements. To further enrich the information, external data from OpenSenseMap as well as Stadt Zurich Open Data are also integrated. Below is the list of data sources for this project.",
        legal: "Contents published on this website by the author are subject to Swiss copyright laws. Reproducing, editing, distribution and using outside the scope of the copyright law require the permission of the author. The commercial use of the content without permission of the author is prohibited. Contributions of third parties are indicated as such and listed above.",
        sources: [
            {name:"External Temperature by Sensebox at Schwamendingen", link:"https://opensensemap.org/explore/5e253fd4ff64c1001a8deb27"},
            {name:"External PM 2.5 by Sensebox at Schwamendingen", link:"https://opensensemap.org/explore/5e253fd4ff64c1001a8deb27"},
            {name:"External PM 10 by Sensebox at Schwamendingen", link:"https://opensensemap.org/explore/5e253fd4ff64c1001a8deb27"},
            {name:"District Boundary of Seeback", link:"https://www.stadt-zuerich.ch/geodaten/download/Kreisarchitekteneinteilung?format=10009"}
        ],
        privacy: "This website does not collect any user data or collect any cookies. Should you have any doubt, please contatct via wuti@student.ethz.ch.",
    
    })
}
</script>