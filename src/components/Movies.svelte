<script>
	export let movies;
	import MovieCard from './MovieCard.svelte';
</script>

<div class="movies">
	{#each movies as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
	}
</style>
