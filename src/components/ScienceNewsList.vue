<template lang="html">
	<div class="news-container">
        <h3>Search Solar System news articles from NewsAPI</h3>
			<input class="input" type="text" placeholder="Enter something" v-model="query" />
			<input class="submit" type="submit" @click="getResult" />
		

		<div class="cards">
			<div class="card" v-for="result in results">
				<div class="card">
					<img class="card-img-top" :src="result.urlToImage" />
					<div class="card-body">
						<h4>{{ result.title }}</h4>
						<p class="card-text">{{ result.description }}</p>
						<a :href="result.url" class="card-link">Read More</a>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import { eventBus } from "../main.js";

	export default {
		name: "science-news-list",
		data() {
			return {
				results: [],
				query: "",
				body: "",
			};
		},

		// props: ['scienceNews'],
		components: {},
		methods: {
			getResult: function() {
				fetch(
					`https://newsapi.org/v2/everything?q=${this.query}&apiKey=44e2ab8a147d4f40bcea6b44a90fc4ca`
				)
					.then((response) => {
						return response.json();
					})
					.then((parsedJson) => {
						this.results = parsedJson["articles"];
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

.news-container {
    margin-left: 20px;
    margin-right: 20px;
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
		box-shadow: 0 0 3px rgba(0, 0, 0, 0.1);
	}
</style>
