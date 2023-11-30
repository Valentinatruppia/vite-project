
<script>
	import { flip } from 'svelte/animate';
	import Spinner from './spinner.svelte';
	
	
	let things = [];
	let colNames = [];
	let rowkeys = [];
	
	async function getThings(){
		
		
	const res = await 
		fetch(`https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json`);
		const json = await res.json();

		if (res.ok) {
			
			setTimeout(() => {
				things = json;				
				//grab column names
				colNames = Object.keys(things[0])
				
				return true;
			}, 0 * Math.random())
			
		} else {
			throw new Error(text);
		}
		
	}
	
	
	let promise = getThings();
	
	function onDelete(id) {
		things = things.filter(t => t.id != id)
	}

	
	let sortBy = {col: "name", ascending: true};
	
	$: sort = (column) => {
		
		if (sortBy.col == column) {
			sortBy.ascending = !sortBy.ascending
		} else {
			sortBy.col = column
			sortBy.ascending = true
		}
		
		// Modifier to sorting function for ascending or descending
		let sortModifier = (sortBy.ascending) ? 1 : -1;
		
		let sort = (a, b) => 
			(a[column] < b[column]) 
			? -1 * sortModifier 
			: (a[column] > b[column]) 
			? 1 * sortModifier 
			: 0;
		
		things = things.sort(sort);
	}
	
</script>

<button on:click={sort("IDProtocollo")}>IDProtocollo &varr;</button>


{#await promise}
	<Spinner/>
{:then getThings}

<table>
	<thead>
	<tr>
		{#each colNames as col}
	<th on:click={sort(col)}>{col} &varr;</th>
{/each}
	</tr>
	</thead>
	<tbody>
		
		{#each things as thing, index (thing.id)}

		<tr>
			{#each colNames as col, index}
			<td>{thing[col]}</td>
			{/each}
		</tr>
		{/each}
	
	</tbody>
</table>



{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

<style>
	table {
		max-width: 100%;
    border: 0;
    white-space: nowrap;
    border-collapse: collapse;
		border: 1px solid rgba(0,0,0,.12);
		border-radius: 4px;
	}
	
	th {
		height: 56px;
		font-family: Roboto,sans-serif;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    font-size: .875rem;
    line-height: 1.375rem;
    font-weight: 500;
    letter-spacing: .00714em;
    text-decoration: inherit;
    text-transform: inherit;
    text-align: left;
		padding-right: 16px;
    padding-left: 16px;
	}
	
	tbody {
		font-family: Roboto,sans-serif;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    font-size: .875rem;
    line-height: 1.25rem;
    font-weight: 400;
    letter-spacing: .01786em;
    text-decoration: inherit;
    text-transform: inherit;
	}
	tr {
		height: 52px;
		border-top-color: rgba(0,0,0,.12);
    border-top-width: 1px;
    border-top-style: solid;
	}
	tr:hover{
		background-color: rgba(0,0,0,.04);
	}
	
	td {
		padding-right: 16px;
    padding-left: 16px;
	}
</style>
