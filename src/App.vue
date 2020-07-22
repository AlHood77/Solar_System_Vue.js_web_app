<template>
  
  <div id="#App">

    <header class="header">
      <h1>Solar System App</h1>
      <p>Search all the planets, dwarf planets, moons and the main asteroids in our Solar System.</p>
    </header>

    <div class="components-container">

        <div class="wrapper">

          <div class="details-wrapper">

             <div class="App-list">
              <solar-system-list :solarSystemBodies='solarSystemBodies'></solar-system-list>
            </div>

            <div class="object-info">
              <solar-system-details />
            </div>

          </div>
          

            <div class="nasa-stuff">
              <nasa-image class="nasa"></nasa-image>
            </div>

        </div>

              
        
            
        
    
        <div class="Articles">
          <science-news-list></science-news-list>
        </div>
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
        
       
      }
    },
    methods: {

    },
    mounted() {
      fetch("https://api.le-systeme-solaire.net/rest/bodies/")
      .then(res => res.json())
      .then(solarSystemBodies => this.solarSystemBodies = solarSystemBodies)
          
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

@import url('https://fonts.googleapis.com/css2?family=Vollkorn&display=swap');

* {
  box-sizing: border-box;
  margin: 0;

}


html, body {
  background-image: linear-gradient( 99.9deg, rgba(27,24,31,1) 21.2%, rgba(50,4,89,1) 84.8% );
  
}

.header {
  padding: 60px;
  text-align: center;
  background: url(assets/space.png);
  background-position: center;
  color: white;
  font-size: 20px;
}

.wrapper {
  display: flex;
  justify-content: space-around;
}

.App-list {
  text-align: center;
}

.nasa {
  margin-top: 20px;
}

.nasa-stuff {
  text-align: center;
}



</style>