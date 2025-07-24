---
title: Dashboard
layout: default
permalink: /dashboard/
---

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Dashboard</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f4f7fa;
    margin: 0;
    padding: 0;
  }

  .dashboard-tabs {
    display: flex;
    justify-content: center;
    background: #1565c0;
    padding: 10px;
    flex-wrap: wrap;
  }

  .dashboard-tabs a {
    color: white;
    padding: 10px 20px;
    text-decoration: none;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
  }

  .dashboard-tabs a.active,
  .dashboard-tabs a:hover {
    background: #64b5f6;
  }

  .dashboard-content {
    max-width: 1000px;
    margin: 30px auto;
    padding: 20px;
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);  
  }

  .tab-content {
    display: none;
  }

  .tab-content.active {
    display: block;
  }

  textarea {
    width: 100%;
    height: 200px;
    margin-top: 10px;
    font-size: 1em;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 6px;
    resize: vertical;
  }

  button.export-btn, button.table-btn {
    margin: 10px 5px 20px 0;
    padding: 8px 18px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 0.95em;
    cursor: pointer;
  }

  table {
    border-collapse: collapse;
    width: 100%;
    background: white;
    margin-bottom: 20px;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 8px;
    text-align: left;
  }

  th[contenteditable], td[contenteditable] {
    background-color: #fafafa;
  }

  .canvas-controls {
    text-align: center;
    margin-top: 10px;
  }

  canvas {
    border: 2px solid #444;
    border-radius: 4px;
    background: #ffffff;
    cursor: crosshair;
    display: block;
    margin: 20px auto;
  }

  /* World Clock & Weather styles */
  .grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 16px;
    margin-top: 20px;
  }

  .card {
    background: white;
    border-radius: 10px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    padding: 16px;
    width: calc(33.333% - 22px);
    box-sizing: border-box;
    text-align: left;
    transition: transform 0.2s ease;
  }

  .card:hover {
    transform: translateY(-2px);
  }

  .card h2 {
    margin-top: 0;
    font-size: 1em;
    margin-bottom: 10px;
  }

  .card p {
    margin: 6px 0;
    font-size: 0.9em;
  }

  .card .loading {
    font-style: italic;
    color: #888;
  }

  @media (max-width: 900px) {
    .card {
      width: calc(50% - 20px);
    }
  }

  @media (max-width: 600px) {
    .card {
      width: 100%;
    }
  }

  /* Combined Dark Mode Overrides */
  [data-theme="dark"] .dashboard-content,
  [data-theme="dark"] .dashboard-tabs a,
  [data-theme="dark"] .card,
  [data-theme="dark"] .card h2,
  [data-theme="dark"] .card p,
  [data-theme="dark"] h2,
  [data-theme="dark"] p,
  [data-theme="dark"] textarea,
  [data-theme="dark"] table,
  [data-theme="dark"] th,
  [data-theme="dark"] td {
    background-color: #111 !important;
    color: #00ff00 !important;
  }

  [data-theme="dark"] .card .loading {
    color: #00aa00;
  }

  [data-theme="dark"] button.export-btn,
  [data-theme="dark"] button.table-btn {
    background-color: #006400;
    color: #00ff00;
  }

  [data-theme="dark"] canvas {
    background: #222;
  }
  /* Fixes: White Canvas + Dark Navbar */
[data-theme="dark"] canvas {
  background: #fff !important;
}

[data-theme="dark"] .dashboard-tabs {
  background: #000 !important;
}
</style>
</head>
<body>

<div id="dashboard-app">

  <!-- Navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="world">World</a>
    <a href="#" data-tab="notes">Notes</a>
    <a href="#" data-tab="sheet">Spreadsheet</a>
    <a href="#" data-tab="canvas">Canvas</a>
  </nav>

  <div class="dashboard-content">

    <!-- World Clock Tab -->
    <section id="world" class="tab-content active">
      <h2>🌍 World Clock & Weather</h2>
      <div class="grid" id="dashboard-grid"></div>
    </section>

    <!-- Notes Tab -->
    <section id="notes" class="tab-content">
      <h2>Quick Notes</h2>
      <textarea id="notesArea" placeholder="Write your notes here..."></textarea>
      <button class="export-btn" onclick="exportText('notesArea', 'notes.txt')">Export Notes</button>
    </section>

    <!-- Spreadsheet Tab -->
    <section id="sheet" class="tab-content">
      <h2>Spreadsheet</h2>
      <button class="table-btn" onclick="addRow()">Add Row</button>
      <button class="table-btn" onclick="addColumn()">Add Column</button>
      <button class="export-btn" onclick="exportCSV()">Export CSV</button>

      <table id="spreadsheet">
        <thead>
          <tr id="header-row">
            <th contenteditable="true">Item</th>
            <th contenteditable="true">Quantity</th>
            <th contenteditable="true">Notes</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td contenteditable="true">Apples</td>
            <td contenteditable="true">10</td>
            <td contenteditable="true">Fresh</td>
          </tr>
          <tr>
            <td contenteditable="true">Bananas</td>
            <td contenteditable="true">5</td>
            <td contenteditable="true">Ripe</td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- Canvas Tab -->
    <section id="canvas" class="tab-content">
      <h2>Canvas Drawing Tool</h2>
      <div class="canvas-controls">
        <label>Color: <input type="color" id="colorPicker" value="#000000"></label>
        <label>Size: <input type="range" id="brushSize" min="1" max="50" value="5"></label>
      </div>
      <canvas id="drawCanvas" width="800" height="400"></canvas>
      <div class="canvas-controls">
        <button onclick="clearCanvas()">Clear</button>
        <button onclick="saveImage()">Export PNG</button>
      </div>
    </section>

  </div>
</div>

<script>
  // Tab switching logic
  document.querySelectorAll('.dashboard-tabs a').forEach(tabLink => {
    tabLink.addEventListener('click', function(e) {
      e.preventDefault();
      document.querySelectorAll('.dashboard-tabs a').forEach(a => a.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      this.classList.add('active');
      document.getElementById(this.dataset.tab).classList.add('active');
    });
  });

  // Export functions for notes
  function exportText(id, filename) {
    const content = document.getElementById(id).value;
    const blob = new Blob([content], { type: 'text/plain' });
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = filename;
    link.click();
  }

  // Spreadsheet CSV export
  function exportCSV() {
    const table = document.getElementById("spreadsheet");
    let csv = [];
    for (let row of table.rows) {
      let data = [];
      for (let cell of row.cells) {
        let txt = cell.innerText.replace(/"/g, '""');
        data.push(`"${txt}"`);
      }
      csv.push(data.join(","));
    }
    const blob = new Blob([csv.join("\n")], { type: 'text/csv' });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "spreadsheet.csv";
    link.click();
  }

  function addRow() {
    const table = document.getElementById("spreadsheet");
    const maxRows = 20;
    if (table.rows.length - 1 >= maxRows) return alert("Max 20 rows allowed.");
    const row = table.insertRow(-1);
    const cols = table.rows[0].cells.length;
    for (let i = 0; i < cols; i++) {
      const cell = row.insertCell();
      cell.contentEditable = "true";
      cell.innerText = "";
    }
  }

  function addColumn() {
    const table = document.getElementById("spreadsheet");
    const maxCols = 10;
    if (table.rows[0].cells.length >= maxCols) return alert("Max 10 columns allowed.");
    table.rows[0].insertCell(-1).outerHTML = `<th contenteditable="true">Column ${table.rows[0].cells.length + 1}</th>`;
    for (let i = 1; i < table.rows.length; i++) {
      const cell = table.rows[i].insertCell(-1);
      cell.contentEditable = "true";
      cell.innerText = "";
    }
  }

  // Canvas logic
  const canvas = document.getElementById('drawCanvas');
  const ctx = canvas.getContext('2d');
  let painting = false;

  function getPointerPosition(e) {
    const rect = canvas.getBoundingClientRect();
    if (e.touches && e.touches.length > 0) {
      return {
        x: e.touches[0].clientX - rect.left,
        y: e.touches[0].clientY - rect.top
      };
    } else {
      return {
        x: e.clientX - rect.left,
        y: e.clientY - rect.top
      };
    }
  }

  function startPosition(e) {
    e.preventDefault();
    painting = true;
    draw(e);
  }

  function finishedPosition(e) {
    e.preventDefault();
    painting = false;
    ctx.beginPath();
  }

  function draw(e) {
    e.preventDefault();
    if (!painting) return;

    const pos = getPointerPosition(e);
    ctx.lineWidth = document.getElementById('brushSize').value;
    ctx.lineCap = 'round';
    ctx.strokeStyle = document.getElementById('colorPicker').value;

    ctx.lineTo(pos.x, pos.y);
    ctx.stroke();
    ctx.beginPath();
    ctx.moveTo(pos.x, pos.y);
  }

  canvas.addEventListener('mousedown', startPosition);
  canvas.addEventListener('mouseup', finishedPosition);
  canvas.addEventListener('mouseout', finishedPosition);
  canvas.addEventListener('mousemove', draw);

  canvas.addEventListener('touchstart', startPosition, { passive: false });
  canvas.addEventListener('touchend', finishedPosition, { passive: false });
  canvas.addEventListener('touchcancel', finishedPosition, { passive: false });
  canvas.addEventListener('touchmove', draw, { passive: false });

  function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }

  function saveImage() {
    const link = document.createElement('a');
    link.download = 'canvas.png';
    link.href = canvas.toDataURL();
    link.click();
  }

  // World Clock & Weather logic
  const cities = [
    { name: "London", tz: "Europe/London", lat: 51.5074, lon: -0.1278, code: "GB" },
    { name: "New York", tz: "America/New_York", lat: 40.7128, lon: -74.0060, code: "US" },
    { name: "Paris", tz: "Europe/Paris", lat: 48.8566, lon: 2.3522, code: "FR" },
    { name: "Berlin", tz: "Europe/Berlin", lat: 52.52, lon: 13.4050, code: "DE" },
    { name: "Tokyo", tz: "Asia/Tokyo", lat: 35.6762, lon: 139.6503, code: "JP" },
    { name: "Riyadh", tz: "Asia/Riyadh", lat: 24.7136, lon: 46.6753, code: "SA" },
    { name: "Mumbai", tz: "Asia/Kolkata", lat: 19.0760, lon: 72.8777, code: "IN" },
    { name: "Beijing", tz: "Asia/Shanghai", lat: 39.9042, lon: 116.4074, code: "CN" },
    { name: "San Francisco", tz: "America/Los_Angeles", lat: 37.7749, lon: -122.4194, code: "US" }
  ];

  const dashboardGrid = document.getElementById('dashboard-grid');

  function createCard(city) {
    const card = document.createElement('div');
    card.className = 'card';
    card.innerHTML = `
      <h2>📍 ${city.name} (${city.code})</h2>
      <p><strong>Time:</strong> <span class="clock">--:--:--</span></p>
      <p><strong>Temp:</strong> <span class="temp">Loading...</span></p>
      <p><strong>Wind:</strong> <span class="wind">Loading...</span></p>
    `;
    dashboardGrid.appendChild(card);
    return card;
  }

  function updateClock(card, city) {
    const clockSpan = card.querySelector('.clock');
    setInterval(() => {
      const now = new Date();
      const timeStr = new Intl.DateTimeFormat('en-GB', {
        timeZone: city.tz,
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit'
      }).format(now);
      clockSpan.textContent = timeStr;
    }, 1000);
  }

  function updateWeather(card, temp, wind) {
    const tempSpan = card.querySelector('.temp');
    const windSpan = card.querySelector('.wind');
    tempSpan.textContent = `${temp}°C`;
    windSpan.textContent = `${wind} km/h`;
  }

  if (dashboardGrid) {
    cities.forEach(city => {
      const card = createCard(city);
      updateClock(card, city);
      fetch(`https://api.open-meteo.com/v1/forecast?latitude=${city.lat}&longitude=${city.lon}&current_weather=true`)
        .then(res => res.json())
        .then(weather => {
          const temp = weather.current_weather?.temperature ?? "N/A";
          const wind = weather.current_weather?.windspeed ?? "N/A";
          updateWeather(card, temp, wind);
        })
        .catch(() => updateWeather(card, "N/A", "N/A"));
    });
  }
</script>
</body>
</html>
