<script>
  import { onMount } from "svelte";

  let dati = [];

  onMount(async () => {
    // Carica i dati dal file
    dati = await fetch("https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json").then((response) => response.json());
  });
</script>

<style>
  body {
    overflow: hidden; /* Impedisce lo scrolling sulla pagina principale */
    margin: 0; /* Rimuove il margine predefinito */
  }

  .tabella-container {
    max-width: 95vw; /* Imposta la larghezza massima a 95% della larghezza della viewport */
    max-height: 80vh; /* Imposta l'altezza massima a 80% dell'altezza della viewport */
    overflow-y: auto;  /* Abilita lo scrolling verticale se necessario */
    margin: 20px auto; /* Aggiunge margine per una migliore presentazione e centra la tabella */
  }

  .tabella {
    border-collapse: collapse;
    width: 100%;
  }

  .tabella th, .tabella td {
    border: 2px solid black; /* Imposta i bordi a 2px di spessore e colore nero */
    padding: 8px;
    text-align: left;
  }

  .tabella th {
    background-color: #f2f2f2;
    position: sticky;
    top: 0;
  }
</style>

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
