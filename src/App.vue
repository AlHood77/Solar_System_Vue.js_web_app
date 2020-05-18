<template>
  
<div id="#App" class="grid-container">

  <div class="Image">
    <div class="Data-Bar">
      <solar-system-details />
    </div>
    <div class="Image">
      <p>Image</p>
      <nasa-image></nasa-image>
    </div>
  </div>

  <div class="Articles">
    <science-news-list :scienceNews = 'scienceNews'>  </science-news-list>
  </div>

  <div class="search-header">
    <solar-system-list :solarSystemBodies='solarSystemBodies'></solar-system-list>
  </div>

</div>
</template>

<script>
import SolarSystemList from "./components/SolarSystemList.vue";
import SolarSystemDetails from "./components/SolarSystemDetails";

import ScienceNewsList from "./components/ScienceNewsList.vue";

import NasaImage from "./components/NasaImage.vue"

export default {
    name: "App",
    data() {
      return {
        solarSystemBodies: [],
        scienceNews: [],
        nasaImage: []
      }
    },
    methods: {

    },
    mounted() {
      fetch("https://api.le-systeme-solaire.net/rest/bodies/")
      .then(res => res.json())
      .then(solarSystemBodies => this.solarSystemBodies = solarSystemBodies)
      
      fetch("http://newsapi.org/v2/top-headlines?country=gb&category=science&apiKey=44e2ab8a147d4f40bcea6b44a90fc4ca")
      .then(res => res.json())
      .then(scienceNews => this.scienceNews = scienceNews)
      
      fetch("https://images-api.nasa.gov/search?q=sun&media_type=image")
      .then(res=> res.json())
      .then(nasaImage => this.nasaImage = nasaImage)
      },


      components: {
        "solar-system-list": SolarSystemList,
        "solar-system-details": SolarSystemDetails,
        
        "science-news-list": ScienceNewsList,

        "nasa-image": NasaImage
      }
}



</script>

<style>

* {
  box-sizing: border-box;

}

.grid-container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 0.1fr 1.3fr fr;
  gap: 1px 1px;
  grid-template-areas: "search-header" "Image" "Articles";
}

.Image {
  display: grid;
  grid-template-columns: 0.4fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 1px 1px;
  grid-template-areas: "Data-Bar Image Image" "Data-Bar Image Image";
  grid-area: Image;
}

.Data-Bar { 
  grid-area: Data-Bar;
  border: solid blue 1px;
  display: flex;
  justify-content: center;
  height: 300px;

   }

.Image { 
  grid-area: Image;
  border: solid orange 1px;
   }

.Articles { 
  grid-area: Articles;
  border: solid green 1px;
  display: flex;
  flex-direction: row;
  
   }

.search-header { 
  grid-area: search-header;
  border: solid red 1px;
  display: flex;
  justify-content: center;
  align-items: center;

  
  }

</style>