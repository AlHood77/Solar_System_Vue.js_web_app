<template>
	<div class="image-container">
		<div class="nasa-search-container">
			<h3>Search images from NASA's image library</h3>
			
				<input class="input" type="text" placeholder="Enter something" v-model="query" />
				<input class="submit" type="submit" @click="getResult" />
		

			<div class="cards">
				<div class="card" v-for="result in results.slice(0, 4)">
					<img class="card-img-top" :src="result.links[0].href" alt="" />
					<div class="card-body">
						<h2>{{ result.data[0].title }}</h2>
						<p class="card-text">{{ result.data[0].description }}</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import { eventBus } from "../main.js";

	export default {
		name: "nasa-image",
		data() {
			return {
				results: [],
				query: "",
				body: "",
			};
		},
		methods: {
			getResult: function() {
				fetch(
					`https://images-api.nasa.gov/search?q=${this.query}&media_type=image`
				)
					.then((response) => {
						return response.json();
					})
					.then((parsedJson) => {
						this.results = parsedJson["collection"]["items"];
					});
			},
		},
		mounted() {
			eventBus.$on("body-selected", (body) => {
				this.query = body.englishName;
			});
		},
	};
</script>

<style scoped>

    .nasa-search-container {
        margin-left: 20px;
        margin-right: 20px;
        margin-bottom: 30px;
    }

    .input {
        width: 380px;
    }
    .submit {
        margin-bottom: 20px;
    }
	.cards {
		margin: 0 auto;
		max-width: 1800px;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 20px;
	}

	.card {
		box-shadow: 0 0 4px rgba(247, 245, 243, 0.671);
	}

	img {
        width: 100%;
        height: 300px;
        display: block;
    }
    
    .card-body{
        font-size: 1em;
        background: #fafafa;
    }
</style>
