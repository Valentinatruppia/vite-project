<title>STATISTICS</title>
<script type="module">
  import Menu from "../lib/Menu.svelte";
  require(Menu);
</script>
<script>
function myFunction() {
        window.location.href = '../index.html';
}
</script>

<main>
  <h1>CRASH ANALYZER</h1>
  <section class="content">
    <button onclick="myFunction()">Click me</button>

    <Menu />
  </section>
</main>
<body>   
  <header>
    <h1>STATISTICS</h1>
  </header>
  
  <div class="buttons-container">
    <button type="button" >Maschi e Femmine</button>
    <button type="button">................</button>
    <button type="button">----------------</button>
    <button type="button">''''''''''''''''</button>
    <button type="button">,,,,,,,,,,,,,,,,</button>
  </div>

  <div class="charts-container">
    <canvas id="myChart" width="400" height="300"></canvas>
    <canvas id="myChartPast" width="400" height="300"></canvas>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script>
    let array = [0];
    let arraypast = [0];
    fetchDati(), fetchDatiPast();
    let y = [];
    let yPast = [];
    async function fetchDati() {
      try {
        // Effettua la richiesta fetch e attendi la risposta
        const response = await fetch(
          "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"
        );
        if (!response.ok) {
          throw new Error(`Errore HTTP: ${response.status}`);
        }
        const data = await response.json();
        data.forEach((element) => {
          array.push(element);
        }); //popola l'array locale
        const Maschi = array.filter(
          (s) => s["Sesso"] === "M" && s["TipoPersona"] === "Conducente"
        );
        const Femmine = array.filter(
          (s) => s["Sesso"] === "F" && s["TipoPersona"] === "Conducente"
        );
        y = [Maschi.length, Femmine.length];
        PlotIstogramma();
        /*
                console.log("array completo: ",array);
                const anno=array.filter(a => a["Anno"]===2019);
                console.log("filtro con anno 2019: ",anno);
                const giorno=array.filter(g => g["Giorno"]==="Lunedi");
                console.log("filtro con giorno lunedi: ",giorno);
                const totale1=array.reduce((accumulatore, smc)=> accumulatore+smc["Totale (Smc)"],1);
                console.log("reduce smc: ",totale1);
                const smc=array.filter(smc => smc["Totale (Smc)"]>6641610);
                console.log("filtro con smc>6641610: ",smc);
                */
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }

    async function fetchDatiPast() {
      try {
        // Effettua la richiesta fetch e attendi la risposta
        const response = await fetch(
          "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
        );
        if (!response.ok) {
          throw new Error(`Errore HTTP: ${response.status}`);
        }
        const data = await response.json();
        data.forEach((element) => {
          arraypast.push(element);
        }); //popola l'array locale
        const MaschiPast = arraypast.filter(
          (s) => s["Sesso"] === "M" && s["TipoPersona"] === "Conducente"
        );
        const FemminePast = arraypast.filter(
          (s) => s["Sesso"] === "F" && s["TipoPersona"] === "Conducente"
        );
        yPast = [MaschiPast.length, FemminePast.length];
        PlotIstogrammaPast();
        /*
                console.log("array completo: ",array);
                const anno=array.filter(a => a["Anno"]===2019);
                console.log("filtro con anno 2019: ",anno);
                const giorno=array.filter(g => g["Giorno"]==="Lunedi");
                console.log("filtro con giorno lunedi: ",giorno);
                const totale1=array.reduce((accumulatore, smc)=> accumulatore+smc["Totale (Smc)"],1);
                console.log("reduce smc: ",totale1);
                const smc=array.filter(smc => smc["Totale (Smc)"]>6641610);
                console.log("filtro con smc>6641610: ",smc);
            */
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }

    function PlotIstogramma() {
      new Chart("myChart", {
        type: "pie",
        data: {
          labels: ["Maschi", "Femmine"],
          datasets: [
            {
              label: "Numero incidenti",
              backgroundColor: ["rgb(54, 162, 235)", "rgb(255, 99, 132)"],
              data: y,
            },
          ],
        },
        options: {
          plugins: {
            title: {
              display: true,
              text: "Distribution of Incidents by Gender(2022)",
            },
          },
          responsive: false,
        },
      });
    }
    function PlotIstogrammaPast() {
      new Chart("myChartPast", {
        type: "pie",
        data: {
          labels: ["Maschi", "Femmine"],
          datasets: [
            {
              label: "Numero incidenti",
              backgroundColor: ["rgb(54, 162, 235)", "rgb(255, 99, 132)"],
              data: yPast,
            },
          ],
        },
        options: {
          plugins: {
            title: {
              display: true,
              text: "Distribution of Incidents by Gender(2008)",
            },
          },
          responsive: false,
        },
      });
    }
  </script>
</body>

<style>
  main {
    text-align: center;
    display: flex;
    min-height: 10vh;
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
    margin-left: 20px; /* Aggiunto margine sinistro */
    margin-right: 20px; /* Aggiunto margine destro */
  }
  :global(body) {
    overflow-y: scroll;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    background-color: #f4f4f4;
  }

  header {
    text-align: center;
    padding: 40px 0;
    background-color: #4285f4;
    color: #fff;
    margin-bottom: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  h1 {
    font-size: 2em;
    margin: 0;
  }

  .buttons-container {
    display: flex;
    justify-content: center;
    margin: 20px 0;
  }

  button {
    margin: 5px;
    padding: 10px;
    font-size: 14px;
    cursor: pointer;
  }

  .charts-container {
    display: flex;
    justify-content: space-around;
    margin: 20px;
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  canvas {
    border: 1px solid #ccc;
    margin-bottom: 20px;
    max-width: 100%; /* Adapts canvas size */
    border-radius: 5px;
  }
</style>
