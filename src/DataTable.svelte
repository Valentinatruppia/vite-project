<script>
  import { onMount, defineComponent } from "svelte";
  
  export default defineComponent({
    name: "Tabella",
    props: {},
    onMount() {
      // Carica i dati dal file
      const dati = await fetch("incidenti.json").then((response) => response.json());
  
      // Crea la tabella
      const tabella = document.createElement("table");
      tabella.classList.add("tabella");
  
      // Aggiungi le intestazioni
      const intestazioni = ["IDProtocollo", "IDVeicolo", "Progressivo", "TipoPersona", "Sesso", "TipoLesione", "Deceduto", "CinturaCascoUtilizzato", "Airbag", "DecedutoDopo"];
      for (const intestazione of intestazioni) {
        const colonna = document.createElement("th");
        colonna.textContent = intestazione;
        tabella.appendChild(colonna);
      }
  
      // Aggiungi le righe
      for (const dato of dati) {
        const riga = document.createElement("tr");
  
        for (const chiave in dato) {
          const cella = document.createElement("td");
          cella.textContent = dato[chiave];
          riga.appendChild(cella);
        }
  
        tabella.appendChild(riga);
      }
  
      // Aggiungi la tabella al DOM
      document.body.appendChild(tabella);
    },
  });
  </script>
  
  <style>
  table {
    border-collapse: collapse;
    width: 100%;
  }
  
  th,
  td {
    border: 1px solid black;
    padding: 5px;
  }
  </style>
  