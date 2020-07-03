<template lang="html">

<div class="search-body-results" v-if="body" id="body-detail">
      <h2>{{body.englishName}}</h2>
      <p><span>Radius</span>: {{body.meanRadius}}</p>
      <p><span>Revolution Around Sun</span>: {{body.sideralOrbit}}</p>
      <p><span>Rotation Period</span>: {{body.sideralRotation}}</p>
      <p><span>Mass</span>: {{body.mass.massValue}}</p>
      <p><span>Density</span>: {{body.density}}</p>
      <p><span>Gravity</span>: {{body.gravity}}</p>

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

<style>
</style>