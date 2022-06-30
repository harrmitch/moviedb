<script>
	import { goto } from '$app/navigation';

	let input = '';
	let active = false;
	let placeholder = 'Search Movies';
	$: if (active) {
		placeholder = '';
	} else {
		placeholder = 'Search Movies';
	}
	const submitSearch = () => {
		goto(`/search/${input}`);
	};
</script>

<header class="hero">
	<div class="hero-inner">
		<form class="hero-form" on:submit|preventDefault={submitSearch}>
			<div class="hero-form-input">
				<input
					bind:value={input}
					on:focus={() => {
						active = true;
					}}
					on:blur={() => {
						active = false;
					}}
					class={input ? 'hero-text-input selected' : 'hero-text-input'}
					{placeholder}
					type="text"
					required
				/>
				{#if input}
					<button type="submit" class="hero-form-submit">Search</button>
				{/if}
			</div>
		</form>
	</div>
</header>

<style>
	.hero {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 2rem;
	}

	.hero-inner {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2rem;
		max-width: 900px;
		margin: auto;
	}

	.hero-form {
		margin-top: 1rem;
	}

	@media (min-width: 700px) {
		.hero-form {
			margin-top: 2rem;
		}
	}

	.hero-form-input {
		display: grid;
		grid-template-columns: 1fr;
	}

	@media (min-width: 400px) {
		.hero-form-input {
			display: grid;
			grid-template-columns: 1fr auto;
		}
	}

	.hero-text-input {
		padding: 1rem;
		box-sizing: border-box;
	}

	.hero-form-submit {
		background-color: #f50057;
		color: #fff;
		border: none;
		padding: 1rem 2rem;
		margin-top: 0.5rem;
	}

	@media (min-width: 400px) {
		.hero-form-submit {
			margin-top: 0;
		}
	}
	input.selected {
		background-color: rgb(200, 200, 200);
	}
</style>
