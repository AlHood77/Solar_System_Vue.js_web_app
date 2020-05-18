<template lang="html">

<div>
    
     <form class="body-form" v-on:submit.prevent>
         <input type="text" v-model="search" placeholder="Select a Solar System Object..." v-on:keyup="searchForObject">
         <select v-on:change="handleSelect" v-model="selectedBody">
             <option disabled value="">Select a Solar System Object...</option>
             <option v-for ="body in solarSystemBodies.bodies" :value="body">{{body.englishName}}</option>
         </select>
     </form>
     
</div>
  
</template>

<script>

import { eventBus } from '../main.js'

export default {
    name: 'solar-system-list',
    data(){
        return {
        "search": "",
        "selectedBody": {}
        }
    },

    props: ['solarSystemBodies'],
    methods: {
        searchForObject(){
            let foundObject = this.solarSystemBodies.bodies.find((body) => {
                return body.englishName.toLowerCase().indexOf(this.search.toLowerCase()) > -1
            })
            this.selectedBody = foundObject

            eventBus.$emit('body-selected', this.selectedBody)
        },
        handleSelect(){
            this.search = ""
            eventBus.$emit('body-selected', this.selectedBody)
        }
    }

}
</script>
    

<style>

.body-form {
    display: flex;
    flex-direction: column;
    align-content: center;
    width: 300px;
    }

</style>