<template lang="html">

<div class="search-body-results" v-if="body" id="body-detail">
      <h2>{{body.englishName}}</h2>
      <p><span>meanRadius</span>: {{body.meanRadius}} km</p>
      <p><span>Sideral Orbit Time (Around Sun or Parent Planet)</span>: {{body.sideralOrbit}} Earth Days</p>
      <p><span>Sideral Rotation Period</span>: {{body.sideralRotation}} hours</p>
      <p><span>Mass</span>: {{body.mass.massValue}} 10<sup>n</sup> kg</p>
      <p><span>Density</span>: {{body.density}} g.cm<sup>3</sup></p>
      <p><span>Gravity</span>: {{body.gravity}} m.s<sup>-1</sup></p>
      <p><span>Orbiting Planet (if applicable)</span>: {{body.aroundPlanet.planet}}</p>
      <p><span>Discovered By:</span> {{body.discoveredBy}} {{body.discoveryDate}} </p>

</div>
      
</template>

<script>
import { eventBus } from '../main.js'

export default {
      name: 'solar-system-details',
      data(){
            return {
                  body: null
            }
      },
      mounted(){
            eventBus.$on('body-selected', (body) => {
                  this.body = body
            })
      }
}

</script>

<style scoped>

.search-body-results {
      margin-left: 20px;
}

</style>>
