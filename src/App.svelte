<script>
// @ts-nocheck
	let url = "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"

	import fetchStore from './fetch.js'
	const [data, loading, error, get] = fetchStore(url)
	import Menu from './lib/Menu.svelte'
	import VolunteerCards from './Table/VolunteerCards.svelte';
	let name = 'world';
</script>
	<h1>CRASH ANALYZER</h1>
<Menu />  	
<VolunteerCards />

<main>
	<section class="content">
    <button on:click={get}>
    Fetch again
    </button>

    {#if $loading}
      Loading: {$loading}
    {:else if $error}
      Error: {$error}
    {:else}
      <pre>{JSON.stringify($data, null, 2)}</pre>
    {/if}
	</section>

</main>

<style>

	:global(body) {
		margin: 0;
		padding: 0;
	}
	main {
		text-align:center;
		grid-template:
			"nav content" min-content
	}
	.content {
		grid-area: content;
	}
</style>