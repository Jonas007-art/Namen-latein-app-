# Namen-latein-app-<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Latein-Vokabeltrainer</title>
  <link rel="manifest" href="manifest.json">
  <style>
    body {
      font-family: sans-serif;
      background-color: #007BFF;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      color: white;
      text-align: center;
    }
    #points {
      position: absolute;
      top: 10px;
      left: 10px;
      background: white;
      color: black;
      padding: 6px 12px;
      border-radius: 10px;
      font-weight: bold;
    }
    #word {
      font-size: 2.5em;
      margin-bottom: 20px;
    }
    #input {
      font-size: 1.5em;
      padding: 10px;
      width: 80%;
      border: none;
      border-radius: 10px;
      text-align: center;
    }
    #checkBtn {
      margin-top: 15px;
      padding: 12px 20px;
      font-size: 1.2em;
      background-color: gold;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    #checkBtn:hover {
      background-color: orange;
    }
  </style>
</head>
<body>
  <div id="points">Punkte: 0</div>
  <div id="word">Lade Vokabeln...</div>
  <input type="text" id="input" placeholder="deutsche Bedeutung eingeben" />
  <button id="checkBtn">Prüfen</button>

  <script>
    const vokabeln = [
      { latein: "vidēre", deutsch: "sehen" },
      { latein: "currere", deutsch: "laufen" },
      { latein: "dīcere", deutsch: "sagen" },
      { latein: "venīre", deutsch: "kommen" },
      { latein: "capere", deutsch: "nehmen" },
      { latein: "facere", deutsch: "machen" },
      { latein: "dūcere", deutsch: "führen" },
      { latein: "accēdere", deutsch: "herankommen" },
      { latein: "legiō", deutsch: "Legion" },
      { latein: "vincere", deutsch: "besiegen" }
    ];

    let index = 0;
    let punkte = parseInt(localStorage.getItem("punkte") || "0");

    const wordEl = document.getElementById("word");
    const inputEl = document.getElementById("input");
    const pointsEl = document.getElementById("points");
    const button = document.getElementById("checkBtn");

    function zeigeNeueVokabel() {
      const vokabel = vokabeln[index];
      wordEl.textContent = vokabel.latein;
      inputEl.value = "";
    }

    function prüfen() {
      const vokabel = vokabeln[index];
      const antwort = inputEl.value.trim().toLowerCase();
      if (antwort === vokabel.deutsch.toLowerCase()) {
        punkte++;
        localStorage.setItem("punkte", punkte);
        pointsEl.textContent = `Punkte: ${punkte}`;
        index = (index + 1) % vokabeln.length;
        zeigeNeueVokabel();
      } else {
        alert("❌ Falsch! Versuch es nochmal.");
      }
    }

    button.addEventListener("click", prüfen);
    inputEl.addEventListener("keypress", e => {
      if (e.key === "Enter") prüfen();
    });

    pointsEl.textContent = `Punkte: ${punkte}`;
    zeigeNeueVokabel();
  </script>
</body>
</html>
