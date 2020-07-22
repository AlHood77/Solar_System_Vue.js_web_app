<template>
	<div class="image-container">
		<div class="nasa-search-container">
			<h3>Search images from NASA's image library.</h3>

			<input
				class="input"
				type="text"
				placeholder="Enter something"
				v-model="query"
			/>
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
	.image-container h3 {
		align-items: center;
	}

	.nasa-search-container {
		margin-left: 20px;
		margin-right: 0px;
		margin-bottom: 30px;
		color: #f2a127;
		
	}

	.input {
		width: 380px;
		margin: 5px 0 0 0;
		display: inline-block;
	}
	.submit {
		margin-bottom: 20px;
		background: #f2a127;
		border: 1px solid #eee;
		border-radius: 20px;
		box-shadow: 2px 2px 5px #eee;
		outline: none;
		display: inline-block;
		margin-left: 10px;
	}

	.submit:hover {
		background: #f2a127d7;
	}

	.submit:active {
		box-shadow: 1px 1px 1px #eee;
	}
	.cards {
		margin: 0 auto;
		max-width: 1800px;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 20px;
	}

	.card {
		box-shadow: 0 2px 7px 0 rgba(247, 246, 246, 0.986),
			0 2px 7px 0 rgba(231, 228, 228, 0.918);
	}

	.card:focus,
	.card:hover {
		box-shadow: 0 5px 11px 0 rgba(0, 0, 0, 0.18),
			0 4px 15px 0 rgba(0, 0, 0, 0.15);
	}

	img {
		width: 100%;
		height: 200px;
		display: block;
	}

	.card-body {
		font-size: 1em;
		background: #fafafa;
	}
</style>
