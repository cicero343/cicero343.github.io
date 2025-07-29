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
    font-size: 1em;
  }

  /* Mobile-friendly tab layout - Fixed for 3 per line */
  @media (max-width: 768px) {
    .dashboard-tabs {
      padding: 8px 2px;
      gap: 2px;
    }
    
    .dashboard-tabs a {
      flex: 0 0 calc(33.333% - 4px);
      width: calc(33.333% - 4px);
      padding: 8px 4px;
      margin: 1px;
      font-size: 0.8em;
      text-align: center;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      box-sizing: border-box;
    }
  }

  /* Extra small screens */
  @media (max-width: 480px) {
    .dashboard-tabs a {
      font-size: 0.75em;
      padding: 7px 2px;
    }
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

  /* Exchange Rates specific styles */
  table caption {
    margin-top: 0.5rem;
    font-size: 0.9rem;
    color: #666;
  }
  
  img.flag {
    width: 24px;
    height: 18px;
    border: 1px solid #ccc;
    border-radius: 3px;
    vertical-align: middle;
    margin-right: 0.5rem;
  }

  /* Foodbanks Finder styles */
  form {
    margin-bottom: 1rem;
  }
  
  label, select, input {
    font-size: 1.1em;
  }
  
  input[type="text"] {
    width: 180px;
    padding: 6px;
    margin-right: 10px;
  }
  
  select {
    padding: 6px;
    margin-right: 10px;
  }
  
  button {
    padding: 7px 15px;
    font-size: 1.1em;
    cursor: pointer;
  }
  
  #error {
    color: red;
    margin-bottom: 15px;
    display: none;
  }
  
  .foodbank {
    border: 1px solid #ddd;
    padding: 12px;
    margin-bottom: 15px;
    border-radius: 6px;
    background: #f9f9f9;
  }
  
  .foodbank h3 {
    margin-top: 0;
    margin-bottom: 6px;
  }

  /* Food Recipes styles */
  .recipe-search-bar {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 20px;
    flex-wrap: wrap;
  }

  .recipe-search-bar input[type="text"] {
    flex: 1;
    min-width: 200px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1em;
  }

  .recipe-search-bar button {
    padding: 10px 20px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1em;
  }

  .recipe-search-bar button:hover {
    background: #0056b3;
  }

  .recipe-controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    flex-wrap: wrap;
    gap: 10px;
  }

  .results-per-page {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .results-per-page select {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 3px;
  }

  .recipe-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
  }

  .recipe-card {
    background: white;
    border-radius: 10px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: transform 0.2s ease;
    cursor: pointer;
  }

  .recipe-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
  }

  .recipe-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  .recipe-card-content {
    padding: 15px;
  }

  .recipe-card h3 {
    margin: 0 0 10px 0;
    font-size: 1.1em;
    color: #333;
  }

  .recipe-card p {
    margin: 5px 0;
    color: #666;
    font-size: 0.9em;
  }

  .recipe-card .category {
    background: #e3f2fd;
    color: #1976d2;
    padding: 3px 8px;
    border-radius: 12px;
    font-size: 0.8em;
    display: inline-block;
    margin-top: 8px;
  }

  .pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    margin-top: 20px;
  }

  .pagination button {
    padding: 8px 12px;
    border: 1px solid #ddd;
    background: white;
    color: #333;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9em;
  }

  .pagination button:hover:not(:disabled) {
    background: #f0f0f0;
  }

  .pagination button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  .pagination button.active {
    background: #007bff;
    color: white;
    border-color: #007bff;
  }

  .pagination-info {
    font-size: 0.9em;
    color: #666;
  }

  .recipe-loading {
    text-align: center;
    padding: 40px;
    color: #666;
    font-style: italic;
  }

  .recipe-error {
    text-align: center;
    padding: 40px;
    color: #d32f2f;
    background: #ffebee;
    border-radius: 8px;
    margin: 20px 0;
  }

  .no-results {
    text-align: center;
    padding: 40px;
    color: #666;
    background: #f5f5f5;
    border-radius: 8px;
    margin: 20px 0;
  }

  /* Recipe Detail Modal */
  .recipe-modal {
    display: none;
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    overflow-y: auto;
  }

  .recipe-modal-content {
    background-color: white;
    margin: 2% auto;
    padding: 0;
    border-radius: 10px;
    width: 90%;
    max-width: 800px;
    position: relative;
    max-height: 90vh;
    overflow-y: auto;
  }

  .recipe-modal-header {
    position: relative;
    padding: 0;
  }

  .recipe-modal-header img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    border-radius: 10px 10px 0 0;
  }

  .close-modal {
    position: absolute;
    top: 15px;
    right: 20px;
    color: white;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 50%;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
  }

  .close-modal:hover {
    background: rgba(0, 0, 0, 0.7);
  }

  .recipe-modal-body {
    padding: 30px;
  }

  .recipe-modal-body h2 {
    margin-top: 0;
    margin-bottom: 15px;
    color: #333;
    font-size: 1.8em;
  }

  .recipe-meta {
    display: flex;
    gap: 20px;
    margin-bottom: 25px;
    flex-wrap: wrap;
  }

  .recipe-meta-item {
    background: #f8f9fa;
    padding: 8px 15px;
    border-radius: 20px;
    font-size: 0.9em;
    color: #666;
  }

  .recipe-tags {
    margin-bottom: 25px;
  }

  .recipe-tag {
    background: #e3f2fd;
    color: #1976d2;
    padding: 5px 12px;
    border-radius: 15px;
    font-size: 0.85em;
    display: inline-block;
    margin-right: 8px;
    margin-bottom: 5px;
  }

  .recipe-section {
    margin-bottom: 30px;
  }

  .recipe-section h3 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.3em;
    border-bottom: 2px solid #007bff;
    padding-bottom: 5px;
  }

  .ingredients-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 10px;
    margin-bottom: 20px;
  }

  .ingredient-item {
    background: #f8f9fa;
    padding: 10px 15px;
    border-radius: 8px;
    border-left: 4px solid #007bff;
  }

  .ingredient-name {
    font-weight: bold;
    color: #333;
  }

  .ingredient-measure {
    color: #666;
    font-size: 0.9em;
  }

  .instructions {
    line-height: 1.7;
    color: #444;
    font-size: 1.05em;
  }

  .youtube-link {
    display: inline-block;
    background: #ff0000;
    color: white;
    padding: 10px 20px;
    border-radius: 25px;
    text-decoration: none;
    font-weight: bold;
    margin-top: 15px;
  }

  .youtube-link:hover {
    background: #cc0000;
    color: white;
  }

  @media (max-width: 600px) {
    .recipe-modal-content {
      width: 95%;
      margin: 5% auto;
    }
    
    .recipe-modal-body {
      padding: 20px;
    }
    
    .ingredients-list {
      grid-template-columns: 1fr;
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
  [data-theme="dark"] td,
  [data-theme="dark"] .foodbank,
  [data-theme="dark"] .recipe-card,
  [data-theme="dark"] .recipe-card-content {
    background-color: #111 !important;
    color: #00ff00 !important;
  }

  [data-theme="dark"] .card .loading {
    color: #00aa00;
  }

  [data-theme="dark"] button.export-btn,
  [data-theme="dark"] button.table-btn,
  [data-theme="dark"] button {
    background-color: #006400;
    color: #00ff00;
  }

  [data-theme="dark"] canvas {
    background: #fff !important;
  }

  [data-theme="dark"] .dashboard-tabs {
    background: #000 !important;
  }

  [data-theme="dark"] .recipe-modal-content,
  [data-theme="dark"] .recipe-modal-body {
    background-color: #111 !important;
    color: #00ff00 !important;
  }
</style>
</head>
<body>

<div id="dashboard-app">

  <!-- Navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="world">World</a>
    <a href="#" data-tab="foodbanks">UK Foodbanks</a>
    <a href="#" data-tab="exchange">Exchange Rates</a>
    <a href="#" data-tab="recipes">Food Recipes</a>
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

    <!-- UK Foodbanks Tab -->
    <section id="foodbanks" class="tab-content">
      <h2>Find Nearby UK Foodbanks</h2>

      <form id="searchForm">
        <label for="postcode">Enter UK postcode:</label>
        <input type="text" id="postcode" name="postcode" placeholder="e.g. OX49 5NU" required />

        <label for="radius">Radius (miles):</label>
        <select id="radius" name="radius">
          <option value="5">5</option>
          <option value="10" selected>10</option>
          <option value="15">15</option>
          <option value="20">20</option>
        </select>

        <button type="submit">Search</button>
      </form>

      <div id="error"></div>
      <div id="results"></div>
    </section>

    <!-- Exchange Rates Tab -->
    <section id="exchange" class="tab-content">
      <h2>Exchange Rates (Base: GBP)</h2>
      <table>
        <thead>
          <tr>
            <th>Flag</th>
            <th>Currency Code</th>
            <th>Rate (vs GBP)</th>
          </tr>
        </thead>
        <tbody id="exchange-body">
          <!-- Injected by JS -->
        </tbody>
        <caption>Rates pulled from Fawaz Exchange API</caption>
      </table>
    </section>

    <!-- Food Recipes Tab -->
    <section id="recipes" class="tab-content">
      <h2>🍽️ Food Recipes</h2>
      
      <div class="recipe-search-bar">
        <input type="text" id="recipeSearch" placeholder="Search for recipes (e.g., chicken, pasta, dessert)..." />
        <button onclick="searchRecipes()">Search</button>
        <button onclick="getRandomRecipe()">Random Recipe</button>
      </div>

      <div class="recipe-controls">
        <div class="results-per-page">
          <label for="resultsPerPage">Results per page:</label>
          <select id="resultsPerPage" onchange="changeResultsPerPage()">
            <option value="12">12</option>
            <option value="24" selected>24</option>
            <option value="48">48</option>
          </select>
        </div>
        <div class="pagination-info" id="paginationInfo"></div>
      </div>

      <div id="recipeResults">
        <div class="recipe-grid" id="recipeGrid"></div>
        <div class="pagination" id="recipePagination"></div>
      </div>

      <!-- Recipe Detail Modal -->
      <div id="recipeModal" class="recipe-modal">
        <div class="recipe-modal-content">
          <div class="recipe-modal-header">
            <img id="modalRecipeImage" src="" alt="Recipe Image">
            <span class="close-modal" onclick="closeRecipeModal()">&times;</span>
          </div>
          <div class="recipe-modal-body">
            <h2 id="modalRecipeTitle"></h2>
            <div class="recipe-meta" id="modalRecipeMeta"></div>
            <div class="recipe-tags" id="modalRecipeTags"></div>
            <div class="recipe-section">
              <h3>🥘 Ingredients</h3>
              <div class="ingredients-list" id="modalIngredients"></div>
            </div>
            <div class="recipe-section">
              <h3>👩‍🍳 Instructions</h3>
              <div class="instructions" id="modalInstructions"></div>
              <div id="modalYoutubeLink"></div>
            </div>
          </div>
        </div>
      </div>
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

  // --- Exchange Rates Script ---
  const preferredCurrencies = ["usd", "eur", "jpy", "aud", "cad", "inr", "cny", "chf", "zar", "btc", "eth"];

  const currencyToCountry = {
    usd: "us",
    eur: "eu",
    jpy: "jp",
    aud: "au",
    cad: "ca",
    inr: "in",
    cny: "cn",
    chf: "ch",
    zar: "za"
  };

  async function fetchRates() {
    const fallbackURL = "https://latest.currency-api.pages.dev/v1/currencies/gbp.json";
    const mainURL = "https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/gbp.json";

    try {
      const res = await fetch(mainURL);
      if (!res.ok) throw new Error("Primary failed");
      const data = await res.json();
      updateTable(data.gbp);
    } catch (err) {
      console.warn("Falling back to Cloudflare:", err.message);
      try {
        const fallbackRes = await fetch(fallbackURL);
        if (!fallbackRes.ok) throw new Error("Fallback failed");
        const fallbackData = await fallbackRes.json();
        updateTable(fallbackData.gbp);
      } catch (fallbackErr) {
        document.getElementById("exchange-body").innerHTML = `
          <tr><td colspan="3">Failed to load exchange rates.</td></tr>`;
      }
    }
  }

  function updateTable(rates) {
    const tbody = document.getElementById("exchange-body");
    tbody.innerHTML = "";

    preferredCurrencies.forEach(code => {
      if (rates[code]) {
        let flagCellContent = '';
        if (code === 'btc' || code === 'eth') {
          flagCellContent = '💰';
        } else {
          const countryCode = currencyToCountry[code] || "un";
          const flagUrl = `https://flagcdn.com/w20/${countryCode}.png`;
          flagCellContent = `<img class="flag" src="${flagUrl}" alt="${code.toUpperCase()} flag">`;
        }

        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td>${flagCellContent}</td>
          <td>${code.toUpperCase()}</td>
          <td>${rates[code].toFixed(4)}</td>
        `;
        tbody.appendChild(tr);
      }
    });
  }

  fetchRates();

  // --- Foodbanks Finder Script ---
  // Haversine formula to calculate distance between 2 lat/lng points in miles
  function distanceMiles(lat1, lon1, lat2, lon2) {
    const toRad = x => (x * Math.PI) / 180;
    const R = 3958.8; // Radius of the Earth in miles
    const dLat = toRad(lat2 - lat1);
    const dLon = toRad(lon2 - lon1);
    const a = Math.sin(dLat/2)**2 + Math.cos(toRad(lat1)) * Math.cos(toRad(lat2)) * Math.sin(dLon/2)**2;
    const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
    return R * c;
  }

  const form = document.getElementById('searchForm');
  const resultsDiv = document.getElementById('results');
  const errorDiv = document.getElementById('error');

  form.addEventListener('submit', async (e) => {
    e.preventDefault();
    resultsDiv.innerHTML = '';
    errorDiv.style.display = 'none';

    const postcode = document.getElementById('postcode').value.trim();
    const radius = Number(document.getElementById('radius').value);

    if (!postcode) return;

    try {
      // Step 1: Get lat/lng for input postcode
      const resPostcode = await fetch(`https://api.postcodes.io/postcodes/${encodeURIComponent(postcode)}`);
      const dataPostcode = await resPostcode.json();

      if (dataPostcode.status !== 200) {
        throw new Error(dataPostcode.error || "Invalid postcode");
      }

      const { latitude: userLat, longitude: userLng } = dataPostcode.result;

      // Step 2: Fetch full live foodbanks list from the API
      const resFoodbanks = await fetch('https://www.givefood.org.uk/api/2/foodbanks/');
      if (!resFoodbanks.ok) {
        throw new Error("Failed to fetch foodbanks list");
      }
      const dataFoodbanks = await resFoodbanks.json();

      // Filter foodbanks within radius
      const filtered = dataFoodbanks.filter(fb => {
        if (!fb.lat_lng) return false;
        const [fbLat, fbLng] = fb.lat_lng.split(',').map(Number);
        const dist = distanceMiles(userLat, userLng, fbLat, fbLng);
        return dist <= radius;
      });

      if (filtered.length === 0) {
        resultsDiv.innerHTML = `<p>No foodbanks found within ${radius} miles.</p>`;
        return;
      }

      // Sort by distance ascending
      const sorted = filtered.sort((a,b) => {
        const [aLat, aLng] = a.lat_lng.split(',').map(Number);
        const [bLat, bLng] = b.lat_lng.split(',').map(Number);
        return distanceMiles(userLat, userLng, aLat, aLng) - distanceMiles(userLat, userLng, bLat, bLng);
      });

      resultsDiv.innerHTML = sorted.map(fb => {
        const [fbLat, fbLng] = fb.lat_lng.split(',').map(Number);
        const dist = distanceMiles(userLat, userLng, fbLat, fbLng).toFixed(1);
        return `
          <div class="foodbank">
            <h3>${fb.name} (${dist} miles)</h3>
            <p>${fb.address ? fb.address.replace(/\n/g, '<br>') : 'No address available'}</p>
            <p>Phone: ${fb.phone || 'N/A'}</p>
            ${fb.urls?.homepage ? `<p><a href="${fb.urls.homepage}" target="_blank" rel="noopener">Website</a></p>` : ''}
          </div>
        `;
      }).join('');

    } catch (err) {
      errorDiv.textContent = `Error: ${err.message}`;
      errorDiv.style.display = 'block';
    }
  });

  // --- Food Recipes Script ---
  let currentRecipes = [];
  let currentPage = 1;
  let resultsPerPage = 24;

  // Allow search on Enter key
  document.getElementById('recipeSearch').addEventListener('keypress', function(e) {
    if (e.key === 'Enter') {
      searchRecipes();
    }
  });

  async function searchRecipes() {
    const searchTerm = document.getElementById('recipeSearch').value.trim();
    if (!searchTerm) {
      alert('Please enter a search term');
      return;
    }

    showLoading();

    try {
      const response = await fetch(`https://www.themealdb.com/api/json/v1/1/search.php?s=${encodeURIComponent(searchTerm)}`);
      const data = await response.json();

      if (data.meals) {
        currentRecipes = data.meals;
        currentPage = 1;
        displayRecipes();
      } else {
        showNoResults(searchTerm);
      }
    } catch (error) {
      showError('Failed to fetch recipes. Please try again.');
      console.error('Recipe search error:', error);
    }
  }

  async function getRandomRecipe() {
    showLoading();

    try {
      // Get multiple random recipes for a better selection
      const promises = Array.from({length: 12}, () => 
        fetch('https://www.themealdb.com/api/json/v1/1/random.php').then(r => r.json())
      );
      
      const results = await Promise.all(promises);
      currentRecipes = results.map(result => result.meals[0]);
      currentPage = 1;
      displayRecipes();
    } catch (error) {
      showError('Failed to fetch random recipes. Please try again.');
      console.error('Random recipe error:', error);
    }
  }

  function displayRecipes() {
    const grid = document.getElementById('recipeGrid');
    const totalPages = Math.ceil(currentRecipes.length / resultsPerPage);
    const startIndex = (currentPage - 1) * resultsPerPage;
    const endIndex = startIndex + resultsPerPage;
    const recipesToShow = currentRecipes.slice(startIndex, endIndex);

    grid.innerHTML = recipesToShow.map(recipe => `
      <div class="recipe-card" onclick="openRecipeModal('${recipe.idMeal}')" style="cursor: pointer;">
        <img src="${recipe.strMealThumb}" alt="${recipe.strMeal}" loading="lazy">
        <div class="recipe-card-content">
          <h3>${recipe.strMeal}</h3>
          <p><strong>Category:</strong> ${recipe.strCategory}</p>
          <p><strong>Cuisine:</strong> ${recipe.strArea}</p>
          ${recipe.strTags ? `<div class="category">${recipe.strTags.split(',')[0]}</div>` : ''}
          <p style="margin-top: 10px;"><strong>Instructions:</strong> ${recipe.strInstructions.substring(0, 120)}...</p>
          <p style="color: #007bff; font-weight: bold; margin-top: 10px;">Click to view full recipe →</p>
        </div>
      </div>
    `).join('');

    updatePaginationInfo();
    updatePagination();
  }

  function updatePaginationInfo() {
    const info = document.getElementById('paginationInfo');
    const totalResults = currentRecipes.length;
    const startIndex = (currentPage - 1) * resultsPerPage + 1;
    const endIndex = Math.min(currentPage * resultsPerPage, totalResults);
    
    info.textContent = `Showing ${startIndex}-${endIndex} of ${totalResults} recipes`;
  }

  function updatePagination() {
    const pagination = document.getElementById('recipePagination');
    const totalPages = Math.ceil(currentRecipes.length / resultsPerPage);

    if (totalPages <= 1) {
      pagination.innerHTML = '';
      return;
    }

    let paginationHTML = '';

    // Previous button
    paginationHTML += `<button onclick="changePage(${currentPage - 1})" ${currentPage === 1 ? 'disabled' : ''}>Previous</button>`;

    // Page numbers
    const startPage = Math.max(1, currentPage - 2);
    const endPage = Math.min(totalPages, currentPage + 2);

    if (startPage > 1) {
      paginationHTML += `<button onclick="changePage(1)">1</button>`;
      if (startPage > 2) {
        paginationHTML += `<span>...</span>`;
      }
    }

    for (let i = startPage; i <= endPage; i++) {
      paginationHTML += `<button onclick="changePage(${i})" ${i === currentPage ? 'class="active"' : ''}>${i}</button>`;
    }

    if (endPage < totalPages) {
      if (endPage < totalPages - 1) {
        paginationHTML += `<span>...</span>`;
      }
      paginationHTML += `<button onclick="changePage(${totalPages})">${totalPages}</button>`;
    }

    // Next button
    paginationHTML += `<button onclick="changePage(${currentPage + 1})" ${currentPage === totalPages ? 'disabled' : ''}>Next</button>`;

    pagination.innerHTML = paginationHTML;
  }

  function changePage(page) {
    const totalPages = Math.ceil(currentRecipes.length / resultsPerPage);
    if (page < 1 || page > totalPages) return;
    
    currentPage = page;
    displayRecipes();
    
    // Scroll to top of results
    document.getElementById('recipeResults').scrollIntoView({ behavior: 'smooth' });
  }

  function changeResultsPerPage() {
    resultsPerPage = parseInt(document.getElementById('resultsPerPage').value);
    currentPage = 1;
    if (currentRecipes.length > 0) {
      displayRecipes();
    }
  }

  function showLoading() {
    document.getElementById('recipeGrid').innerHTML = '<div class="recipe-loading">Loading recipes...</div>';
    document.getElementById('recipePagination').innerHTML = '';
    document.getElementById('paginationInfo').textContent = '';
  }

  function showError(message) {
    document.getElementById('recipeGrid').innerHTML = `<div class="recipe-error">${message}</div>`;
    document.getElementById('recipePagination').innerHTML = '';
    document.getElementById('paginationInfo').textContent = '';
  }

  function showNoResults(searchTerm) {
    document.getElementById('recipeGrid').innerHTML = `
      <div class="no-results">
        <h3>No recipes found for "${searchTerm}"</h3>
        <p>Try searching for different ingredients or dish names.</p>
        <p>Popular searches: chicken, pasta, beef, vegetarian, dessert</p>
      </div>
    `;
    document.getElementById('recipePagination').innerHTML = '';
    document.getElementById('paginationInfo').textContent = '';
  }

  // Recipe Modal Functions
  function openRecipeModal(recipeId) {
    console.log('Opening recipe modal for ID:', recipeId); // Debug log
    
    // Show modal immediately with loading state
    const modal = document.getElementById('recipeModal');
    modal.style.display = 'block';
    document.getElementById('modalRecipeTitle').textContent = 'Loading recipe...';
    document.getElementById('modalRecipeImage').src = '';
    document.getElementById('modalRecipeMeta').innerHTML = '';
    document.getElementById('modalRecipeTags').innerHTML = '';
    document.getElementById('modalIngredients').innerHTML = '<div style="text-align: center; padding: 20px;">Loading ingredients...</div>';
    document.getElementById('modalInstructions').innerHTML = '<div style="text-align: center; padding: 20px;">Loading instructions...</div>';
    document.getElementById('modalYoutubeLink').innerHTML = '';
    
    // Fetch full recipe details
    fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${recipeId}`)
      .then(response => {
        if (!response.ok) {
          throw new Error('Failed to fetch recipe');
        }
        return response.json();
      })
      .then(data => {
        console.log('Recipe data received:', data); // Debug log
        if (data.meals && data.meals[0]) {
          displayRecipeModal(data.meals[0]);
        } else {
          throw new Error('Recipe not found');
        }
      })
      .catch(error => {
        console.error('Error fetching recipe details:', error);
        document.getElementById('modalRecipeTitle').textContent = 'Error loading recipe';
        document.getElementById('modalIngredients').innerHTML = '<div style="text-align: center; padding: 20px; color: red;">Failed to load recipe details. Please try again.</div>';
        document.getElementById('modalInstructions').innerHTML = '';
      });
  }

  function displayRecipeModal(recipe) {
    // Set basic info
    document.getElementById('modalRecipeImage').src = recipe.strMealThumb;
    document.getElementById('modalRecipeImage').alt = recipe.strMeal;
    document.getElementById('modalRecipeTitle').textContent = recipe.strMeal;

    // Set meta information
    const metaHTML = `
      <div class="recipe-meta-item">📂 ${recipe.strCategory}</div>
      <div class="recipe-meta-item">🌍 ${recipe.strArea}</div>
      ${recipe.strSource ? `<div class="recipe-meta-item">📄 <a href="${recipe.strSource}" target="_blank">Source</a></div>` : ''}
    `;
    document.getElementById('modalRecipeMeta').innerHTML = metaHTML;

    // Set tags
    const tagsHTML = recipe.strTags ? 
      recipe.strTags.split(',').map(tag => `<span class="recipe-tag">${tag.trim()}</span>`).join('') : 
      '<span class="recipe-tag">No tags available</span>';
    document.getElementById('modalRecipeTags').innerHTML = tagsHTML;

    // Set ingredients
    const ingredients = [];
    for (let i = 1; i <= 20; i++) {
      const ingredient = recipe[`strIngredient${i}`];
      const measure = recipe[`strMeasure${i}`];
      if (ingredient && ingredient.trim()) {
        ingredients.push({
          name: ingredient.trim(),
          measure: measure ? measure.trim() : ''
        });
      }
    }

    const ingredientsHTML = ingredients.map(ing => `
      <div class="ingredient-item">
        <div class="ingredient-name">${ing.name}</div>
        ${ing.measure ? `<div class="ingredient-measure">${ing.measure}</div>` : ''}
      </div>
    `).join('');
    document.getElementById('modalIngredients').innerHTML = ingredientsHTML;

    // Set instructions
    const instructions = recipe.strInstructions.replace(/\r\n/g, '<br><br>');
    document.getElementById('modalInstructions').innerHTML = instructions;

    // Set YouTube link
    const youtubeHTML = recipe.strYoutube ? 
      `<a href="${recipe.strYoutube}" target="_blank" class="youtube-link">📺 Watch on YouTube</a>` : '';
    document.getElementById('modalYoutubeLink').innerHTML = youtubeHTML;
  }

  function closeRecipeModal() {
    document.getElementById('recipeModal').style.display = 'none';
  }

  // Close modal when clicking outside of it
  window.onclick = function(event) {
    const modal = document.getElementById('recipeModal');
    if (event.target === modal) {
      closeRecipeModal();
    }
  }

  // Close modal with Escape key
  document.addEventListener('keydown', function(event) {
    if (event.key === 'Escape') {
      closeRecipeModal();
    }
  });
</script>
</body>
</html>
