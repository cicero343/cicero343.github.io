---
title: Dashboard
layout: default
permalink: /dashboard/
---

<div id="dashboard-app">

  <!-- Secondary tabs navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="notes">Notes</a>
    <a href="#" data-tab="sheet">Spreadsheet</a>
    <a href="#" data-tab="canvas">Canvas</a>
  </nav>

  <!-- Container for tab content -->
  <div class="dashboard-content">

    <section id="notes" class="tab-content active">
      <h2>Quick Notes</h2>
      <textarea id="notesArea" placeholder="Write your notes here..."></textarea>
      <button class="export-btn" onclick="exportText('notesArea', 'notes.txt')">Export Notes</button>
    </section>

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

<style>
  /* Secondary tabs styles */
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
</style>

---
title: Dashboard
layout: default
permalink: /dashboard/
---

<div id="dashboard-app">

  <!-- Secondary tabs navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="notes">Notes</a>
    <a href="#" data-tab="sheet">Spreadsheet</a>
    <a href="#" data-tab="canvas">Canvas</a>
  </nav>

  <!-- Container for tab content -->
  <div class="dashboard-content">

    <section id="notes" class="tab-content active">
      <h2>Quick Notes</h2>
      <textarea id="notesArea" placeholder="Write your notes here..."></textarea>
      <button class="export-btn" onclick="exportText('notesArea', 'notes.txt')">Export Notes</button>
    </section>

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

<style>
  /* Secondary tabs styles */
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
</style>

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

  // Spreadsheet functions
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

  // Canvas drawing with mouse and touch support
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

  // Mouse events
  canvas.addEventListener('mousedown', startPosition);
  canvas.addEventListener('mouseup', finishedPosition);
  canvas.addEventListener('mouseout', finishedPosition);
  canvas.addEventListener('mousemove', draw);

  // Touch events
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
</script>

