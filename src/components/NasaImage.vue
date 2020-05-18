<template>
   
   <div class="search">
       
           <!-- <form v-on:submit.prevent="getResult(query)">
               <input type="text" placeholder="Search Nasa Image Library" v-model="query" />
           </form>
            <div v-for="result in results">
                <img v-bind:src="result.links[0].href" />
            </div> -->

            <input type="text" placeholder="Enter something" v-model="query">
            <input type="submit" @click=getResult>
         
            <div v-for="result in results">
                <h2>{{result}}</h2>
            </div>
   </div>

</template>

<script>
export default {
    name: 'nasa-image',
    data(){
        return {
            results: [],
            query: ''
        }
    },
    methods: {
        getResult: function() {
            fetch(`https://images-api.nasa.gov/search?q=${this.query}&media_type=image`)
            .then(res => res.json())
            .then(res => {
                this.results = ["collection"]["items"];
            })
        }
    }
}
</script>

<style>

</style>