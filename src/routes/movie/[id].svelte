<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=${
				import.meta.env.VITE_API
			}&language=en-US`
		);
		const data = await res.json();
		if (res.ok) {
			return { props: { details: data } };
		}
	}
</script>

<script>
	import { fly } from 'svelte/transition';
	export let details;
</script>

<svelte:head>
	<title>{details.title} ({details.release_date.slice(0, 4)})</title>
</svelte:head>

<div
	class="movie-detail"
	in:fly={{ y: 50, duration: 500, delay: 500 }}
	out:fly={{ y: 50, duration: 500 }}
>
	<div class="img-container">
		<img src={`https://image.tmdb.org/t/p/w500${details.backdrop_path}`} alt={details.title} />
	</div>
	<div class="text-container">
		<h1>{details.title}</h1>
		<p class="overview">{details.overview}</p>
		<p>
			<span>Release Date:</span>
			{details.release_date}<br />

			<span>Budget:</span>
			${details.budget}<br />

			<span>Rating:</span>
			{details.vote_average}<br />

			<span>Runtime:</span>
			{details.runtime} minutes
		</p>
	</div>
</div>

<style>
	h1 {
		padding: 1rem 0rem 2rem;
	}
	p {
		padding: 1rem 0rem;
	}
	.img-container {
		width: 100%;
	}
	img {
		width: 100%;
		border-radius: 1rem;
	}
	.movie-detail {
		margin: 2rem 20%;
	}
	span {
		font-weight: bold;
	}
</style>
