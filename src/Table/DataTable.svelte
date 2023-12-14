<script>
  import { onMount } from "svelte";

  let dati = [];

  onMount(async () => {
    // Carica i dati dal file
    dati = await fetch("https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json").then((response) => response.json());
  });
</script>

{#if dati.length > 0}
  <div class="tabella-container">
    <table class="tabella">
      <thead>
        <tr>
          {#each Object.keys(dati[0]) as intestazione}
            <th>{intestazione}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each dati as dato}
          <tr>
            {#each Object.values(dato) as cella}
              <td>{cella}</td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
{:else}
  <p>Caricamento dati...</p>
{/if}

<style>
  body {
    overflow: hidden;
    margin: 0;
  }

  .tabella-container {
    max-width: 95vw;
    max-height: 80vh;
    overflow-y: auto;
    margin: 20px auto; 
  }

  .tabella {
    border-collapse: collapse;
    width: 100%;
  }

  .tabella th, .tabella td {
    border: 2px solid black;
    padding: 8px;
    text-align: left;
  }

  .tabella th {
    background-color: #f2f2f2;
    position: sticky;
    top: 0;
  }
</style>

