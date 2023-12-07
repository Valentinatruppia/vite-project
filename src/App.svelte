<script>
	import Menu from './lib/Menu.svelte'
	import DataTable from './Table/DataTable.svelte';
	import DataTablePast from './Table/DataTablePast.svelte';
</script>

<main>
	<h1>CRASH ANALYZER</h1>

	<section class="content">
		<h2>Tabella Dati Incidenti</h2>
		<Menu />

		<div class="tables-container">
			<DataTable />
			<div class="table-separator"></div> <!-- Aggiunto un div separatore -->
			<DataTablePast />
		</div>
	</section>
</main>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		font-family: 'Arial', sans-serif;
		background-color: #f5f5f5; /* Background slightly lighter than white */
		color: #333;
	}

	main {
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
	}

	h1 {
		margin-bottom: 10px;
		font-size: 2.5em;
		color: #2e7d32; /* Green color */
		text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.1); /* Slight text shadow */
	}


	.content {
		width: 100%;
		max-width: 9000px; /* Set a maximum width for the content */
		padding: 20px;
		background-color: #fff;
		box-shadow: 0 2px 4px rgba(66, 56, 56, 1); /* Slight box shadow */
		border-radius: 20px;
		margin-top: 20px; /* Aggiunto spazio sopra il contenuto */
		margin-bottom: 20px; /* Aggiunto spazio sotto il contenuto */
        margin-left: 20px;  /* Aggiunto margine sinistro */
        margin-right: 20px; /* Aggiunto margine destro */
	}
    

	h2 {
		font-size: 1.8em;
		color: #1565c0; /* Blue color */
		margin-bottom: 20px;
	}

	.tables-container {
		display: flex;
		justify-content: space-between; /* Spazio uniforme tra le tabelle */
		margin-top: 2px; /* Aumentato il margine superiore per più spazio */
	}

	.table-separator {
		width: 20px; /* Larghezza del separatore */
	}

	/* Adjust width and height of the DataTable component */
	.table-container {
		flex: 0 0 48%; /* Larghezza massima del 48% per garantire uno spazio adeguato tra le tabelle */
		overflow-x: auto;
		max-height: 250px; /* Adjust the height as needed */
	}

	/* Add additional styles for Menu and DataTable components if needed */
</style>
