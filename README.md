# random-colour-pairs
Choose a colour for the picnic 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Random Colour Pair Generator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      padding: 20px;
      max-width: 600px;
      margin: auto;
    }

    h1 {
      text-align: center;
    }

    input, button {
      width: 100%;
      padding: 12px;
      margin-top: 10px;
      font-size: 16px;
    }

    button {
      background: #333;
      color: white;
      border: none;
      cursor: pointer;
    }

    button:hover {
      background: #555;
    }

    .name-list {
      margin-top: 15px;
      font-size: 14px;
    }

    .pair {
      margin-top: 20px;
      padding: 20px;
      border-radius: 12px;
      background: white;
      border: 2px solid #ddd;
      text-align: center;
      font-weight: bold;
    }

    .color-box {
      height: 80px;
      border-radius: 10px;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>

  <h1>🎨 Random Colour Pair Generator</h1>

  <input id="nameInput" placeholder="Enter your name">
  <button onclick="addName()">Join</button>

  <div class="name-list" id="nameList"></div>

  <button onclick="generatePairs()">Generate Pairs</button>

  <div id="results"></div>

<script>
  let names = [];

  function addName() {
    const input = document.getElementById("nameInput");
    const name = input.value.trim();

    if (!name) return;
    if (names.includes(name)) {
      alert("Name already added!");
      return;
    }

    names.push(name);
    input.value = "";
    updateList();
  }

  function updateList() {
    document.getElementById("nameList").innerText =
      "Joined (" + names.length + "): " + names.join(", ");
  }

  function generatePairs() {
    if (names.length < 2) {
      alert("At least 2 people are needed.");
      return;
    }

    shuffle(names);
    const results = document.getElementById("results");
    results.innerHTML = "";

    for (let i = 0; i < names.length; i += 2) {
      const pair = names.slice(i, i + 2);
      const color = randomColor();

      const div = document.createElement("div");
      div.className = "pair";

      div.innerHTML = `
        <div class="color-box" style="background:${color};"></div>
        <div>${pair.join(" & ")}</div>
        <div>${color}</div>
      `;

      results.appendChild(div);
    }
  }

  function shuffle(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }

  function randomColor() {
    while (true) {
      const r = Math.floor(Math.random() * 256);
      const g = Math.floor(Math.random() * 256);
      const b = Math.floor(Math.random() * 256);

      // Exclude red-dominant colors
      const isRed = r > 200 && g < 80 && b < 80;

      // Exclude white or near-white colors
      const isWhite = r > 230 && g > 230 && b > 230;

      if (!isRed && !isWhite) {
        return `rgb(${r}, ${g}, ${b})`;
      }
    }
  }
</script>

</body>
</html>
