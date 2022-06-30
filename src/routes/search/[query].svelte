<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${import.meta.env.VITE_API}&query=${
				params.query
			}&language=en-US&page=1&include_adult=false`
		);
		const data = await res.json();
		console.log(data);
		if (res.ok) {
			return { props: { results: data.results, query: params.query } };
		}
	}
</script>

<script>
	import Movies from '../../components/Movies.svelte';
	export let results, query;
</script>

<h1>Search results for: {query}</h1>
<Movies movies={results} />
