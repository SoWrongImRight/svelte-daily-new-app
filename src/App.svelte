<script>
	export let name;

	import { onMount } from 'svelte';

	const apiKey = "9844969a6fa14dffb8dbfd7c5ed8b620"
	const url = `https://newsapi.org/v2/everything?q=comics&sortBy=publishedAt&apiKey=${apiKey}`;
	let articles = []

	onMount(async function() {
		const response = await fetch(url);
		const json = await response.json();
		articles = json["articles"];
	})
</script>

<main>
	<h1>
		<img src="https://dailyplanetdc.files.wordpress.com/2018/12/cropped-daily-planet-logo.jpg?w=656&h=146" />
		<p class="about">
			The Daily Planet is where heroes are born and the story continues. We are proud to report on the planet, daily.
		</p>
	</h1>
	<div class="container">
		{#each articles as article}
			<div class="card">
				<img src="{article.urlToImage}">
				<div class="card-body">
					<h3>{article.title}</h3>
					<p>{article.description}</p>
					<a href="{article.url}">Read story</a>
				</div>
			</div>
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>

