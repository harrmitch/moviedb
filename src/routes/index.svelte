<script context="module">
	export async function load({ fetch }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=${
				import.meta.env.VITE_API
			}&language=en-US&page=1`
		);
		const data = await res.json();
		if (res.ok) {
			return { props: { popular: data.results } };
		}
	}
</script>

<script>
	import Movies from '../components/Movies.svelte';
	import Search from '../components/Search.svelte';
	import { fly } from 'svelte/transition';
	export let popular;
</script>

<svelte:head>
	<title>Popular Movies</title>
</svelte:head>

<Search />

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ y: 50, duration: 500 }}>
	<h3>Popular Movies</h3>
	<Movies movies={popular} />
</section>

<style>
	h3 {
		padding: 0 1rem;
	}
</style>
