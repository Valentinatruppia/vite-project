<title>STATISTICS</title>
<script>
function myFunction() {
  
        window.location.href = '../index.html';
        
}
</script>
<main>
  <h1>CRASH ANALYZER</h1>
  <section class="content">
    <button onclick="myFunction()">Back to home</button>
  </section>
</main>
<body>   
  <meta charset="utf-8" />
  <header>
    <h1>STATISTICS</h1>
  </header>
  <div class="charts-container seventh-group">
    <canvas id="myChartTotIncidenti" width="800" height="300"></canvas>
  </div>

  <div class="charts-container first-group">
    <canvas id="myChartMF" width="400" height="300"></canvas>
    <canvas id="myChartMFPast" width="400" height="300"></canvas>
  </div>

  <div class="charts-container second-group">
    <canvas id="myChartAirbag" width="400" height="300"></canvas>
    <canvas id="myChartAirbagPast" width="400" height="300"></canvas>
  </div>
  <div class="charts-container third-group">
    <canvas id="myChartConducenti" width="400" height="300"></canvas>
    <canvas id="myChartConducentiPast" width="400" height="300"></canvas>
  </div>
  <div class="charts-container fourth-group">
    <canvas id="myChartProgressivo" width="400" height="300"></canvas>
    <canvas id="myChartProgressivoPast" width="400" height="300"></canvas>
  </div>
  <div class="charts-container fifth-group">
    <canvas id="myChartLesioni" width="400" height="300"></canvas>
    <canvas id="myChartLesioniPast" width="400" height="300"></canvas>
  </div>
  <div class="charts-container six-group">
    <canvas id="myChartCinturaCasco" width="400" height="300"></canvas>
    <canvas id="myChartCinturaCascoPast" width="400" height="300"></canvas>
  </div>

  
    

  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script>

    let array = [0];
    let arraypast = [0];
    fetchDatiTotIncidenti(),fetchDati(), fetchDatiPast(),fetchDatiAirbag(),fetchDatiAirbagPast();
    let y = [];
    let yPast = [];
    let yTotIncidenti = [];
    
    //////////////////////////////////////////////////////////////////////////////////
    async function fetchDatiTotIncidenti() {
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

        const response1 = await fetch(
          "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
        );
        if (!response1.ok) {
          throw new Error(`Errore HTTP: ${response1.status}`);
        }
        const data1 = await response1.json();
        data1.forEach((element1) => {
          arraypast.push(element1);
        });
        const tot =array.length;
        const totPast=arraypast.length;
        yTotIncidenti = [tot,totPast];
        PlotIstogrammaTotIncidenti();
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }
    //////////////////////////////////////////////////////////////////////////////////
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
        //filtro maschi vs femmine
        const Maschi = array.filter(
          (s) => s["Sesso"] === "M" && s["TipoPersona"] === "Conducente"
        );
        const Femmine = array.filter(
          (s) => s["Sesso"] === "F" && s["TipoPersona"] === "Conducente"
        );
        y = [Maschi.length, Femmine.length];
        PlotIstogramma();
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////////////////
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

      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }

    /////////////////////////////////////////////////////////////////////////////////////////////////////////////
    async function fetchDatiAirbag() {
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
        //Gravità incidenti(Airbag)
        const Airbag_ine = array.filter(
          (i) => i["Airbag"] == "Inesistente");
        const Airbag_esploso = array.filter(
          (e) => e["Airbag"] == "Esploso");
        const Airbag_inesploso = array.filter(
          (n) => n["Airbag"] == "Inesploso");
        y_Airbag=[Airbag_ine.length,Airbag_esploso.length,Airbag_inesploso.length];
        PlotIstogrammaAirbag();
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }
        //////////////////////////////////////////////////////////////////////////////////////////////

    async function fetchDatiAirbagPast() {
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
          array.push(element);
        }); //popola l'array locale
        //Gravità incidenti(Airbag)
        const Airbag_ine = array.filter(
          (i) => i["Airbag"] == "Inesistente");
        const Airbag_esploso = array.filter(
          (e) => e["Airbag"] == "Esploso");
        const Airbag_inesploso = array.filter(
          (n) => n["Airbag"] == "Inesploso");
        y_AirbagPast=[Airbag_ine.length,Airbag_esploso.length,Airbag_inesploso.length];
        PlotIstogrammaAirbagPast();
      } catch (error) {
        console.error(`Impossibile recuperare i dati: ${error}`);
      }
    }
        //////////////////////////////////////////////////////////////////////////////////////////////


async function fetchDatiConducenti() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    const conducenti = data.filter((persona) => persona["TipoPersona"] === "Conducente");
    const percentualeConducenti = (conducenti.length / data.length) * 100;

    plotIstogrammaConducenti(percentualeConducenti, "myChartConducenti", "Distribution of Drivers and Passenger");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico della percentuale di conducenti
function plotIstogrammaConducenti(percentualeConducenti, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: ["Altri", "Conducenti"],
      datasets: [
        {
          data: [100 - percentualeConducenti, percentualeConducenti],
          backgroundColor: ["rgb(220, 220, 220)", "rgb(54, 162, 235)"],
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati
fetchDatiConducenti();



//tabella 2008

async function fetchDatiConducentiPast() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    const conducentiPast = data.filter((persona) => persona["TipoPersona"] === "Conducente");
    const percentualeConducentiPast = (conducentiPast.length / data.length) * 100;

    plotIstogrammaConducentiPast(percentualeConducentiPast, "myChartConducentiPast", "Distribution of Drivers and Passenger");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico della percentuale di conducenti
function plotIstogrammaConducentiPast(percentualeConducenti, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: ["Altri", "Conducenti"],
      datasets: [
        {
          data: [100 - percentualeConducenti, percentualeConducenti],
          backgroundColor: ["rgb(220, 220, 220)", "rgb(54, 162, 235)"],
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati
fetchDatiConducentiPast();






//grafivo progressivo 2022


  async function fetchDatiProgressivo() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Ottieni un conteggio dei valori unici di "Progressivo"
    const progressivoCounts = {};
    data.forEach((persona) => {
      const progressivo = persona["Progressivo"];
      progressivoCounts[progressivo] = (progressivoCounts[progressivo] || 0) + 1;
    });

    // Calcola la percentuale per ogni valore di "Progressivo"
    const totalEntries = data.length;
    const percentualiProgressivo = Object.keys(progressivoCounts).map((progressivo) => ({
      progressivo,
      percentuale: (progressivoCounts[progressivo] / totalEntries) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico a torta
    PlotIstogrammaProgressivo(percentualiProgressivo, "myChartProgressivo", "Distribution of Progressivo(2022)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico a torta per "Progressivo"
function PlotIstogrammaProgressivo(data, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: data.map((item) => item.progressivo),
      datasets: [
        {
          data: data.map((item) => item.percentuale),
          backgroundColor: getRandomColors(data.length),
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Funzione per generare colori casuali
function getRandomColors(count) {
  const colors = [];
  for (let i = 0; i < count; i++) {
    colors.push(`rgb(${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)})`);
  }
  return colors;
}

// Chiamata alla funzione per ottenere e visualizzare i dati
fetchDatiProgressivo();





//grafico progressivo 2008


async function fetchDatiProgressivoPast() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Ottieni un conteggio dei valori unici di "Progressivo"
    const progressivoCounts = {};
    data.forEach((persona) => {
      const progressivo = persona["Progressivo"];
      progressivoCounts[progressivo] = (progressivoCounts[progressivo] || 0) + 1;
    });

    // Calcola la percentuale per ogni valore di "Progressivo"
    const totalEntries = data.length;
    const percentualiProgressivo = Object.keys(progressivoCounts).map((progressivo) => ({
      progressivo,
      percentuale: (progressivoCounts[progressivo] / totalEntries) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico a torta
    plotIstogrammaProgressivoPast(percentualiProgressivo, "myChartProgressivoPast", "Distribution of Progressivo(2008)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico a torta per "Progressivo"
function plotIstogrammaProgressivoPast(data, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: data.map((item) => item.progressivo),
      datasets: [
        {
          data: data.map((item) => item.percentuale),
          backgroundColor: getRandomColors(data.length),
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Funzione per generare colori casuali
function getRandomColors(count) {
  const colors = [];
  for (let i = 0; i < count; i++) {
    colors.push(`rgb(${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)})`);
  }
  return colors;
}

// Chiamata alla funzione per ottenere e visualizzare i dati
fetchDatiProgressivoPast();




//grafico tipo lesione 2022
async function fetchDatiLesioni() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Raggruppa i dati per il parametro TipoLesione
    const lesioniCount = {};
    data.forEach((persona) => {
      const tipoLesione = persona["TipoLesione"];
      lesioniCount[tipoLesione] = (lesioniCount[tipoLesione] || 0) + 1;
    });

    // Calcola la percentuale per ogni tipo di lesione
    const totalPersonas = data.length;
    const percentualiLesioni = Object.entries(lesioniCount).map(([tipoLesione, count]) => ({
      tipoLesione,
      percentuale: (count / totalPersonas) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico delle lesioni a torta
    plotTortaLesioni(percentualiLesioni, "myChartLesioni", "Distribution of Injury Types(2022)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico delle lesioni a torta
function plotTortaLesioni(percentualiLesioni, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  const labels = percentualiLesioni.map((entry) => entry.tipoLesione);
  const data = percentualiLesioni.map((entry) => entry.percentuale);

  const colori = [
    "rgb(255, 99, 132)",
    "rgb(54, 162, 235)",
    "rgb(255, 205, 86)",
    "rgb(75, 192, 192)",
    "rgb(153, 102, 255)",
    "rgb(255, 159, 64)",
    // Aggiungi altri colori se necessario
  ];

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: labels,
      datasets: [
        {
          data: data,
          backgroundColor: colori.slice(0, labels.length), // Usa solo i primi N colori, dove N è il numero di etichette
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati
fetchDatiLesioni();

//grafico tipo lesioni 2008
async function fetchDatiLesioniPast() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Raggruppa i dati per il parametro TipoLesione
    const lesioniCount = {};
    data.forEach((persona) => {
      const tipoLesione = persona["TipoLesione"];
      lesioniCount[tipoLesione] = (lesioniCount[tipoLesione] || 0) + 1;
    });

    // Calcola la percentuale per ogni tipo di lesione
    const totalPersonas = data.length;
    const percentualiLesioni = Object.entries(lesioniCount).map(([tipoLesione, count]) => ({
      tipoLesione,
      percentuale: (count / totalPersonas) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico delle lesioni a torta
    plotTortaLesioniPast(percentualiLesioni, "myChartLesioniPast", "Distribution of Injury Types (2008)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico delle lesioni a torta (Past)
function plotTortaLesioniPast(percentualiLesioni, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  const labels = percentualiLesioni.map((entry) => entry.tipoLesione);
  const data = percentualiLesioni.map((entry) => entry.percentuale);

  const colori = [
    "rgb(255, 99, 132)",
    "rgb(54, 162, 235)",
    "rgb(255, 205, 86)",
    "rgb(75, 192, 192)",
    "rgb(153, 102, 255)",
    "rgb(255, 159, 64)",
    // Aggiungi altri colori se necessario
  ];

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: labels,
      datasets: [
        {
          data: data,
          backgroundColor: colori.slice(0, labels.length), // Usa solo i primi N colori, dove N è il numero di etichette
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati (Past)
fetchDatiLesioniPast();






//grafico tipo cinturacascoutilizzato 2022

async function fetchDatiCinturaCasco() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidenti.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Raggruppa i dati per il parametro CinturaCascoUtilizzato
    const cinturaCascoCount = {};
    data.forEach((persona) => {
      const cinturaCasco = persona["CinturaCascoUtilizzato"];
      cinturaCascoCount[cinturaCasco] = (cinturaCascoCount[cinturaCasco] || 0) + 1;
    });

    // Calcola la percentuale per ogni valore di CinturaCascoUtilizzato
    const totalPersonas = data.length;
    const percentualiCinturaCasco = Object.entries(cinturaCascoCount).map(([cinturaCasco, count]) => ({
      cinturaCasco,
      percentuale: (count / totalPersonas) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico della cintura/casco
    plotTortaCinturaCasco(percentualiCinturaCasco, "myChartCinturaCasco", "Distribution of Seatbelt/Helmet Usage(2022)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico della cintura/casco
function plotTortaCinturaCasco(percentualiCinturaCasco, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  const labels = percentualiCinturaCasco.map((entry) => entry.cinturaCasco);
  const data = percentualiCinturaCasco.map((entry) => entry.percentuale);

  const colori = [
    "rgb(255, 99, 132)",
    "rgb(54, 162, 235)",
    "rgb(255, 205, 86)",
    "rgb(75, 192, 192)",
    "rgb(153, 102, 255)",
    "rgb(255, 159, 64)",
    // Aggiungi altri colori se necessario
  ];

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: labels,
      datasets: [
        {
          data: data,
          backgroundColor: colori.slice(0, labels.length), // Usa solo i primi N colori, dove N è il numero di etichette
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati della cintura/casco
fetchDatiCinturaCasco();





//grafico tipo cinturacascoutilizzato 2022
async function fetchDatiCinturaCascoPast() {
  try {
    const response = await fetch(
      "https://raw.githubusercontent.com/Valentinatruppia/vite-project/main/incidentipast.json"
    );
    if (!response.ok) {
      throw new Error(`Errore HTTP: ${response.status}`);
    }
    const data = await response.json();

    // Raggruppa i dati per il parametro CinturaCascoUtilizzato
    const cinturaCascoCount = {};
    data.forEach((persona) => {
      const cinturaCasco = persona["CinturaCascoUtilizzato"];
      cinturaCascoCount[cinturaCasco] = (cinturaCascoCount[cinturaCasco] || 0) + 1;
    });

    // Calcola la percentuale per ogni valore di CinturaCascoUtilizzato
    const totalPersonas = data.length;
    const percentualiCinturaCasco = Object.entries(cinturaCascoCount).map(([cinturaCasco, count]) => ({
      cinturaCasco,
      percentuale: (count / totalPersonas) * 100,
    }));

    // Chiamata alla funzione per visualizzare il grafico della cintura/casco (Past)
    plotTortaCinturaCascoPast(percentualiCinturaCasco, "myChartCinturaCascoPast", "Distribution of Seatbelt/Helmet Usage (2008)");
  } catch (error) {
    console.error(`Impossibile recuperare i dati: ${error}`);
  }
}

// Aggiungi questa funzione per visualizzare il grafico della cintura/casco (Past)
function plotTortaCinturaCascoPast(percentualiCinturaCasco, chartId, titleText) {
  const canvasElement = document.getElementById(chartId);

  if (!canvasElement) {
    console.error(`Elemento canvas non trovato con id ${chartId}`);
    return;
  }

  const labels = percentualiCinturaCasco.map((entry) => entry.cinturaCasco);
  const data = percentualiCinturaCasco.map((entry) => entry.percentuale);

  const colori = [
    "rgb(255, 99, 132)",
    "rgb(54, 162, 235)",
    "rgb(255, 205, 86)",
    "rgb(75, 192, 192)",
    "rgb(153, 102, 255)",
    "rgb(255, 159, 64)",
    // Aggiungi altri colori se necessario
  ];

  new Chart(canvasElement, {
    type: "pie",
    data: {
      labels: labels,
      datasets: [
        {
          data: data,
          backgroundColor: colori.slice(0, labels.length), // Usa solo i primi N colori, dove N è il numero di etichette
        },
      ],
    },
    options: {
      plugins: {
        title: {
          display: true,
          text: titleText,
        },
      },
      responsive: false,
    },
  });
}

// Chiamata alla funzione per ottenere e visualizzare i dati della cintura/casco (Past)
fetchDatiCinturaCascoPast();
function PlotIstogrammaTotIncidenti() {
      new Chart("myChartTotIncidenti", {
        type: "bar",
        data: {
          labels: ["Incidenti(2022)", "Incidenti(2008)"],
          datasets: [
            {
              label: "Totale incidenti",
              backgroundColor: ["rgb(54, 162, 235)", "rgb(255, 99, 132)"],
              data: yTotIncidenti,
            },
          ],
        },
        options: {
          plugins: {
            title: {
              display: true,
              text: "Total of Incsidents(2022-2008)",
            },
          },
          responsive: false,
        },
      });
    }
    
function PlotIstogramma() {
      new Chart("myChartMF", {
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
      new Chart("myChartMFPast", {
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

    function PlotIstogrammaAirbag() {
      new Chart("myChartAirbag", {
        type: "pie",
        data: {
          labels: ["Inesistente", "Esploso", "Inesploso"],
          datasets: [
            {
              label: "Gravita' incidenti(Airbag)",
              backgroundColor: ["rgb(54, 162, 235)", "rgb(255, 99, 132)", "rgb(120, 99, 140)"],
              data: y_Airbag,
            },
          ],
        },
        options: {
          plugins: {
            title: {
              display: true,
              text: "Distribution of Incidents by Gravity(Airbag 2022)",
            },
          },
          responsive: false,
        },
      });
    }
    
    function PlotIstogrammaAirbagPast() {
      new Chart("myChartAirbagPast", {
        type: "pie",
        data: {
          labels: ["Inesistente", "Esploso", "Inesploso"],
          datasets: [
            {
              label: "Gravita' incidenti(Airbag)",
              backgroundColor: ["rgb(54, 162, 235)", "rgb(255, 99, 132)", "rgb(120, 99, 140)"],
              data: y_AirbagPast,
            },
          ],
        },
        options: {
          plugins: {
            title: {
              display: true,
              text: "Distribution of Incidents by Gravity(Airbag 2008)",
            },
          },
          responsive: false,
        },
      });
    }
//grafico con i conducenti

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
    max-width: 9000px; 
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(66, 56, 56, 1);
    border-radius: 20px;
    margin-top: 20px;
    margin-bottom: 20px;
    margin-left: 20px;
    margin-right: 20px;
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

  button:focus {
    margin: 5px;
    padding: 10px;
    font-size: 14px;
    cursor: pointer;
    top: 50%;
    outline-color: transparent;
    outline-style: solid;
    box-shadow: 0 0 0 4px #5a01a7;
    transition: 0.7s;
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
  .first-group {
      background-color: #d9d9d9; /* Cambia il colore di sfondo */
      padding: 15px; /* Modifica il padding se necessario */
    }

    /* Aggiungi stili specifici per il secondo gruppo di grafici */
    .second-group {
      background-color: #d9d9d9; /* Cambia il colore di sfondo */
      padding: 15px; /* Modifica il padding se necessario */
    }

    .third-group {
    background-color: #d9d9d9; /* Cambia il colore di sfondo */
    padding: 15px; /* Modifica il padding se necessario */
 }
 .fourth-group {
    background-color: #d9d9d9; /* Cambia il colore di sfondo */
    padding: 15px; /* Modifica il padding se necessario */
 }
 .fifth-group {
    background-color: #d9d9d9; /* Cambia il colore di sfondo */
    padding: 15px; /* Modifica il padding se necessario */
 }
 .six-group {
    background-color: #d9d9d9; /* Cambia il colore di sfondo */
    padding: 15px; /* Modifica il padding se necessario */
 }
 
 .seventh-group {
    background-color: #d9d9d9; /* Cambia il colore di sfondo */
    padding: 15px; /* Modifica il padding se necessario */
 }
  canvas {
    border: 1px solid #ccc;
    margin-bottom: 20px;
    max-width: 100%; /* Adapts canvas size */
    border-radius: 5px;
  }

</style>
