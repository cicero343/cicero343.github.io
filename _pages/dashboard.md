---
title: Dashboard
layout: default
permalink: /dashboard/
---
<style>
/* =============================================================
   Dashboard — terminal theme
   Uses the site-wide theme variables from assets/main.scss
   (--bg, --chrome, --border, --text, --text-dim, --heading,
   --accent, --accent-2) so light/dark switch automatically.
   Only colours/typography/chrome changed vs the old design;
   class names, layout behaviour and JS hooks are unchanged.
   ============================================================= */

/* ---- Extra tokens (severity + helpers) ---------------------- */
:root,
[data-theme="light"] {
  --db-bar:   #e8e8de;          /* title / header bars           */
  --db-raise: #ffffff;          /* cards that sit on --bg        */
  --db-ink:   #ffffff;          /* text on an --accent fill      */
  --db-crit:  #cf222e;
  --db-high:  #bc4c00;
  --db-med:   #9a6700;
  --db-low:   #1a7f37;
  --db-info:  #0969da;
  --db-tint:  rgba(26, 127, 55, 0.08);
  --db-shadow: 0 1px 2px rgba(0, 0, 0, 0.04);
}

[data-theme="dark"] {
  --db-bar:   #1c2129;
  --db-raise: #161b22;
  --db-ink:   #0d1117;
  --db-crit:  #ff7b72;
  --db-high:  #ffa657;
  --db-med:   #d29922;
  --db-low:   #3fb950;
  --db-info:  #58a6ff;
  --db-tint:  rgba(63, 185, 80, 0.10);
  --db-shadow: none;
}

/* ---- Shell: one terminal-style panel ------------------------- */
#dashboard-app {
  border: 1px solid var(--border);
  border-radius: 6px;
  background: var(--bg);
  overflow: hidden;
}

.dashboard-titlebar {
  display: flex;
  align-items: baseline;
  flex-wrap: wrap;
  gap: 4px 12px;
  padding: 8px 15px;
  background: var(--db-bar);
  border-bottom: 1px solid var(--border);
  font-size: 0.9em;
}

.dashboard-titlebar h1 {
  font-size: 1.05rem !important;
  font-weight: 500 !important;
  margin: 0 !important;
  color: var(--heading);
}

.dashboard-titlebar .subtitle {
  font-size: 0.78rem;
  color: var(--text-dim);
}

/* Primary tabs */
.dashboard-tabs {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  gap: 6px;
  padding: 10px 15px;
  background: var(--chrome);
  border-bottom: 1px solid var(--border);
}

.dashboard-tabs a,
.cve-secondary-nav a,
.tools-secondary-nav a {
  color: var(--text);
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 4px 10px;
  border-radius: 3px;
  text-decoration: none;
  cursor: pointer;
  font-size: 0.8rem;
  line-height: 1.5;
  white-space: nowrap;
  transition: background-color 0.15s, color 0.15s, border-color 0.15s;
}

.dashboard-tabs a:visited,
.cve-secondary-nav a:visited,
.tools-secondary-nav a:visited { color: var(--text); }

.dashboard-tabs a:hover,
.cve-secondary-nav a:hover,
.tools-secondary-nav a:hover {
  color: var(--accent);
  border-color: var(--accent);
  text-decoration: none;
}

.dashboard-tabs a.active,
.dashboard-tabs a.active:hover {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}

/* Secondary navs (CVE + Tools) */
.cve-secondary-nav,
.tools-secondary-nav {
  display: none;
  align-items: center;
  justify-content: flex-start;
  flex-wrap: wrap;
  gap: 6px;
  padding: 8px 15px;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
}

.cve-secondary-nav.show,
.tools-secondary-nav.show {
  display: flex;
}

.cve-secondary-nav::before,
.tools-secondary-nav::before {
  color: var(--text-dim);
  font-size: 0.78rem;
  margin-right: 4px;
}
.cve-secondary-nav::before   { content: "cve/"; }
.tools-secondary-nav::before { content: "tools/"; }

.cve-secondary-nav a.active,
.tools-secondary-nav a.active,
.cve-secondary-nav a.active:hover,
.tools-secondary-nav a.active:hover {
  color: var(--accent);
  border-color: var(--accent);
  background: var(--db-tint);
}

/* Content area */
.dashboard-content {
  padding: 20px;
  background: var(--bg);
}

.tab-content,
.cve-sub-tab,
.tools-sub-tab { display: none; }

.tab-content.active,
.cve-sub-tab.active,
.tools-sub-tab.active { display: block; }

/* ---- Base elements inside the dashboard (zero-specificity scope
        so component classes below always win) ------------------ */
:where(#dashboard-app) :where(input, select, textarea, button) {
  font-family: inherit;
}

:where(#dashboard-app) :where(input[type="text"], input[type="number"], select, textarea) {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 6px 10px;
  font-size: 0.85rem;
}

:where(#dashboard-app) :where(input[type="text"], input[type="number"], select, textarea):focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 2px var(--db-tint);
}

:where(#dashboard-app) button {
  background: var(--chrome);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 6px 14px;
  font-size: 0.85rem;
  cursor: pointer;
  transition: background-color 0.15s, color 0.15s, border-color 0.15s;
}

:where(#dashboard-app) button:hover:not(:disabled) {
  color: var(--accent);
  border-color: var(--accent);
}

:where(#dashboard-app) button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

:where(#dashboard-app) label { font-size: 0.85rem; }

/* Section headings ("$ World Clock & Weather" etc.) */
#dashboard-app .tab-content > h2,
#dashboard-app .tools-sub-tab > h2 {
  font-size: 1.05rem;
  color: var(--heading);
  margin: 0 0 16px;
  padding-bottom: 8px;
  border-bottom: 1px dashed var(--border);
}

#dashboard-app .tab-content > h2::before,
#dashboard-app .tools-sub-tab > h2::before {
  content: "$ ";
  color: var(--accent);
}

/* Tool header bar (shared look for Domain / Currency) */
.domain-header,
.currency-header {
  background: var(--db-bar);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 10px 14px;
  margin-bottom: 16px;
  text-align: left;
  color: var(--text);
  position: relative;
}

.domain-header h1, .domain-header h2,
.currency-header h2 {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--heading);
  margin: 0;
  border-left: 3px solid var(--accent);
  padding-left: 12px;
  text-shadow: none;
  line-height: 1.4;
}

.domain-header p,
.currency-header p {
  color: var(--text-dim);
  font-size: 0.78rem;
  margin: 4px 0 0 15px;
  opacity: 1;
}

@keyframes spin {
  0%   { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* =============================================================
   World Clock & Weather
   ============================================================= */
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
  margin-top: 20px;
}

.card {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 14px 16px;
  width: calc(33.333% - 11px);
  box-sizing: border-box;
  text-align: left;
  transition: border-color 0.2s ease;
}

.card:hover { border-color: var(--accent); }

.card h2 {
  margin: 0 0 8px;
  font-size: 0.95rem;
  color: var(--heading);
}

.card p {
  margin: 4px 0;
  font-size: 0.82rem;
  color: var(--text);
}

.card p strong { color: var(--text-dim); font-weight: 500; }
.card .clock { color: var(--accent); }

.card .loading {
  font-style: italic;
  color: var(--text-dim);
}

@media (max-width: 900px) {
  .card { width: calc(50% - 8px); }
}

@media (max-width: 600px) {
  .card { width: 100%; }
}

/* =============================================================
   UK Foodbanks
   ============================================================= */
#foodbanks form {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 8px 10px;
  margin-bottom: 1rem;
}

#foodbanks input[type="text"] { width: 180px; }

#foodbanks button[type="submit"] {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}
#foodbanks button[type="submit"]:hover { color: var(--db-ink); filter: brightness(1.1); }

#error {
  color: var(--db-crit);
  margin-bottom: 15px;
  display: none;
  font-size: 0.85rem;
}

.foodbank {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 4px;
  padding: 12px 14px;
  margin-bottom: 12px;
  font-size: 0.85rem;
}

.foodbank h3 {
  margin: 0 0 6px !important;
  font-size: 0.95rem;
  color: var(--heading);
}

.foodbank p { margin: 4px 0 !important; }

/* =============================================================
   Currency Exchange
   ============================================================= */
.currency-exchange-container {
  max-width: 480px;
  margin: 0 auto;
}

.currency-control-panel,
.currency-rates-container {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
}

.currency-control-panel {
  padding: 14px;
  margin-bottom: 16px;
}

.currency-controls {
  display: grid;
  grid-template-columns: 80px 1fr auto; /* Amount, Currency, Convert */
  gap: 8px;
  align-items: end;
}

.currency-control-group label {
  display: block;
  font-size: 0.75rem;
  color: var(--text-dim);
  margin-bottom: 2px;
}

.currency-control-group select,
.currency-control-group input {
  width: 100%;
  box-sizing: border-box;
}

.currency-control-group input[type="number"] {
  text-align: center;
  max-width: 80px;
}

.currency-convert-btn {
  background: var(--accent) !important;
  border-color: var(--accent) !important;
  color: var(--db-ink) !important;
  white-space: nowrap;
}
.currency-convert-btn:hover:not(:disabled) { filter: brightness(1.1); }

.currency-rates-container { overflow: hidden; }

.currency-rates-header {
  background: var(--db-bar);
  padding: 12px 16px;
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.currency-base-amount {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--heading);
}

.currency-last-updated {
  font-size: 0.72rem;
  color: var(--text-dim);
  text-align: right;
}

.currency-rate-row {
  display: flex;
  align-items: center;
  padding: 10px 16px;
  border-bottom: 1px solid var(--border);
}

.currency-rate-row:last-child { border-bottom: none; }
.currency-rate-row:hover,
.currency-rate-row:active { background-color: var(--bg); }

.currency-flag {
  width: 24px;
  height: 18px;
  border: 1px solid var(--border);
  border-radius: 2px;
  margin-right: 12px;
  object-fit: cover;
}

.currency-info {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 8px;
}

.currency-code {
  font-weight: 600;
  font-size: 0.88rem;
  color: var(--accent);
  line-height: 1.2;
  min-width: 45px;
}

.currency-name {
  color: var(--text-dim);
  font-size: 0.72rem;
  line-height: 1.2;
}

.currency-rate-value {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--heading);
  text-align: right;
  font-variant-numeric: tabular-nums;
}

.currency-loading,
.currency-error {
  text-align: center;
  padding: 28px 20px;
  color: var(--text-dim);
  font-size: 0.85rem;
}

.currency-error { color: var(--db-crit); }

@media (max-width: 576px) {
  .currency-control-panel { padding: 10px; }
  .currency-controls {
    grid-template-columns: 60px 1fr auto;
    gap: 6px;
  }
  .currency-rate-row { padding: 12px 14px; }
  .currency-rates-header {
    padding: 12px 14px;
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
  }
  .currency-last-updated { text-align: left; }
}

/* =============================================================
   Domain Lookup
   ============================================================= */
.domain-container {
  max-width: 1200px;
  margin: 0 auto;
}

.domain-search-section {
  padding: 0 0 16px;
}

.domain-search-box {
  display: flex;
  gap: 8px;
}

#domain-input {
  flex: 1;
  padding: 8px 12px;
  font-size: 0.9rem;
}

#analyze-btn {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
  white-space: nowrap;
}
#analyze-btn:hover:not(:disabled) { color: var(--db-ink); filter: brightness(1.1); }

.domain-results-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.domain-result-card {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  min-width: 0;
}

.domain-card-header {
  background: var(--db-bar);
  color: var(--heading);
  border-bottom: 1px solid var(--border);
  padding: 8px 12px;
  font-weight: 600;
  font-size: 0.85rem;
}

.domain-card-content {
  padding: 12px;
  max-height: 400px;
  overflow-y: auto;
  font-size: 0.8rem;
  word-break: break-word;
}

.domain-dns-record {
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 6px 8px;
  margin: 5px 0;
  border-radius: 3px;
}

.domain-cert-item {
  border-bottom: 1px solid var(--border);
  padding: 8px 0;
}
.domain-cert-item:last-child { border-bottom: none; }

.domain-cert-cn     { font-weight: bold; color: var(--heading); }
.domain-cert-dates  { font-size: 0.72rem; color: var(--text-dim); margin: 4px 0; }
.domain-cert-issuer { font-size: 0.72rem; color: var(--accent); }

.domain-archive-info {
  text-align: center;
  padding: 16px;
}

.domain-archive-link,
.domain-archive-link:visited {
  display: inline-block;
  background: var(--accent);
  color: var(--db-ink);
  padding: 6px 14px;
  text-decoration: none;
  border-radius: 4px;
  margin-top: 10px;
}
.domain-archive-link:hover { color: var(--db-ink); text-decoration: none; filter: brightness(1.1); }

.domain-loading {
  text-align: center;
  color: var(--text-dim);
  font-style: italic;
  padding: 16px;
}

.domain-error,
.domain-card-content .error {
  background: rgba(207, 34, 46, 0.08);
  color: var(--db-crit);
  border: 1px solid var(--db-crit);
  padding: 8px 10px;
  border-radius: 3px;
  margin: 8px 0;
}

.domain-status-indicator,
.status-indicator {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 8px;
}

.domain-status-online,  .status-online  { background: var(--db-low); }
.domain-status-offline, .status-offline { background: var(--db-crit); }

/* =============================================================
   Food Recipes (+ modal)
   ============================================================= */
.recipe-search-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.recipe-search-bar input[type="text"] {
  flex: 1;
  min-width: 200px;
  padding: 8px 12px;
}

.recipe-search-bar button:first-of-type {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}
.recipe-search-bar button:first-of-type:hover { color: var(--db-ink); filter: brightness(1.1); }

.recipe-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
  flex-wrap: wrap;
  gap: 10px;
}

.results-per-page {
  display: flex;
  align-items: center;
  gap: 10px;
}

.recipe-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 16px;
  margin-bottom: 24px;
}

.recipe-card {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  cursor: pointer;
  transition: border-color 0.2s ease, transform 0.2s ease;
}

.recipe-card:hover {
  border-color: var(--accent);
  transform: translateY(-2px);
}

.recipe-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  display: block;
}

.recipe-card-content { padding: 12px 14px; }

.recipe-card h3 {
  margin: 0 0 8px !important;
  font-size: 0.95rem;
  color: var(--heading);
}

.recipe-card p {
  margin: 4px 0 !important;
  color: var(--text-dim);
  font-size: 0.78rem;
  line-height: 1.5;
}

.recipe-card .category,
.recipe-tag {
  display: inline-block;
  background: var(--db-tint);
  color: var(--accent);
  border: 1px solid var(--border);
  padding: 1px 8px;
  border-radius: 3px;
  font-size: 0.72rem;
}

.recipe-card .category { margin-top: 8px; }

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 20px;
}

.pagination button { padding: 4px 10px; font-size: 0.8rem; }

.pagination button.active {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}

.pagination-info {
  font-size: 0.8rem;
  color: var(--text-dim);
}

.recipe-loading,
.no-results {
  text-align: center;
  padding: 40px;
  color: var(--text-dim);
  font-style: italic;
}

.no-results {
  background: var(--chrome);
  border: 1px dashed var(--border);
  border-radius: 4px;
  margin: 20px 0;
  font-style: normal;
}

.recipe-error {
  text-align: center;
  padding: 30px;
  color: var(--db-crit);
  border: 1px solid var(--db-crit);
  border-radius: 4px;
  margin: 20px 0;
}

.recipe-modal {
  display: none;
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  overflow-y: auto;
}

.recipe-modal-content {
  background-color: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
  margin: 2% auto;
  padding: 0;
  border-radius: 6px;
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
  border-radius: 6px 6px 0 0;
  display: block;
}

.close-modal {
  position: absolute;
  top: 12px;
  right: 14px;
  color: #fff;
  font-size: 24px;
  font-weight: bold;
  cursor: pointer;
  background: rgba(0, 0, 0, 0.55) !important;
  border: 1px solid rgba(255, 255, 255, 0.25) !important;
  border-radius: 50% !important;
  width: 36px;
  height: 36px;
  padding: 0 !important;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  line-height: 1;
}

.close-modal:hover { background: rgba(0, 0, 0, 0.75) !important; color: #fff !important; }

.recipe-modal-body { padding: 24px; }

.recipe-modal-body h2 {
  margin: 0 0 12px;
  color: var(--heading);
  font-size: 1.3rem;
}

.recipe-meta {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.recipe-meta-item {
  background: var(--chrome);
  border: 1px solid var(--border);
  padding: 4px 12px;
  border-radius: 3px;
  font-size: 0.8rem;
  color: var(--text-dim);
}

.recipe-tags { margin-bottom: 20px; }
.recipe-tag { margin: 0 6px 6px 0; }

.recipe-section { margin-bottom: 26px; }

.recipe-section h3 {
  color: var(--heading);
  margin: 0 0 12px;
  font-size: 1rem;
  border-bottom: 1px dashed var(--border);
  padding-bottom: 6px;
}

.ingredients-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 8px;
  margin-bottom: 20px;
}

.ingredient-item {
  background: var(--chrome);
  padding: 8px 12px;
  border-radius: 3px;
  border-left: 3px solid var(--accent);
  font-size: 0.82rem;
}

.ingredient-name    { font-weight: bold; color: var(--heading); }
.ingredient-measure { color: var(--text-dim); font-size: 0.9em; }

.instructions {
  line-height: 1.7;
  color: var(--text);
  font-size: 0.88rem;
}

.youtube-link,
.youtube-link:visited {
  display: inline-block;
  background: #cc0000;
  color: #fff;
  padding: 6px 16px;
  border-radius: 4px;
  text-decoration: none;
  font-weight: bold;
  margin-top: 15px;
}
.youtube-link:hover { background: #a30000; color: #fff; text-decoration: none; }

@media (max-width: 600px) {
  .recipe-modal-content { width: 95%; margin: 5% auto; }
  .recipe-modal-body { padding: 18px; }
  .ingredients-list { grid-template-columns: 1fr; }
}

/* =============================================================
   Notes & Tools
   ============================================================= */
#notesArea {
  width: 100%;
  height: 200px;
  margin-top: 4px;
  padding: 10px;
  font-size: 0.85rem;
  resize: vertical;
  box-sizing: border-box;
}

button.export-btn,
button.table-btn {
  margin: 10px 5px 20px 0;
}

button.export-btn {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}
button.export-btn:hover { color: var(--db-ink) !important; filter: brightness(1.1); }

#spreadsheet {
  border-collapse: collapse;
  width: 100%;
  background: var(--bg);
  margin-bottom: 20px;
  font-size: 0.85rem;
}

#spreadsheet th,
#spreadsheet td {
  border: 1px solid var(--border);
  padding: 6px 8px;
  text-align: left;
}

#spreadsheet th {
  background: var(--db-bar);
  color: var(--heading);
}

#spreadsheet td[contenteditable] { background-color: var(--chrome); }

#spreadsheet th:focus,
#spreadsheet td:focus {
  outline: 2px solid var(--accent);
  outline-offset: -2px;
}

.canvas-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 10px 16px;
  margin-top: 10px;
  font-size: 0.85rem;
}

.canvas-controls input[type="color"] {
  vertical-align: middle;
  width: 34px;
  height: 24px;
  padding: 0;
  border: 1px solid var(--border);
  border-radius: 3px;
  background: none;
}

.canvas-controls input[type="range"] {
  vertical-align: middle;
  accent-color: var(--accent);
}

#drawCanvas {
  border: 1px solid var(--border);
  border-radius: 4px;
  background: #ffffff; /* drawing surface stays white in both themes */
  cursor: crosshair;
  display: block;
  margin: 16px auto;
  /* no max-width: the drawing code maps pointer coords 1:1 to canvas pixels */
}

/* =============================================================
   CVE hub (Lookup + GHSA / Patch Tuesday / KEV feeds)
   ============================================================= */
.cvh-head {
  background: var(--db-bar);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 10px 14px;
  margin-bottom: 14px;
}

.cvh-head h1 {
  font-size: 1.05rem !important;
  font-weight: 600;
  color: var(--heading);
  margin: 0 !important;
  border-left: 3px solid var(--accent);
  padding-left: 12px;
  line-height: 1.4;
}

.cvh-head p {
  color: var(--text-dim);
  font-size: 0.78rem;
  margin: 4px 0 0 15px !important;
  line-height: 1.5;
}

/* search + controls */
.cvh-search,
.cvh-controls {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  align-items: center;
  margin-bottom: 10px;
}

.cvh-search input[type="text"] { flex: 1 1 220px; min-width: 0; padding: 8px 12px; font-size: 0.9rem; }
.cvh-controls input[type="text"] { flex: 1 1 160px; min-width: 0; }
.cvh-controls select,
.cvh-search select { font-size: 0.8rem; }

.cvh-primary {
  background: var(--accent) !important;
  border-color: var(--accent) !important;
  color: var(--db-ink) !important;
  font-weight: 600;
}
.cvh-primary:hover { filter: brightness(1.1); }

.cvh-check {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-size: 0.78rem !important;
  color: var(--text-dim);
  cursor: pointer;
  white-space: nowrap;
}
.cvh-check input { accent-color: var(--accent); }

.cvh-seg { display: inline-flex; }
.cvh-seg button {
  border-radius: 0 !important;
  margin-left: -1px;
  padding: 5px 12px !important;
  font-size: 0.8rem !important;
}
.cvh-seg button:first-child { border-radius: 4px 0 0 4px !important; margin-left: 0; }
.cvh-seg button:last-child  { border-radius: 0 4px 4px 0 !important; }
.cvh-seg button.active {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
  position: relative;
}

.cvh-examples {
  font-size: 0.75rem;
  color: var(--text-dim);
  margin-bottom: 12px;
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  align-items: center;
}
.cvh-examples button {
  padding: 1px 8px !important;
  font-size: 0.72rem !important;
  background: transparent;
}

/* per-source status chips */
.cvh-status {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 12px;
}
.cvh-status:empty { display: none; }

.cvh-chip {
  font-size: 0.7rem !important;
  padding: 1px 8px !important;
  border-radius: 3px !important;
  background: var(--chrome);
  cursor: default !important;
}
.cvh-chip small { color: inherit; opacity: 0.85; }
.cvh-chip-loading { color: var(--text-dim) !important; }
.cvh-chip-ok      { color: var(--db-low) !important; border-color: color-mix(in srgb, var(--db-low) 45%, var(--border)) !important; }
.cvh-chip-none    { color: var(--text-dim) !important; border-style: dashed !important; }
.cvh-chip-fail    { color: var(--db-crit) !important; border-color: var(--db-crit) !important; cursor: pointer !important; }
.cvh-chip-ok:hover, .cvh-chip-none:hover, .cvh-chip-loading:hover { border-color: var(--border) !important; }

/* source tag */
.cvh-src {
  display: inline-block;
  font-size: 0.6rem;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: var(--accent-2);
  border: 1px solid color-mix(in srgb, var(--accent-2) 45%, var(--border));
  border-radius: 3px;
  padding: 0 4px;
  line-height: 1.5;
  vertical-align: middle;
  white-space: nowrap;
  cursor: help;
}
.cvh-tags { display: inline-flex; gap: 4px; flex-wrap: wrap; justify-content: flex-end; }

/* result card */
.cvh-card {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 4px;
  padding: 14px;
  margin-bottom: 10px;
}

.cvh-card-head {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  flex-wrap: wrap;
  gap: 6px 12px;
}

.cvh-id { font-size: 1.2rem; font-weight: 700; color: var(--accent); }

.cvh-quicklinks { display: flex; flex-wrap: wrap; gap: 4px 10px; font-size: 0.75rem; }

.cvh-title { margin-top: 4px; color: var(--heading); font-weight: 600; font-size: 0.9rem; }

.cvh-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 2px 14px;
  font-size: 0.72rem;
  color: var(--text-dim);
  margin: 6px 0 10px;
}

.cvh-tiles {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 8px;
}
.cvh-tiles-sm { grid-template-columns: repeat(auto-fit, minmax(110px, 1fr)); margin-bottom: 8px; }

.cvh-tile {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 8px 10px;
  min-width: 0;
}
.cvh-tile-label {
  font-size: 0.68rem;
  color: var(--text-dim);
  text-transform: uppercase;
  letter-spacing: 0.04em;
  display: flex;
  align-items: center;
  gap: 5px;
  flex-wrap: wrap;
}
.cvh-tile-val { font-size: 1.15rem; font-weight: 700; color: var(--heading); margin: 2px 0; line-height: 1.3; }
.cvh-tile-val .cvh-sev { font-size: 0.85rem; }
.cvh-tile-text { font-size: 0.85rem; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.cvh-tile-sub { font-size: 0.7rem; color: var(--text-dim); line-height: 1.4; }
.cvh-hot { color: var(--db-crit) !important; }
.cvh-c-crit { color: var(--db-crit) !important; }
.cvh-c-high { color: var(--db-high) !important; }

/* collapsible sections */
.cvh-sec {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  margin-bottom: 8px;
}
.cvh-sec > summary {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  padding: 8px 12px;
  cursor: pointer;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--heading);
  list-style: none;
}
.cvh-sec > summary::-webkit-details-marker { display: none; }
.cvh-sec > summary > span:first-child::before { content: "▸ "; color: var(--accent); }
.cvh-sec[open] > summary > span:first-child::before { content: "▾ "; }
.cvh-sec[open] > summary { border-bottom: 1px solid var(--border); }
.cvh-sec-body { padding: 10px 12px; font-size: 0.82rem; }

.cvh-count {
  font-size: 0.68rem;
  color: var(--text-dim);
  font-weight: 400;
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 0 5px;
  margin-left: 4px;
}

.cvh-desc { margin: 0 0 8px !important; line-height: 1.6; white-space: pre-line; }
.cvh-cwes { display: flex; flex-wrap: wrap; gap: 6px; font-size: 0.75rem; }

.cvh-dl {
  display: grid;
  grid-template-columns: max-content 1fr;
  gap: 4px 14px;
  margin: 0;
  font-size: 0.8rem;
}
.cvh-dl dt { color: var(--text-dim); }
.cvh-dl dd { margin: 0; min-width: 0; word-break: break-word; }

.cvh-table-wrap { overflow-x: auto; margin-bottom: 6px; }
.cvh-table { width: 100%; border-collapse: collapse; font-size: 0.75rem; }
.cvh-table th, .cvh-table td {
  text-align: left;
  padding: 5px 8px;
  border-bottom: 1px solid var(--border);
  vertical-align: top;
}
.cvh-table th { color: var(--text-dim); font-weight: 600; white-space: nowrap; }
.cvh-table tr:last-child td { border-bottom: none; }
.cvh-vector { font-size: 0.7rem; color: var(--text-dim); word-break: break-all; }

.cvh-pill {
  display: inline-block;
  font-size: 0.7rem;
  border: 1px solid var(--border);
  background: var(--bg);
  border-radius: 3px;
  padding: 0 6px;
  margin: 0 4px 3px 0;
  white-space: nowrap;
  max-width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
  vertical-align: middle;
}
.cvh-pill-warn { border-color: var(--db-med); color: var(--db-med); }
.cvh-pills { display: flex; flex-wrap: wrap; }
.cvh-eco { color: var(--accent-2); font-size: 0.68rem; text-transform: lowercase; }

.cvh-refs { margin: 0; padding-left: 0; list-style: none; font-size: 0.75rem; }
.cvh-refs li { padding: 3px 0; border-bottom: 1px dashed var(--border); word-break: break-all; }
.cvh-refs li:last-child { border-bottom: none; }
.cvh-refs-inline { word-break: break-all; }

/* severity + flags */
.cvh-sev {
  display: inline-block;
  font-size: 0.68rem;
  font-weight: 700;
  text-transform: uppercase;
  border: 1px solid currentColor;
  border-radius: 3px;
  padding: 0 6px;
  line-height: 1.6;
  white-space: nowrap;
}
.cvh-sev-crit { color: var(--db-crit); background: color-mix(in srgb, var(--db-crit) 10%, transparent); }
.cvh-sev-high { color: var(--db-high); background: color-mix(in srgb, var(--db-high) 10%, transparent); }
.cvh-sev-med  { color: var(--db-med);  background: color-mix(in srgb, var(--db-med) 10%, transparent); }
.cvh-sev-low  { color: var(--db-low);  background: color-mix(in srgb, var(--db-low) 10%, transparent); }
.cvh-sev-none { color: var(--text-dim); }

.cvh-flag {
  display: inline-block;
  font-size: 0.65rem;
  font-weight: 700;
  text-transform: uppercase;
  color: #fff;
  background: var(--db-crit);
  border-radius: 3px;
  padding: 0 5px;
  line-height: 1.6;
  white-space: nowrap;
}
.cvh-flag-soft { background: transparent; color: var(--db-high); border: 1px solid currentColor; }
[data-theme="dark"] .cvh-flag:not(.cvh-flag-soft) { color: #0d1117; }

/* lists (keyword results + feeds) */
.cvh-list { display: flex; flex-direction: column; gap: 6px; }

.cvh-listhead {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 6px;
  font-size: 0.75rem;
  color: var(--text-dim);
  margin-bottom: 8px;
}

.cvh-row,
.cvh-item {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent-2);
  border-radius: 4px;
  padding: 8px 10px;
  min-width: 0;
}
.cvh-item-hot { border-left-color: var(--db-crit); }
.cvh-item > summary { list-style: none; cursor: pointer; }
.cvh-item > summary::-webkit-details-marker { display: none; }
.cvh-item[open] { border-color: var(--accent); }
.cvh-item-body { margin-top: 8px; padding-top: 8px; border-top: 1px dashed var(--border); }
.cvh-item-body p { margin: 0 0 6px !important; }

.cvh-row-top {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 4px 8px;
  font-size: 0.78rem;
}
.cvh-date { margin-left: auto; font-size: 0.7rem; color: var(--text-dim); white-space: nowrap; }
.cvh-row-title { font-size: 0.82rem; color: var(--heading); margin-top: 4px; line-height: 1.45; }
.cvh-row-desc {
  font-size: 0.78rem;
  color: var(--text);
  margin-top: 4px;
  line-height: 1.45;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.cvh-pkgs { margin-top: 5px; }
.cvh-mono-sm { font-size: 0.7rem; }

.cvh-cvebtn {
  font-weight: 700 !important;
  color: var(--accent) !important;
  background: transparent !important;
  border: none !important;
  padding: 0 !important;
  font-size: 0.82rem !important;
  text-decoration: underline;
  text-decoration-style: dotted;
  text-underline-offset: 3px;
}
.cvh-cvebtn:hover { text-decoration-style: solid; }

.cvh-link {
  background: none !important;
  border: none !important;
  padding: 0 !important;
  color: var(--accent) !important;
  text-decoration: underline;
  font-size: inherit !important;
}

.cvh-pager {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  margin-top: 12px;
  font-size: 0.8rem;
}

/* GHSA per-day histogram */
.cvh-hist {
  display: flex;
  align-items: flex-end;
  gap: 3px;
  height: 64px;
  margin: 4px 0 6px;
}
.cvh-bar {
  flex: 1;
  height: 100%;
  display: flex !important;
  flex-direction: column;
  justify-content: flex-end;
  align-items: stretch;
  padding: 0 !important;
  border: none !important;
  background: transparent !important;
  min-width: 0;
}
.cvh-bar span {
  display: block;
  min-height: 2px;
  background: color-mix(in srgb, var(--accent) 55%, transparent);
  border-radius: 2px 2px 0 0;
}
.cvh-bar em { font-style: normal; font-size: 0.6rem; color: var(--text-dim); line-height: 1.4; }
.cvh-bar:hover span, .cvh-bar.active span { background: var(--accent); }
.cvh-bar.active em { color: var(--accent); font-weight: 700; }

/* misc */
.cvh-empty {
  text-align: center;
  padding: 32px 16px;
  color: var(--text-dim);
  font-size: 0.85rem;
  background: var(--chrome);
  border: 1px dashed var(--border);
  border-radius: 4px;
}
.cvh-big { font-size: 1.6rem; color: var(--accent); }
.cvh-error {
  color: var(--db-crit);
  background: color-mix(in srgb, var(--db-crit) 8%, transparent);
  border: 1px solid var(--db-crit);
  border-left-width: 3px;
  border-radius: 4px;
  padding: 10px 12px;
  font-size: 0.82rem;
}
.cvh-small { font-size: 0.75rem; line-height: 1.55; margin: 6px 0 0; }
.cvh-dim { color: var(--text-dim); }

.cvh-spin {
  display: inline-block;
  width: 11px;
  height: 11px;
  border: 2px solid var(--border);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.9s linear infinite;
  vertical-align: -1px;
}

@media (max-width: 600px) {
  .cvh-search select { flex: 1 1 auto; }
  .cvh-search .cvh-primary { flex: 0 0 auto; }
  .cvh-controls select { flex: 1 1 40%; }
  .cvh-tiles { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .cvh-tiles-sm { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .cvh-dl { grid-template-columns: 1fr; gap: 0; }
  .cvh-dl dt { margin-top: 6px; }
  .cvh-table th:nth-child(4), .cvh-table td:nth-child(4) { display: none; } /* hide long vectors / advisory col on phones */
  .cvh-date { margin-left: 0; }
}

/* =============================================================
   Responsive
   ============================================================= */
@media (max-width: 768px) {
  /* Tab bar: 3 per row on phones (same layout as before) */
  .dashboard-tabs {
    padding: 8px;
    gap: 4px;
  }

  .dashboard-tabs a {
    flex: 0 0 calc(33.333% - 3px);
    width: calc(33.333% - 3px);
    padding: 6px 2px;
    font-size: 0.72rem;
    text-align: center;
    overflow: hidden;
    text-overflow: ellipsis;
    box-sizing: border-box;
  }

  /* Secondary navs: 2 per row */
  .cve-secondary-nav,
  .tools-secondary-nav {
    padding: 6px 8px;
    gap: 4px;
  }

  .cve-secondary-nav::before,
  .tools-secondary-nav::before { display: none; }

  .cve-secondary-nav a,
  .tools-secondary-nav a {
    flex: 0 0 calc(50% - 2px);
    width: calc(50% - 2px);
    padding: 6px 2px;
    font-size: 0.72rem;
    text-align: center;
    overflow: hidden;
    text-overflow: ellipsis;
    box-sizing: border-box;
  }

  .tools-secondary-nav a { flex-basis: calc(33.333% - 3px); width: calc(33.333% - 3px); }

  .dashboard-content { padding: 14px 12px; }


  .domain-results-grid { grid-template-columns: 1fr; }

  .domain-search-box { flex-direction: column; }
}

@media (max-width: 480px) {
  .dashboard-tabs a,
  .cve-secondary-nav a,
  .tools-secondary-nav a { font-size: 0.68rem; }
  .dashboard-titlebar .subtitle { display: none; }
}
</style>

<div id="dashboard-app">

  <!-- Title bar -->
  <div class="dashboard-titlebar">
    <h1>~/dashboard</h1>
    <span class="subtitle">clocks, cve feeds, lookups &amp; tools</span>
  </div>

  <!-- Primary Navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="world">World</a>
    <a href="#" data-tab="cve">CVE Tracker</a>
    <a href="#" data-tab="foodbanks">UK Foodbanks</a>
    <a href="#" data-tab="exchange">Exchange Rates</a>
    <a href="#" data-tab="domain">Domain Lookup</a>
    <a href="#" data-tab="recipes">Food Recipes</a>
    <a href="#" data-tab="tools">Notes & Tools</a>
  </nav>

  <!-- Secondary CVE Navigation -->
  <nav class="cve-secondary-nav" id="cve-secondary-nav">
    <a href="#" class="active" data-cve-tab="cve-lookup">Lookup</a>
    <a href="#" data-cve-tab="cve-ghsa">GHSA feed</a>
    <a href="#" data-cve-tab="cve-msrc">Patch Tuesday</a>
    <a href="#" data-cve-tab="cve-kev">CISA KEV</a>
  </nav>

  <!-- Secondary Tools Navigation -->
<nav class="tools-secondary-nav" id="tools-secondary-nav">
  <a href="#" class="active" data-tools-tab="notes">Notes</a>
  <a href="#" data-tools-tab="sheet">Spreadsheet</a>
  <a href="#" data-tools-tab="canvas">Canvas</a>
</nav>

  <div class="dashboard-content">

    <!-- World Clock Tab -->
    <section id="world" class="tab-content active">
      <h2>🌍 World Clock & Weather</h2>
      <div class="grid" id="dashboard-grid"></div>
    </section>

    <!-- CVE Tracker Tab: Lookup + feeds (every result is tagged with its source) -->
    <section id="cve" class="tab-content">

      <!-- Lookup: one CVE across every source, or a keyword/product search -->
      <div id="cve-lookup" class="cve-sub-tab active">
        <div class="cvh-head">
          <h1>🔎 CVE lookup</h1>
          <p>One search across NVD, CVE.org, Shodan CVEDB, FIRST EPSS, OSV/GHSA and MSRC. Each source loads on its own, so if one is down the rest still show.</p>
        </div>
        <form id="cvh-lookup-form" class="cvh-search" autocomplete="off">
          <input type="text" id="cvh-q" placeholder="CVE-2024-3094, or a keyword" spellcheck="false" autocapitalize="off">
          <select id="cvh-mode" title="Where to search when the query isn't a CVE ID">
            <option value="nvd">keyword · NVD</option>
            <option value="cvedb">product · CVEDB by EPSS</option>
          </select>
          <button type="submit" class="cvh-primary">lookup</button>
        </form>
        <div class="cvh-examples">try:
          <button type="button" data-q="CVE-2024-3094">CVE-2024-3094</button>
          <button type="button" data-q="CVE-2021-44228">CVE-2021-44228</button>
          <button type="button" data-q="CVE-2023-23397">CVE-2023-23397</button>
          <button type="button" data-q="fortios" data-mode="cvedb">fortios (by EPSS)</button>
        </div>
        <div id="cvh-status" class="cvh-status"></div>
        <div id="cvh-result"></div>
      </div>

      <!-- GHSA feed -->
      <div id="cve-ghsa" class="cve-sub-tab">
        <div class="cvh-head">
          <h1>📦 GitHub Security Advisories</h1>
          <p>Newest advisories from the GitHub Advisory Database. Pick a timeframe to load.</p>
        </div>
        <div class="cvh-controls">
          <div class="cvh-seg" id="cvh-ghsa-range">
            <button type="button" data-range="1">1d</button><button type="button" data-range="3">3d</button><button type="button" data-range="7">7d</button>
          </div>
          <select id="cvh-ghsa-sev" title="Severity (filtered by GitHub)">
            <option value="">all severities</option><option value="critical">critical</option><option value="high">high</option><option value="medium">medium</option><option value="low">low</option>
          </select>
          <select id="cvh-ghsa-eco" title="Ecosystem">
            <option value="">all ecosystems</option><option value="npm">npm</option><option value="pip">pip</option><option value="maven">maven</option><option value="go">go</option><option value="nuget">nuget</option><option value="composer">composer</option><option value="rubygems">rubygems</option><option value="rust">rust</option><option value="actions">actions</option>
          </select>
          <select id="cvh-ghsa-type" title="Advisory type">
            <option value="reviewed">reviewed</option><option value="unreviewed">unreviewed</option><option value="malware">malware</option>
          </select>
          <input type="text" id="cvh-ghsa-filter" placeholder="filter: package, CVE, text">
        </div>
        <div id="cvh-ghsa-stats"></div>
        <div id="cvh-ghsa-list" class="cvh-list"><div class="cvh-empty"><span class="cvh-big">▸</span><br>Pick a timeframe to fetch the latest advisories</div></div>
      </div>

      <!-- Patch Tuesday (MSRC) -->
      <div id="cve-msrc" class="cve-sub-tab">
        <div class="cvh-head">
          <h1>🪟 Microsoft Patch Tuesday</h1>
          <p>Microsoft's Security Update Guide for a release month. Falls back to the full CVRF document if the API is unavailable.</p>
        </div>
        <div class="cvh-controls">
          <select id="cvh-msrc-month" title="Release month"></select>
          <select id="cvh-msrc-src" title="Data source">
            <option value="sug">Update Guide API (fast)</option>
            <option value="cvrf">CVRF document (~20 MB)</option>
          </select>
          <button type="button" id="cvh-msrc-load" class="cvh-primary">load</button>
        </div>
        <div class="cvh-controls">
          <select id="cvh-msrc-sev" title="Severity">
            <option value="">all severities</option><option value="critical">critical</option><option value="important">important</option><option value="moderate">moderate</option><option value="low">low</option>
          </select>
          <label class="cvh-check"><input type="checkbox" id="cvh-msrc-ex"> exploited / disclosed only</label>
          <label class="cvh-check" title="Chromium (Edge), GitHub, Azure Linux etc."><input type="checkbox" id="cvh-msrc-third"> include third-party</label>
          <input type="text" id="cvh-msrc-filter" placeholder="filter: product, CVE, title">
        </div>
        <div id="cvh-msrc-stats"></div>
        <div id="cvh-msrc-list" class="cvh-list"><div class="cvh-empty"><span class="cvh-big">▸</span><br>Choose a month and press load</div></div>
      </div>

      <!-- CISA KEV -->
      <div id="cve-kev" class="cve-sub-tab">
        <div class="cvh-head">
          <h1>🚨 CISA Known Exploited Vulnerabilities</h1>
          <p>CVEs confirmed as exploited in the wild, newest additions first.</p>
        </div>
        <div class="cvh-controls">
          <div class="cvh-seg" id="cvh-kev-range">
            <button type="button" data-range="7">7d</button><button type="button" data-range="30">30d</button><button type="button" data-range="90">90d</button><button type="button" data-range="0">all</button>
          </div>
          <label class="cvh-check"><input type="checkbox" id="cvh-kev-ransom"> ransomware-linked only</label>
          <input type="text" id="cvh-kev-filter" placeholder="filter: vendor, product, CVE">
        </div>
        <div id="cvh-kev-stats"></div>
        <div id="cvh-kev-list" class="cvh-list"><div class="cvh-empty"><span class="cvh-big">▸</span><br>Pick a timeframe to load the catalogue</div></div>
      </div>

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
  <div class="currency-exchange-container">
    <div class="currency-header">
      <h2>Currency Exchange</h2>
      <p>Exchange rates via Frankfurter API</p>
    </div>

    <div class="currency-control-panel">
      <div class="currency-controls">
        <div class="currency-control-group">
          <label>Amount</label>
          <input type="number" id="currencyAmount" value="1" min="0.01" step="0.01">
        </div>
        <div class="currency-control-group">
          <label>Currency</label>
          <select id="currencyBaseCurrency">
            <option value="GBP">GBP</option>
            <option value="USD">USD</option>
            <option value="EUR">EUR</option>
            <option value="JPY">JPY</option>
            <option value="AUD">AUD</option>
            <option value="CAD">CAD</option>
            <option value="CHF">CHF</option>
            <option value="CNY">CNY</option>
          </select>
        </div>
        <button class="currency-convert-btn" onclick="convertCurrency()" id="currencyConvertBtn">
          Convert
        </button>
      </div>
    </div>

    <div class="currency-rates-container">
      <div class="currency-rates-header">
        <div class="currency-base-amount" id="currencyBaseAmount">1 GBP equals:</div>
        <div class="currency-last-updated" id="currencyLastUpdated">Loading...</div>
      </div>

      <div class="currency-rates-table" id="currencyRatesTable">
        <div class="currency-loading">Loading exchange rates...</div>
      </div>
    </div>
  </div>
</section>


<!-- Domain Lookup Tab -->
<section id="domain" class="tab-content">
  <div class="domain-container">
    <div class="domain-header">
      <h1>🔍 Domain Lookup</h1>
      <p>Domain analysis using Cloudflare DNS over HTTPS, crt.sh Certificate Transparency, and Wayback Machine API</p>
    </div>

    <div class="domain-search-section">
      <div class="domain-search-box">
        <input type="text" id="domain-input" placeholder="Enter domain (e.g., google.com)" value="">
        <button id="analyze-btn" onclick="analyzeDomain()">Analyze Domain</button>
      </div>
    </div>

    <div class="domain-results-grid" id="results-grid" style="display: none;">
      <div class="domain-result-card">
        <div class="domain-card-header">🌐 DNS Resolution</div>
        <div class="domain-card-content" id="dns-content">
          <div class="domain-loading">Enter a domain to analyze...</div>
        </div>
      </div>

      <div class="domain-result-card">
        <div class="domain-card-header">🔒 SSL Certificates</div>
        <div class="domain-card-content" id="cert-content">
          <div class="domain-loading">Enter a domain to analyze...</div>
        </div>
      </div>

      <div class="domain-result-card">
        <div class="domain-card-header">📚 Archive History</div>
        <div class="domain-card-content" id="archive-content">
          <div class="domain-loading">Enter a domain to analyze...</div>
        </div>
      </div>

      <div class="domain-result-card">
        <div class="domain-card-header">📊 Domain Summary</div>
        <div class="domain-card-content" id="summary-content">
          <div class="domain-loading">Enter a domain to analyze...</div>
        </div>
      </div>
    </div>
  </div>
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

<!-- Notes & Tools Tab -->
<section id="tools" class="tab-content">
  <div id="notes" class="tools-sub-tab active">
    <h2>Quick Notes</h2>
    <textarea id="notesArea" placeholder="Write your notes here..."></textarea>
    <button class="export-btn" onclick="exportText('notesArea', 'notes.txt')">Export Notes</button>
  </div>

  <div id="sheet" class="tools-sub-tab">
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
  </div>

  <div id="canvas" class="tools-sub-tab">
    <h2>Canvas Drawing Tool</h2>
    <div class="canvas-controls">
      <label>Color: <input type="color" id="colorPicker" value="#000000"></label>
      <label>Size: <input type="range" id="brushSize" min="1" max="50" value="5"></label>
    </div>
    <canvas id="drawCanvas" width="700" height="400"></canvas>
    <div class="canvas-controls">
      <button onclick="clearCanvas()">Clear</button>
      <button onclick="saveImage()">Export PNG</button>
    </div>
  </div>
</section>

  </div> <!-- Close dashboard-content -->
</div> <!-- Close dashboard-app -->

<script>

// ---------------------------------------------------------------------
// Proxy for APIs that don't send CORS headers (MSRC, Shodan CVEDB, crt.sh).
// WORKER: paste your dashboard-proxy Worker origin here (no path) to stop
// relying on the public CorsProxy.io. Leave "" to keep using CorsProxy.io.
// Worker contract: WORKER_URL + "/?url=" + encoded target (same as cybernews).
// ---------------------------------------------------------------------
const DASH_WORKER_URL = "https://dashboard-proxy.cicerodev-343.workers.dev";

function proxied(targetUrl) {
  const w = DASH_WORKER_URL.trim().replace(/\/$/, '');
  return w
    ? `${w}/?url=${encodeURIComponent(targetUrl)}`
    : `https://corsproxy.io/?${encodeURIComponent(targetUrl)}`;
}

// Tab switching logic for primary navigation
document.querySelectorAll('.dashboard-tabs a').forEach(tabLink => {
  tabLink.addEventListener('click', function(e) {
    e.preventDefault();
    
    // Update primary tab styling
    document.querySelectorAll('.dashboard-tabs a').forEach(a => a.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
    this.classList.add('active');
    
    // Show/hide secondary navs
    const cveSecondaryNav = document.getElementById('cve-secondary-nav');
    const toolsSecondaryNav = document.getElementById('tools-secondary-nav');

    if (this.dataset.tab === 'cve') {
      cveSecondaryNav.classList.add('show');
      toolsSecondaryNav.classList.remove('show');
    } else if (this.dataset.tab === 'tools') {
      toolsSecondaryNav.classList.add('show');
      cveSecondaryNav.classList.remove('show');
    } else {
      cveSecondaryNav.classList.remove('show');
      toolsSecondaryNav.classList.remove('show');
    }
    
    // Show the selected tab content
    document.getElementById(this.dataset.tab).classList.add('active');
    
    // Initialize tools when first accessed
    if (this.dataset.tab === 'cve' && !window.cveToolsInitialized) {
      window.cveToolsInitialized = true;
      setTimeout(() => cveHub.init(), 0);
    }
  });
});

// Secondary CVE navigation
document.querySelectorAll('.cve-secondary-nav a').forEach(cveTabLink => {
  cveTabLink.addEventListener('click', function(e) {
    e.preventDefault();
    
    // Update secondary tab styling
    document.querySelectorAll('.cve-secondary-nav a').forEach(a => a.classList.remove('active'));
    document.querySelectorAll('.cve-sub-tab').forEach(c => c.classList.remove('active'));
    this.classList.add('active');
    
    // Show the selected CVE sub-tab
    document.getElementById(this.dataset.cveTab).classList.add('active');
  });
});

// Secondary Tools navigation
document.querySelectorAll('.tools-secondary-nav a').forEach(toolsTabLink => {
  toolsTabLink.addEventListener('click', function(e) {
    e.preventDefault();
    
    // Update secondary tab styling
    document.querySelectorAll('.tools-secondary-nav a').forEach(a => a.classList.remove('active'));
    document.querySelectorAll('.tools-sub-tab').forEach(c => c.classList.remove('active'));
    this.classList.add('active');
    
// Show the selected tools sub-tab
const targetTab = document.getElementById(this.dataset.toolsTab);
if (targetTab) {
  targetTab.classList.add('active');
} else {
  console.error('Target tab not found:', this.dataset.toolsTab);
}
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

  // --- Currency Exchange Script ---
  const targetCurrencies = [
    { code: 'GBP', name: 'British Pound', country: 'gb' },
    { code: 'USD', name: 'US Dollar', country: 'us' },
    { code: 'EUR', name: 'Euro', country: 'eu' },
    { code: 'JPY', name: 'Japanese Yen', country: 'jp' },
    { code: 'AUD', name: 'Australian Dollar', country: 'au' },
    { code: 'CAD', name: 'Canadian Dollar', country: 'ca' },
    { code: 'INR', name: 'Indian Rupee', country: 'in' },
    { code: 'CNY', name: 'Chinese Yuan', country: 'cn' },
    { code: 'CHF', name: 'Swiss Franc', country: 'ch' },
    { code: 'ZAR', name: 'South African Rand', country: 'za' },
    { code: 'SEK', name: 'Swedish Krona', country: 'se' },
    { code: 'NOK', name: 'Norwegian Krone', country: 'no' }
  ];
  
  function formatNumber(num) {
    return new Intl.NumberFormat('en-US', {
      minimumFractionDigits: 2,
      maximumFractionDigits: 4
    }).format(num);
  }
  
  function formatDate(dateString) {
    return new Date(dateString).toLocaleDateString('en-US', {
      month: 'short',
      day: 'numeric',
      year: 'numeric'
    });
  }
  
  async function convertCurrency() {
    const amount = parseFloat(document.getElementById('currencyAmount').value);
    const baseCurrency = document.getElementById('currencyBaseCurrency').value;
    const convertBtn = document.getElementById('currencyConvertBtn');
    const ratesTable = document.getElementById('currencyRatesTable');
    const baseAmount = document.getElementById('currencyBaseAmount');
    const lastUpdated = document.getElementById('currencyLastUpdated');
  
    if (!amount || amount <= 0) {
      alert('Please enter a valid amount');
      return;
    }
  
    // Show loading state
    convertBtn.disabled = true;
    convertBtn.textContent = 'Loading...';
    ratesTable.innerHTML = '<div class="currency-loading">Fetching latest rates...</div>';
  
    try {
      // Get the symbols we want to convert to (excluding the base currency)
      const symbols = targetCurrencies
        .filter(currency => currency.code !== baseCurrency)
        .map(currency => currency.code)
        .join(',');
  
      const response = await fetch(`https://api.frankfurter.dev/v1/latest?base=${baseCurrency}&symbols=${symbols}`);
  
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
  
      const data = await response.json();
  
      // Update header
      baseAmount.textContent = `${formatNumber(amount)} ${baseCurrency} equals:`;
      lastUpdated.textContent = `Updated ${formatDate(data.date)}`;
  
      // Build the rates table - exclude the selected base currency
      let tableHTML = '';
  
      targetCurrencies.forEach(currency => {
        // Skip the base currency since we're showing conversions FROM it
        if (currency.code === baseCurrency) {
          return;
        }
  
        if (data.rates[currency.code]) {
          const rate = data.rates[currency.code];
          const convertedAmount = amount * rate;
          const flagUrl = `https://flagcdn.com/w20/${currency.country}.png`;
  
          tableHTML += `
            <div class="currency-rate-row">
              <img class="currency-flag" src="${flagUrl}" alt="${currency.code} flag" loading="lazy">
              <div class="currency-info">
                <div class="currency-code">${currency.code}</div>
                <div class="currency-name">(${currency.name})</div>
              </div>
              <div class="currency-rate-value">${formatNumber(convertedAmount)}</div>
            </div>
          `;
        }
      });
  
      ratesTable.innerHTML = tableHTML;
  
    } catch (error) {
      console.error('Error fetching exchange rates:', error);
      ratesTable.innerHTML = `<div class="currency-error">Failed to load rates. Please try again.</div>`;
    } finally {
      convertBtn.disabled = false;
      convertBtn.textContent = 'Convert';
    }
  }
  
  // Load default rates on page load
  if (typeof window !== 'undefined') {
    const originalOnLoad = window.onload;
    window.onload = function() {
      if (originalOnLoad) originalOnLoad();
      // Only convert if currency elements exist
      if (document.getElementById('currencyAmount')) {
        convertCurrency();
      }
    };
  }
  
  // Allow Enter key to trigger conversion
  document.addEventListener('DOMContentLoaded', function() {
    const amountInput = document.getElementById('currencyAmount');
    const baseCurrencySelect = document.getElementById('currencyBaseCurrency');
  
    if (amountInput) {
      amountInput.addEventListener('keypress', function(event) {
        if (event.key === 'Enter') {
          convertCurrency();
        }
      });
    }
  
    // Auto-convert when base currency changes
    if (baseCurrencySelect) {
      baseCurrencySelect.addEventListener('change', convertCurrency);
    }
  });  

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
          <p style="color: var(--accent); font-weight: bold; margin-top: 10px;">Click to view full recipe →</p>
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
        document.getElementById('modalIngredients').innerHTML = '<div style="text-align: center; padding: 20px; color: var(--db-crit);">Failed to load recipe details. Please try again.</div>';
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

  // ===================================================================
  // CVE hub — Lookup + GHSA / Patch Tuesday / KEV feeds
  // Every block of data carries a source tag (NVD, CVE.org, CVEDB, EPSS,
  // OSV, GHSA, MSRC, KEV). Sources load independently and fail on their
  // own; nothing is fetched until you search or pick a timeframe.
  // ===================================================================
  const cveHub = (() => {
    const CVE_RE = /^CVE-\d{4}-\d{4,}$/i;
    const workerBase = () => DASH_WORKER_URL.trim().replace(/\/$/, '');

    // ---------- helpers ----------
    const esc = s => String(s == null ? '' : s).replace(/[&<>"']/g, c =>
      ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' })[c]);
    // Inert HTML -> text (DOMParser documents never run scripts or load images)
    const htmlToText = s => s ? (new DOMParser().parseFromString(String(s), 'text/html').body.textContent || '').trim() : '';
    const $ = id => document.getElementById(id);
    const fmtDate = d => {
      if (!d) return '';
      const t = new Date(d);
      return isNaN(t) ? String(d).slice(0, 10) : t.toLocaleDateString('en-GB', { day: 'numeric', month: 'short', year: 'numeric' });
    };
    const isoDay = d => d.toISOString().slice(0, 10);
    const safeUrl = u => /^https?:\/\//i.test(u || '') ? u : '#';
    const link = (u, text) => `<a href="${esc(safeUrl(u))}" target="_blank" rel="noopener">${esc(text || u)}</a>`;
    const pct = x => (x == null || isNaN(x)) ? '–' : (Number(x) * 100).toFixed(Number(x) < 0.1 ? 2 : 1) + '%';

    function sevFromScore(score) {
      const s = Number(score);
      if (isNaN(s)) return '';
      if (s >= 9) return 'CRITICAL';
      if (s >= 7) return 'HIGH';
      if (s >= 4) return 'MEDIUM';
      if (s > 0) return 'LOW';
      return 'NONE';
    }
    function sevBadge(sev, score) {
      const s = String(sev || sevFromScore(score) || '').toUpperCase();
      const cls = { CRITICAL: 'crit', HIGH: 'high', IMPORTANT: 'high', MEDIUM: 'med', MODERATE: 'med', LOW: 'low' }[s] || 'none';
      const label = s ? s.toLowerCase() : 'n/a';
      return `<span class="cvh-sev cvh-sev-${cls}">${esc(label)}${score != null && score !== '' ? ' ' + esc(Number(score).toFixed(1)) : ''}</span>`;
    }

    const SOURCES = {
      nvd:    { label: 'NVD',     title: 'NIST National Vulnerability Database' },
      cveorg: { label: 'CVE.org', title: 'CVE Program record (CNA + CISA ADP)' },
      cvedb:  { label: 'CVEDB',   title: 'Shodan CVEDB' },
      epss:   { label: 'EPSS',    title: 'FIRST Exploit Prediction Scoring System' },
      osv:    { label: 'OSV',     title: 'OSV.dev open source vulnerability database' },
      ghsa:   { label: 'GHSA',    title: 'GitHub Advisory Database' },
      msrc:   { label: 'MSRC',    title: 'Microsoft Security Update Guide' },
      kev:    { label: 'KEV',     title: 'CISA Known Exploited Vulnerabilities catalogue' },
      adp:    { label: 'CISA-ADP', title: 'CISA vulnrichment (ADP container on the CVE record)' },
    };
    const tag = (k, note) => `<span class="cvh-src" title="${esc(SOURCES[k].title)}${note ? ' · ' + esc(note) : ''}">${SOURCES[k].label}</span>`;
    const cveBtn = id => id ? `<button type="button" class="cvh-cvebtn" data-cve="${esc(id)}" title="Look up ${esc(id)}">${esc(id)}</button>` : '';

    // ---------- fetching ----------
    async function getJSON(url, opts = {}) {
      const t0 = performance.now();
      try {
        const r = await fetch(url, {
          signal: AbortSignal.timeout(opts.timeout || 20000),
          headers: opts.accept ? { Accept: opts.accept } : undefined,
        });
        const txt = await r.text();
        let data = null;
        try { data = txt ? JSON.parse(txt) : null; } catch (e) { data = null; }
        return { ok: r.ok && data !== null, status: r.status, data, ms: Math.round(performance.now() - t0), headers: r.headers };
      } catch (e) {
        return { ok: false, status: 0, data: null, ms: Math.round(performance.now() - t0),
                 error: e && e.name === 'TimeoutError' ? 'timed out' : 'network / CORS error' };
      }
    }
    const routeUrl = (via, url) => via === 'worker'
      ? `${workerBase()}/?url=${encodeURIComponent(url)}`
      : `https://corsproxy.io/?${encodeURIComponent(url)}`;
    // For APIs without CORS: Worker first, then the public proxy as a last resort.
    async function getProxied(url, opts) {
      const routes = workerBase() ? ['worker', 'corsproxy'] : ['corsproxy'];
      let last = null;
      const errs = [];
      for (const via of routes) {
        const r = await getJSON(routeUrl(via, url), opts);
        r.via = via;
        if (r.ok || r.status === 404) return r;
        errs.push(`${via}: ${r.error || 'HTTP ' + r.status}`);
        last = r;
      }
      last.error = errs.join(', ');
      return last;
    }
    const why = r => r.error || (r.status ? `HTTP ${r.status}` : 'failed');

    // =================================================================
    // LOOKUP
    // =================================================================
    const L = {
      id: null,
      res: {},          // source key -> { state, ms, data, note }
      openState: {},
    };

    const LOOKUP_SOURCES = ['nvd', 'cveorg', 'cvedb', 'epss', 'osv', 'msrc'];

    const fetchers = {
      async nvd(id) {
        const r = await getJSON(`https://services.nvd.nist.gov/rest/json/cves/2.0?cveId=${id}`);
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) + (r.status === 403 ? ' (NVD rate limit: wait 30s)' : '') };
        const cve = r.data.vulnerabilities && r.data.vulnerabilities[0] && r.data.vulnerabilities[0].cve;
        return cve ? { state: 'ok', ms: r.ms, data: cve } : { state: 'none', ms: r.ms };
      },
      async cveorg(id) {
        const r = await getJSON(`https://cveawg.mitre.org/api/cve/${id}`);
        if (r.status === 404) return { state: 'none', ms: r.ms };
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) };
        return { state: 'ok', ms: r.ms, data: r.data };
      },
      async cvedb(id) {
        const r = await getProxied(`https://cvedb.shodan.io/cve/${id}`);
        if (r.status === 404) return { state: 'none', ms: r.ms, note: 'via ' + r.via };
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) };
        return { state: 'ok', ms: r.ms, data: r.data, note: 'via ' + r.via };
      },
      async epss(id) {
        const r = await getJSON(`https://api.first.org/data/v1/epss?cve=${id}`);
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) };
        const row = r.data.data && r.data.data[0];
        return row ? { state: 'ok', ms: r.ms, data: row } : { state: 'none', ms: r.ms };
      },
      async osv(id) {
        const r = await getJSON(`https://api.osv.dev/v1/vulns/${id}`);
        if (r.status === 404) return { state: 'none', ms: r.ms };
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) };
        const ghsaIds = [...new Set([...(r.data.aliases || []), ...(r.data.related || [])])]
          .filter(x => /^GHSA-/i.test(x)).slice(0, 4);
        const ghsa = (await Promise.all(ghsaIds.map(g => getJSON(`https://api.osv.dev/v1/vulns/${g}`))))
          .filter(x => x.ok).map(x => x.data);
        return { state: 'ok', ms: r.ms, data: { cve: r.data, ghsa } };
      },
      async msrc(id) {
        const q = encodeURIComponent(`cveNumber eq '${id}'`);
        const r = await getProxied(`https://api.msrc.microsoft.com/sug/v2.0/en-US/vulnerability?$filter=${q}`);
        if (!r.ok) return { state: 'fail', ms: r.ms, note: why(r) };
        const v = r.data.value && r.data.value[0];
        if (!v) return { state: 'none', ms: r.ms, note: 'not a Microsoft CVE' };
        const ap = await getProxied(`https://api.msrc.microsoft.com/sug/v2.0/en-US/affectedProduct?$filter=${q}`);
        return { state: 'ok', ms: r.ms, data: { vuln: v, products: ap.ok ? (ap.data.value || []) : null }, note: 'via ' + r.via };
      },
    };

    function runSource(key, id) {
      L.res[key] = { state: 'loading' };
      renderStatus();
      fetchers[key](id).then(out => {
        if (L.id !== id) return; // a newer lookup started
        L.res[key] = out;
        renderStatus();
        renderLookup();
      }).catch(err => {
        if (L.id !== id) return;
        L.res[key] = { state: 'fail', note: String(err && err.message || err) };
        renderStatus();
        renderLookup();
      });
    }

    function startLookup(rawQuery) {
      const q = String(rawQuery || '').trim();
      if (!q) return;
      $('cvh-q').value = q;
      if (CVE_RE.test(q)) {
        const id = q.toUpperCase();
        L.id = id; L.res = {}; L.openState = {};
        try { history.replaceState(null, '', '#cve=' + id); } catch (e) {}
        $('cvh-result').innerHTML = '';
        LOOKUP_SOURCES.forEach(k => runSource(k, id));
        renderLookup();
      } else {
        L.id = null; L.res = {};
        $('cvh-status').innerHTML = '';
        keywordSearch(q, 0);
      }
    }

    function renderStatus() {
      if (!L.id) return;
      $('cvh-status').innerHTML = LOOKUP_SOURCES.map(k => {
        const r = L.res[k] || { state: 'loading' };
        const icon = { loading: '…', ok: '✓', none: '–', fail: '✗' }[r.state];
        const detail = r.state === 'loading' ? 'loading'
          : r.state === 'ok' ? `${r.ms} ms${r.note ? ' · ' + r.note : ''}`
          : r.state === 'none' ? (r.note || 'no record')
          : (r.note || 'failed') + ' — click to retry';
        return `<button type="button" class="cvh-chip cvh-chip-${r.state}" data-src="${k}" title="${esc(SOURCES[k].title)}: ${esc(detail)}"
                 ${r.state === 'fail' ? '' : 'tabindex="-1"'}>${icon} ${SOURCES[k].label}${r.state === 'fail' ? ' <small>' + esc(r.note || '') + '</small>' : ''}</button>`;
      }).join('');
    }

    // Pull the pieces we want out of each source into one model.
    function buildModel() {
      const d = k => L.res[k] && L.res[k].state === 'ok' ? L.res[k].data : null;
      const nvd = d('nvd'), rec = d('cveorg'), db = d('cvedb'), ep = d('epss'), osv = d('osv'), ms = d('msrc');
      const cna = rec && rec.containers && rec.containers.cna;
      const adp = rec && rec.containers && (rec.containers.adp || []).find(a => a.providerMetadata && /CISA-ADP/i.test(a.providerMetadata.shortName));
      const m = { scores: [], cwes: [], refs: [] };

      // Title / description
      const en = arr => (arr || []).find(x => (x.lang || '').startsWith('en'));
      m.title = (nvd && nvd.cisaVulnerabilityName) || (ms && ms.vuln.cveTitle) || (cna && cna.title) || '';
      m.titleSrc = nvd && nvd.cisaVulnerabilityName ? 'nvd' : ms && ms.vuln.cveTitle ? 'msrc' : cna && cna.title ? 'cveorg' : null;
      if (nvd && en(nvd.descriptions)) { m.desc = en(nvd.descriptions).value; m.descSrc = 'nvd'; }
      else if (cna && en(cna.descriptions)) { m.desc = en(cna.descriptions).value; m.descSrc = 'cveorg'; }
      else if (db && db.summary) { m.desc = db.summary; m.descSrc = 'cvedb'; }
      else if (ms && ms.vuln.description) { m.desc = htmlToText(ms.vuln.description); m.descSrc = 'msrc'; }

      // Dates / status
      m.published = (nvd && nvd.published) || (rec && rec.cveMetadata && rec.cveMetadata.datePublished) || (db && db.published_time);
      m.modified = (nvd && nvd.lastModified) || (rec && rec.cveMetadata && rec.cveMetadata.dateUpdated);
      m.nvdStatus = nvd && nvd.vulnStatus;
      m.state = rec && rec.cveMetadata && rec.cveMetadata.state;
      m.assigner = (rec && rec.cveMetadata && rec.cveMetadata.assignerShortName) || (ms && ms.vuln.issuingCna);

      // CVSS from everywhere
      if (nvd && nvd.metrics) {
        [['cvssMetricV40', '4.0'], ['cvssMetricV31', '3.1'], ['cvssMetricV30', '3.0'], ['cvssMetricV2', '2.0']].forEach(([key, ver]) => {
          (nvd.metrics[key] || []).forEach(x => m.scores.push({
            src: 'nvd', who: x.source === 'nvd@nist.gov' ? 'NIST' : (x.type === 'Primary' ? 'NVD primary' : 'CNA via NVD'),
            primary: x.type === 'Primary', version: ver, score: x.cvssData.baseScore,
            sev: x.cvssData.baseSeverity || x.baseSeverity, vector: x.cvssData.vectorString,
          }));
        });
      }
      const fromCveJson = (metrics, src, who) => (metrics || []).forEach(x => {
        [['cvssV4_0', '4.0'], ['cvssV3_1', '3.1'], ['cvssV3_0', '3.0'], ['cvssV2_0', '2.0']].forEach(([key, ver]) => {
          if (x[key]) m.scores.push({ src, who, version: ver, score: x[key].baseScore, sev: x[key].baseSeverity, vector: x[key].vectorString });
        });
      });
      if (cna) fromCveJson(cna.metrics, 'cveorg', 'CNA' + (m.assigner ? ' (' + m.assigner + ')' : ''));
      if (adp) fromCveJson(adp.metrics, 'adp', 'CISA-ADP');
      if (ms && ms.vuln.baseScore) m.scores.push({ src: 'msrc', who: 'Microsoft', version: (String(ms.vuln.vectorString || '').match(/CVSS:([\d.]+)/) || [])[1] || '3.1',
        score: Number(ms.vuln.baseScore), sev: '', vector: ms.vuln.vectorString });
      if (db && db.cvss != null) m.scores.push({ src: 'cvedb', who: 'CVEDB', version: String(db.cvss_version || ''), score: db.cvss, sev: '', vector: '' });

      // Headline score: NIST/primary v4 or v3 > CNA > ADP > MSRC > CVEDB > anything v2
      const rank = s => (s.version.startsWith('2') ? 100 : 0) +
        ({ nvd: s.primary ? 0 : 3, cveorg: 1, adp: 2, msrc: 4, cvedb: 5 }[s.src]) * 10 + (s.version === '4.0' ? 0 : 1);
      m.headline = [...m.scores].sort((a, b) => rank(a) - rank(b))[0] || null;

      // EPSS
      if (ep) m.epss = { p: Number(ep.epss), pct: Number(ep.percentile), date: ep.date, src: 'epss' };
      else if (db && db.epss != null) m.epss = { p: db.epss, pct: db.ranking_epss, src: 'cvedb' };

      // KEV
      if (nvd && nvd.cisaExploitAdd) m.kev = { added: nvd.cisaExploitAdd, due: nvd.cisaActionDue, action: nvd.cisaRequiredAction, name: nvd.cisaVulnerabilityName, src: 'nvd' };
      else if (db && db.kev) m.kev = { src: 'cvedb' };
      const adpKev = adp && (adp.metrics || []).map(x => x.other).find(o => o && o.type === 'kev');
      if (!m.kev && adpKev) m.kev = { added: adpKev.content && adpKev.content.dateAdded, src: 'adp' };
      if (m.kev && db && db.ransomware_campaign) m.kev.ransomware = db.ransomware_campaign;
      m.kevChecked = Boolean(nvd || db || adp);

      // SSVC (CISA)
      const ssvc = adp && (adp.metrics || []).map(x => x.other).find(o => o && o.type === 'ssvc');
      if (ssvc && ssvc.content && ssvc.content.options) {
        m.ssvc = ssvc.content.options.map(o => Object.entries(o)[0]).filter(Boolean);
      }

      // Microsoft
      if (ms) m.ms = ms;

      // CWE
      const cweSet = new Map();
      (nvd && nvd.weaknesses || []).forEach(w => (w.description || []).forEach(x => { if (/^CWE-\d+/.test(x.value)) cweSet.set(x.value, 'nvd'); }));
      (cna && cna.problemTypes || []).forEach(p => (p.descriptions || []).forEach(x => {
        const id = x.cweId || (String(x.description).match(/CWE-\d+/) || [])[0];
        if (id && !cweSet.has(id)) cweSet.set(id, 'cveorg');
      }));
      m.cwes = [...cweSet.entries()];

      // Packages (GHSA records via OSV)
      m.packages = [];
      if (osv) osv.ghsa.forEach(g => (g.affected || []).forEach(a => {
        const ev = (a.ranges || []).flatMap(r => r.events || []);
        const intro = ev.filter(e => e.introduced != null).map(e => e.introduced);
        const fixed = ev.filter(e => e.fixed != null).map(e => e.fixed);
        const last = ev.filter(e => e.last_affected != null).map(e => e.last_affected);
        m.packages.push({
          ghsa: g.id, eco: a.package && a.package.ecosystem, name: a.package && a.package.name,
          range: intro.map((v, i) => `${v === '0' ? 'all' : '≥ ' + v}${fixed[i] ? ' < ' + fixed[i] : last[i] ? ' ≤ ' + last[i] : ''}`).join(', '),
          fixed: fixed.join(', '), reviewed: g.database_specific && g.database_specific.github_reviewed,
        });
      }));
      m.ghsaIds = osv ? osv.ghsa.map(g => g.id) : [];

      // Products (CPE) — NVD configurations, else CVEDB
      const prod = new Map();
      const addCpe = (c, src) => {
        const p = String(c).split(':');
        if (p.length > 4) { const key = `${p[3]}:${p[4]}`; if (!prod.has(key)) prod.set(key, src); }
      };
      (nvd && nvd.configurations || []).forEach(cfg => (cfg.nodes || []).forEach(n => (n.cpeMatch || []).forEach(c => c.vulnerable && addCpe(c.criteria, 'nvd'))));
      if (!prod.size && db && db.cpes) db.cpes.forEach(c => addCpe(c, 'cvedb'));
      m.products = [...prod.entries()];
      m.cpeCount = db && db.cpes ? db.cpes.length : null;

      // References
      if (nvd && nvd.references) m.refs = nvd.references.map(r => ({ url: r.url, tags: r.tags || [], src: 'nvd' }));
      else if (cna && cna.references) m.refs = cna.references.map(r => ({ url: r.url, tags: r.tags || [], src: 'cveorg' }));
      else if (db && db.references) m.refs = db.references.map(u => ({ url: u, tags: [], src: 'cvedb' }));

      return m;
    }

    function section(key, title, tags, body, open = true) {
      const isOpen = key in L.openState ? L.openState[key] : open;
      return `<details class="cvh-sec" data-key="${key}" ${isOpen ? 'open' : ''}>
        <summary><span>${title}</span><span class="cvh-tags">${tags}</span></summary>
        <div class="cvh-sec-body">${body}</div></details>`;
    }

    function renderLookup() {
      const id = L.id;
      if (!id) return;
      // remember which sections are open before re-rendering
      document.querySelectorAll('#cvh-result details.cvh-sec').forEach(el => { L.openState[el.dataset.key] = el.open; });

      const m = buildModel();
      const pending = LOOKUP_SOURCES.filter(k => !L.res[k] || L.res[k].state === 'loading').length;
      const anyData = LOOKUP_SOURCES.some(k => L.res[k] && L.res[k].state === 'ok');

      if (!anyData) {
        $('cvh-result').innerHTML = pending
          ? `<div class="cvh-empty"><span class="cvh-spin"></span> looking up ${esc(id)}…</div>`
          : `<div class="cvh-empty">No source has a record for <strong>${esc(id)}</strong>. It may be reserved, rejected or brand new.</div>`;
        return;
      }

      const h = m.headline;
      const tiles = [];
      tiles.push(`<div class="cvh-tile"><div class="cvh-tile-label">CVSS ${h ? esc(h.version) : ''} ${h ? tag(h.src, h.who) : ''}</div>
        <div class="cvh-tile-val">${h ? sevBadge(h.sev, h.score) : '<span class="cvh-dim">not scored yet</span>'}</div>
        <div class="cvh-tile-sub">${h ? esc(h.who) : (m.nvdStatus ? 'NVD: ' + esc(m.nvdStatus) : '')}</div></div>`);
      tiles.push(`<div class="cvh-tile"><div class="cvh-tile-label">EPSS ${m.epss ? tag(m.epss.src) : ''}</div>
        <div class="cvh-tile-val ${m.epss && m.epss.p >= 0.1 ? 'cvh-hot' : ''}">${m.epss ? pct(m.epss.p) : '–'}</div>
        <div class="cvh-tile-sub">${m.epss && m.epss.pct != null ? 'percentile ' + pct(m.epss.pct) : 'exploit probability (30 days)'}</div></div>`);
      tiles.push(`<div class="cvh-tile"><div class="cvh-tile-label">CISA KEV ${m.kev ? tag(m.kev.src === 'adp' ? 'adp' : m.kev.src) : ''}</div>
        <div class="cvh-tile-val ${m.kev ? 'cvh-hot' : ''}">${m.kev ? 'listed' : m.kevChecked ? 'not listed' : '–'}</div>
        <div class="cvh-tile-sub">${m.kev && m.kev.added ? 'added ' + esc(fmtDate(m.kev.added)) : m.kev ? 'known exploited' : ''}${m.kev && m.kev.ransomware === 'Known' ? ' · <span class="cvh-flag">ransomware</span>' : ''}</div></div>`);
      if (m.ms) tiles.push(`<div class="cvh-tile"><div class="cvh-tile-label">Microsoft ${tag('msrc')}</div>
        <div class="cvh-tile-val ${m.ms.vuln.exploited === 'Yes' ? 'cvh-hot' : ''}">${m.ms.vuln.exploited === 'Yes' ? 'exploited' : esc((m.ms.vuln.severity || '').toLowerCase() || '–')}</div>
        <div class="cvh-tile-sub">${[m.ms.vuln.impact, m.ms.vuln.publiclyDisclosed === 'Yes' ? 'publicly disclosed' : ''].filter(Boolean).map(esc).join(' · ')}</div></div>`);
      else if (m.ssvc) tiles.push(`<div class="cvh-tile"><div class="cvh-tile-label">SSVC ${tag('adp')}</div>
        <div class="cvh-tile-val">${esc((m.ssvc.find(x => x[0] === 'Exploitation') || [, '–'])[1])}</div>
        <div class="cvh-tile-sub">exploitation · ${esc(m.ssvc.filter(x => x[0] !== 'Exploitation').map(x => x[0].toLowerCase() + ': ' + x[1]).join(' · '))}</div></div>`);

      let html = `<div class="cvh-card">
        <div class="cvh-card-head">
          <div class="cvh-id">${esc(id)}</div>
          <div class="cvh-quicklinks">
            ${link('https://nvd.nist.gov/vuln/detail/' + id, 'NVD')}
            ${link('https://www.cve.org/CVERecord?id=' + id, 'CVE.org')}
            ${m.ghsaIds.map(g => link('https://github.com/advisories/' + g, g.slice(0, 9) + '…')).join(' ')}
            ${m.ms ? link('https://msrc.microsoft.com/update-guide/vulnerability/' + id, 'MSRC') : ''}
          </div>
        </div>
        ${m.title ? `<div class="cvh-title">${esc(m.title)} ${tag(m.titleSrc)}</div>` : ''}
        <div class="cvh-meta">
          ${m.published ? `<span>published ${esc(fmtDate(m.published))}</span>` : ''}
          ${m.modified ? `<span>updated ${esc(fmtDate(m.modified))}</span>` : ''}
          ${m.assigner ? `<span>CNA: ${esc(m.assigner)}</span>` : ''}
          ${m.nvdStatus ? `<span title="NVD analysis status">NVD: ${esc(m.nvdStatus)}</span>` : ''}
          ${m.state && m.state !== 'PUBLISHED' ? `<span class="cvh-flag">${esc(m.state)}</span>` : ''}
        </div>
        <div class="cvh-tiles">${tiles.join('')}</div>
        ${pending ? `<div class="cvh-dim cvh-small"><span class="cvh-spin"></span> waiting on ${pending} more source${pending > 1 ? 's' : ''}…</div>` : ''}
      </div>`;

      if (m.desc) html += section('desc', 'Description', tag(m.descSrc),
        `<p class="cvh-desc">${esc(m.desc)}</p>` +
        (m.cwes.length ? `<div class="cvh-cwes">${m.cwes.map(([c, s]) => link('https://cwe.mitre.org/data/definitions/' + c.replace('CWE-', '') + '.html', c)).join(' ')}</div>` : ''));

      if (m.kev && (m.kev.action || m.kev.due)) html += section('kev', 'CISA KEV entry', tag(m.kev.src),
        `<dl class="cvh-dl">
          ${m.kev.name ? `<dt>Name</dt><dd>${esc(m.kev.name)}</dd>` : ''}
          ${m.kev.added ? `<dt>Added</dt><dd>${esc(fmtDate(m.kev.added))}</dd>` : ''}
          ${m.kev.due ? `<dt>Fed. due date</dt><dd>${esc(fmtDate(m.kev.due))}</dd>` : ''}
          ${m.kev.action ? `<dt>Required action</dt><dd>${esc(m.kev.action)}</dd>` : ''}
          ${m.kev.ransomware ? `<dt>Ransomware use</dt><dd>${esc(m.kev.ransomware)} ${tag('cvedb')}</dd>` : ''}
        </dl>`);

      if (m.scores.length) html += section('scores', `Scores <span class="cvh-count">${m.scores.length}</span>`,
        [...new Set(m.scores.map(s => s.src))].map(s => tag(s)).join(''),
        `<div class="cvh-table-wrap"><table class="cvh-table"><thead><tr><th>source</th><th>ver</th><th>score</th><th>vector</th></tr></thead><tbody>
          ${m.scores.map(s => `<tr><td>${tag(s.src)} <span class="cvh-dim">${esc(s.who)}</span></td><td>${esc(s.version)}</td>
            <td>${sevBadge(s.sev, s.score)}</td><td class="cvh-vector">${esc(s.vector || '')}</td></tr>`).join('')}
        </tbody></table></div>` +
        (m.ssvc ? `<div class="cvh-small">SSVC ${tag('adp')} ${m.ssvc.map(x => `<span class="cvh-pill">${esc(x[0])}: ${esc(x[1])}</span>`).join(' ')}</div>` : '') +
        (m.epss ? `<div class="cvh-small">EPSS ${tag(m.epss.src)} ${pct(m.epss.p)} chance of exploitation in the next 30 days${m.epss.pct != null ? ', higher than ' + pct(m.epss.pct) + ' of all CVEs' : ''}${m.epss.date ? ' (model date ' + esc(m.epss.date) + ')' : ''}.</div>` : ''));

      if (m.packages.length) html += section('pkgs', `Affected packages <span class="cvh-count">${m.packages.length}</span>`, tag('ghsa', 'via OSV.dev') + tag('osv'),
        `<div class="cvh-table-wrap"><table class="cvh-table"><thead><tr><th>package</th><th>affected</th><th>fixed in</th><th>advisory</th></tr></thead><tbody>
          ${m.packages.slice(0, 40).map(p => `<tr><td><span class="cvh-eco">${esc(p.eco)}</span> ${esc(p.name)}</td><td>${esc(p.range)}</td>
            <td>${p.fixed ? esc(p.fixed) : '<span class="cvh-flag">no fix</span>'}</td><td>${link('https://github.com/advisories/' + p.ghsa, p.ghsa)}</td></tr>`).join('')}
        </tbody></table></div>`);

      if (m.ms) {
        const v = m.ms.vuln, prods = m.ms.products || [];
        const kbs = new Map();
        prods.forEach(p => (p.kbArticles || []).forEach(k => { if (k.articleName && !kbs.has(k.articleName)) kbs.set(k.articleName, k.articleUrl || ('https://support.microsoft.com/help/' + k.articleName)); }));
        const fams = [...new Set(prods.map(p => p.product))];
        html += section('ms', 'Microsoft', tag('msrc'),
          `<dl class="cvh-dl">
            <dt>Title</dt><dd>${esc(v.cveTitle)}</dd>
            <dt>Severity</dt><dd>${sevBadge(v.severity)} ${esc(v.impact || '')}</dd>
            <dt>Exploited</dt><dd>${v.exploited === 'Yes' ? '<span class="cvh-flag">yes</span>' : esc(v.exploited || '–')} · publicly disclosed: ${esc(v.publiclyDisclosed || '–')}</dd>
            <dt>Released</dt><dd>${esc(v.releaseNumber || '')} (${esc(fmtDate(v.releaseDate))})</dd>
            ${v.tag ? `<dt>Component</dt><dd>${esc(v.tag)}</dd>` : ''}
            ${fams.length ? `<dt>Products <span class="cvh-count">${fams.length}</span></dt><dd>${fams.slice(0, 12).map(esc).join(' · ')}${fams.length > 12 ? ` <span class="cvh-dim">+${fams.length - 12} more</span>` : ''}</dd>` : ''}
            ${kbs.size ? `<dt>Updates</dt><dd>${[...kbs.entries()].slice(0, 15).map(([n, u]) => link(u, /^\d+$/.test(n) ? 'KB' + n : n)).join(' · ')}</dd>` : ''}
          </dl>
          ${(v.articles || []).filter(a => a.articleType === 'FAQ').slice(0, 3).map(a => `<p class="cvh-small">${esc(htmlToText(a.description)).slice(0, 600)}</p>`).join('')}`,
          true);
      }

      if (m.products.length) html += section('prods', `Affected products (CPE) <span class="cvh-count">${m.products.length}</span>`,
        [...new Set(m.products.map(p => p[1]))].map(s => tag(s)).join(''),
        `<div class="cvh-pills">${m.products.slice(0, 30).map(([p]) => `<span class="cvh-pill">${esc(p.replace(':', ' · '))}</span>`).join('')}
          ${m.products.length > 30 ? `<span class="cvh-dim">+${m.products.length - 30} more</span>` : ''}</div>
          ${m.cpeCount ? `<div class="cvh-small cvh-dim">${m.cpeCount} CPE strings in CVEDB</div>` : ''}`, false);

      if (m.refs.length) {
        const pri = r => (r.tags.includes('Patch') || r.tags.includes('Vendor Advisory') ? 0 : r.tags.includes('Exploit') ? 1 : 2);
        const refs = [...m.refs].sort((a, b) => pri(a) - pri(b));
        html += section('refs', `References <span class="cvh-count">${refs.length}</span>`, tag(refs[0].src),
          `<ul class="cvh-refs">${refs.slice(0, 25).map(r => `<li>${r.tags.slice(0, 3).map(t => `<span class="cvh-pill">${esc(t)}</span>`).join('')} ${link(r.url)}</li>`).join('')}</ul>
           ${refs.length > 25 ? `<div class="cvh-small cvh-dim">+${refs.length - 25} more on ${link('https://nvd.nist.gov/vuln/detail/' + id, 'NVD')}</div>` : ''}`, false);
      }

      $('cvh-result').innerHTML = html;
    }

    // ---------- keyword / product search ----------
    const K = { q: '', mode: 'nvd', start: 0, total: 0, sev: '' };

    async function keywordSearch(q, offset) {
      K.q = q; K.mode = $('cvh-mode').value;
      try { history.replaceState(null, '', location.pathname + location.search); } catch (e) {}
      const out = $('cvh-result');
      out.innerHTML = `<div class="cvh-empty"><span class="cvh-spin"></span> searching ${K.mode === 'nvd' ? 'NVD' : 'CVEDB'} for “${esc(q)}”…</div>`;
      let rows = [], note = '', src = K.mode === 'nvd' ? 'nvd' : 'cvedb', more = false, total = 0;

      if (K.mode === 'nvd') {
        // NVD returns oldest first: read the total, then jump to the newest page.
        const base = `https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=${encodeURIComponent(q)}${K.sev ? '&cvssV3Severity=' + K.sev : ''}`;
        if (offset === 0) {
          const head = await getJSON(base + '&resultsPerPage=1');
          if (!head.ok) { out.innerHTML = errBox('NVD', head, 'NVD allows ~5 requests per 30 seconds without an API key.'); return; }
          K.total = head.data.totalResults || 0;
        }
        total = K.total;
        const start = Math.max(0, total - 20 - offset);
        const count = Math.min(20, total - offset);
        if (count <= 0) { out.innerHTML = `<div class="cvh-empty">No NVD results for “${esc(q)}”.</div>`; return; }
        const r = await getJSON(`${base}&resultsPerPage=${count}&startIndex=${start}`);
        if (!r.ok) { out.innerHTML = errBox('NVD', r, 'NVD allows ~5 requests per 30 seconds without an API key.'); return; }
        rows = (r.data.vulnerabilities || []).map(v => v.cve).reverse().map(c => {
          const met = c.metrics || {};
          const best = (met.cvssMetricV40 || met.cvssMetricV31 || met.cvssMetricV30 || met.cvssMetricV2 || [])[0];
          return { id: c.id, date: c.published, desc: ((c.descriptions || []).find(x => x.lang === 'en') || {}).value,
                   score: best && best.cvssData.baseScore, sev: best && (best.cvssData.baseSeverity || best.baseSeverity),
                   kev: Boolean(c.cisaExploitAdd), status: c.vulnStatus };
        });
        more = offset + 20 < total;
        note = `${total.toLocaleString()} matches · newest first`;
      } else {
        const r = await getProxied(`https://cvedb.shodan.io/cves?product=${encodeURIComponent(q.toLowerCase())}&sort_by_epss=true&limit=20&skip=${offset}`);
        if (!r.ok) { out.innerHTML = errBox('CVEDB', r, 'CVEDB product search needs an exact product name, e.g. "openssl", "exchange_server", "fortios".'); return; }
        rows = (r.data.cves || []).map(c => ({ id: c.cve_id, date: c.published_time, desc: c.summary, score: c.cvss, sev: '', epss: c.epss, kev: c.kev }));
        more = rows.length === 20;
        note = 'sorted by EPSS (most likely to be exploited first)';
        if (!rows.length) { out.innerHTML = `<div class="cvh-empty">CVEDB has no product called “${esc(q)}”. Try the vendor's product id, e.g. <em>exchange_server</em>, <em>fortios</em>, <em>log4j</em>.</div>`; return; }
      }

      K.start = offset;
      out.innerHTML = `<div class="cvh-listhead"><span>${esc(note)} ${tag(src)}</span>
          ${K.mode === 'nvd' ? `<select id="cvh-sev" title="Filter by CVSS v3 severity">
            ${['', 'CRITICAL', 'HIGH', 'MEDIUM', 'LOW'].map(s => `<option value="${s}" ${K.sev === s ? 'selected' : ''}>${s ? s.toLowerCase() : 'all severities'}</option>`).join('')}
          </select>` : ''}</div>
        <div class="cvh-list">${rows.map(r => `<div class="cvh-row">
            <div class="cvh-row-top">${cveBtn(r.id)} ${sevBadge(r.sev, r.score)}
              ${r.epss != null ? `<span class="cvh-pill" title="EPSS">EPSS ${pct(r.epss)}</span>` : ''}
              ${r.kev ? '<span class="cvh-flag">KEV</span>' : ''}
              <span class="cvh-date">${esc(fmtDate(r.date))}</span></div>
            <div class="cvh-row-desc">${esc(r.desc || '')}</div>
          </div>`).join('')}</div>
        <div class="cvh-pager">
          <button type="button" data-kw="${offset - 20}" ${offset === 0 ? 'disabled' : ''}>← newer</button>
          <span class="cvh-dim">${offset + 1}–${offset + rows.length}${total ? ' of ' + total.toLocaleString() : ''}</span>
          <button type="button" data-kw="${offset + 20}" ${more ? '' : 'disabled'}>older →</button>
        </div>`;
      const sevSel = $('cvh-sev');
      if (sevSel) sevSel.onchange = () => { K.sev = sevSel.value; keywordSearch(K.q, 0); };
    }

    function errBox(name, r, hint) {
      return `<div class="cvh-error">${esc(name)} request failed (${esc(why(r))}${r.via ? ', via ' + esc(r.via) : ''}).${hint ? '<br><span class="cvh-small">' + esc(hint) + '</span>' : ''}</div>`;
    }

    // =================================================================
    // GHSA FEED
    // =================================================================
    const G = { days: 0, items: [], day: null, route: 'direct', remaining: null, capped: false, loading: false };
    const GHSA_MAX_PAGES = 5;

    async function ghsaFetch(url) {
      // Try the visitor's own GitHub quota first; fall back to the Worker on rate limits.
      if (G.route === 'direct') {
        const r = await getJSON(url, { accept: 'application/vnd.github+json' });
        if (r.ok) { r.via = 'direct'; return r; }
        if (!(r.status === 403 || r.status === 429 || r.status === 0) || !workerBase()) { r.via = 'direct'; return r; }
        G.route = 'worker';
      }
      const r = await getJSON(routeUrl('worker', url), { accept: 'application/vnd.github+json' });
      r.via = 'worker';
      return r;
    }

    async function ghsaLoad(days) {
      if (G.loading) return;
      G.loading = true; G.days = days; G.day = null; G.items = []; G.capped = false;
      setActive('cvh-ghsa-range', days);
      const list = $('cvh-ghsa-list');
      list.innerHTML = `<div class="cvh-empty"><span class="cvh-spin"></span> fetching advisories…</div>`;
      const today = new Date();
      const since = new Date(today.getTime() - days * 864e5);
      const sev = $('cvh-ghsa-sev').value, eco = $('cvh-ghsa-eco').value, type = $('cvh-ghsa-type').value;
      let url = `https://api.github.com/advisories?type=${type}&published=${isoDay(since)}..${isoDay(today)}&sort=published&direction=desc&per_page=100`
        + (sev ? `&severity=${sev}` : '') + (eco ? `&ecosystem=${eco}` : '');
      let pages = 0, last = null;
      while (url && pages < GHSA_MAX_PAGES) {
        const r = await ghsaFetch(url);
        last = r; pages++;
        if (!r.ok) break;
        G.items.push(...r.data);
        G.remaining = r.headers && r.headers.get('X-RateLimit-Remaining');
        const linkHdr = r.headers && r.headers.get('Link');
        const next = linkHdr && (linkHdr.match(/<([^>]+)>;\s*rel="next"/) || [])[1];
        url = next || null;
      }
      G.capped = Boolean(url);
      G.loading = false;
      if (!G.items.length && last && !last.ok) {
        list.innerHTML = errBox('GitHub', last, last.status === 403
          ? 'GitHub allows 60 anonymous requests an hour per IP. Add a GITHUB_TOKEN secret to the Worker to lift this.' : '');
        $('cvh-ghsa-stats').innerHTML = '';
        return;
      }
      ghsaRender();
    }

    function ghsaRender() {
      const q = $('cvh-ghsa-filter').value.trim().toLowerCase();
      let items = G.items;
      if (q) items = items.filter(a => [a.ghsa_id, a.cve_id, a.summary, ...(a.vulnerabilities || []).map(v => v.package && v.package.name)]
        .some(x => String(x || '').toLowerCase().includes(q)));
      // per-day histogram (UTC days in the window)
      const byDay = new Map();
      for (let i = G.days - 1; i >= 0; i--) byDay.set(isoDay(new Date(Date.now() - i * 864e5)), []);
      items.forEach(a => { const d = (a.published_at || '').slice(0, 10); if (!byDay.has(d)) byDay.set(d, []); byDay.get(d).push(a); });
      const max = Math.max(1, ...[...byDay.values()].map(v => v.length));
      const shown = G.day ? (byDay.get(G.day) || []) : items;
      const count = s => items.filter(a => a.severity === s).length;

      $('cvh-ghsa-stats').innerHTML = `
        <div class="cvh-tiles cvh-tiles-sm">
          <div class="cvh-tile"><div class="cvh-tile-label">advisories ${tag('ghsa')}</div><div class="cvh-tile-val">${items.length}${G.capped ? '+' : ''}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">critical</div><div class="cvh-tile-val cvh-c-crit">${count('critical')}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">high</div><div class="cvh-tile-val cvh-c-high">${count('high')}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">with CVE</div><div class="cvh-tile-val">${items.filter(a => a.cve_id).length}</div></div>
        </div>
        <div class="cvh-hist" title="Advisories per day — tap a bar to filter">
          ${[...byDay.entries()].sort().map(([d, v]) => `<button type="button" class="cvh-bar ${G.day === d ? 'active' : ''}" data-day="${esc(d)}" title="${esc(d)}: ${v.length}">
            <span style="height:${Math.round(v.length / max * 100)}%"></span><em>${esc(d.slice(8))}</em></button>`).join('')}
        </div>
        <div class="cvh-small cvh-dim">via GitHub API (${esc(G.route === 'worker' ? 'Worker' : 'direct')})${G.remaining != null ? ' · ' + esc(G.remaining) + ' requests left this hour' : ''}${G.capped ? ` · showing the newest ${G.items.length} — narrow with severity / ecosystem for more` : ''}${G.day ? ` · filtered to ${esc(G.day)} <button type="button" class="cvh-link" data-day="">clear</button>` : ''}</div>`;

      if (!shown.length) { $('cvh-ghsa-list').innerHTML = `<div class="cvh-empty">No advisories match.</div>`; return; }
      $('cvh-ghsa-list').innerHTML = shown.slice(0, 300).map(a => {
        const pk = (a.vulnerabilities || []).filter(v => v.package);
        const cvss = a.cvss_severities ? (a.cvss_severities.cvss_v4 && a.cvss_severities.cvss_v4.score ? a.cvss_severities.cvss_v4 : a.cvss_severities.cvss_v3) : a.cvss;
        const ep = (a.epss || [])[0];
        return `<details class="cvh-item">
          <summary>
            <div class="cvh-row-top">${sevBadge(a.severity, cvss && cvss.score ? cvss.score : null)} ${cveBtn(a.cve_id)}
              <span class="cvh-dim cvh-mono-sm">${esc(a.ghsa_id)}</span><span class="cvh-date">${esc(fmtDate(a.published_at))}</span></div>
            <div class="cvh-row-title">${esc(a.summary)}</div>
            <div class="cvh-pkgs">${pk.slice(0, 4).map(v => `<span class="cvh-pill"><span class="cvh-eco">${esc(v.package.ecosystem)}</span> ${esc(v.package.name)}</span>`).join('')}${pk.length > 4 ? `<span class="cvh-dim">+${pk.length - 4}</span>` : ''}</div>
          </summary>
          <div class="cvh-item-body">
            ${pk.length ? `<div class="cvh-table-wrap"><table class="cvh-table"><thead><tr><th>package</th><th>vulnerable</th><th>patched</th></tr></thead><tbody>
              ${pk.map(v => `<tr><td><span class="cvh-eco">${esc(v.package.ecosystem)}</span> ${esc(v.package.name)}</td><td>${esc(v.vulnerable_version_range || '')}</td><td>${v.first_patched_version ? esc(typeof v.first_patched_version === 'string' ? v.first_patched_version : v.first_patched_version.identifier) : '<span class="cvh-flag">none</span>'}</td></tr>`).join('')}
            </tbody></table></div>` : ''}
            <div class="cvh-small">
              ${cvss && cvss.vector_string ? `<span class="cvh-vector">${esc(cvss.vector_string)}</span><br>` : ''}
              ${ep ? `EPSS ${pct(ep.percentage)} (percentile ${pct(ep.percentile)}) · ` : ''}
              ${(a.cwes || []).map(c => esc(c.cwe_id)).join(' ')} ${link(a.html_url, 'view on GitHub')}
            </div>
          </div>
        </details>`;
      }).join('') + (shown.length > 300 ? `<div class="cvh-small cvh-dim">showing 300 of ${shown.length}</div>` : '');
    }

    // =================================================================
    // PATCH TUESDAY (MSRC)
    // =================================================================
    const M = { month: '', items: [], src: '', note: '', shown: 60, loading: false };
    const MONTHS = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

    function msrcMonthOptions() {
      const sel = $('cvh-msrc-month');
      if (sel.options.length) return;
      const now = new Date();
      // Patch Tuesday is the 2nd Tuesday; before it, default to last month.
      const first = new Date(now.getFullYear(), now.getMonth(), 1);
      const pt = 1 + ((9 - first.getDay()) % 7) + 7;
      let d = new Date(now.getFullYear(), now.getMonth() - (now.getDate() < pt ? 1 : 0), 1);
      for (let i = 0; i < 18; i++) {
        const label = `${d.getFullYear()}-${MONTHS[d.getMonth()]}`;
        sel.add(new Option(`${MONTHS[d.getMonth()]} ${d.getFullYear()}`, label));
        d = new Date(d.getFullYear(), d.getMonth() - 1, 1);
      }
    }

    function fromSug(v) {
      return { id: v.cveNumber, title: v.cveTitle, sev: v.severity, impact: v.impact, score: v.baseScore ? Number(v.baseScore) : null,
        vector: v.vectorString, exploited: v.exploited === 'Yes', disclosed: v.publiclyDisclosed === 'Yes', tag: v.tag,
        cna: v.issuingCna, date: v.releaseDate, desc: htmlToText(v.description), action: v.customerActionRequired };
    }
    function fromCvrf(v) {
      const note = t => (v.Notes || []).find(n => n.Type === t);
      const threat = (t) => (v.Threats || []).find(x => x.Type === t);
      const ex = (threat(1) && threat(1).Description.Value) || '';
      const sc = (v.CVSSScoreSets || [])[0] || {};
      const tagNote = note(7);
      return { id: v.CVE, title: v.Title && v.Title.Value, sev: threat(3) && threat(3).Description.Value, impact: threat(0) && threat(0).Description.Value,
        score: sc.BaseScore != null ? Number(sc.BaseScore) : null, vector: sc.Vector, exploited: /Exploited:Yes/i.test(ex),
        disclosed: /Publicly Disclosed:Yes/i.test(ex), tag: tagNote && tagNote.Title, cna: note(8) && note(8).Value,
        date: v.ReleaseDate || (v.RevisionHistory && v.RevisionHistory[0] && v.RevisionHistory[0].Date),
        desc: htmlToText(note(2) && note(2).Value), kbs: (v.Remediations || []).filter(r => r.Type === 2 && r.Description && /^\d+$/.test(r.Description.Value)).map(r => r.Description.Value) };
    }

    async function msrcLoad() {
      if (M.loading) return;
      M.loading = true;
      const month = $('cvh-msrc-month').value, pref = $('cvh-msrc-src').value, third = $('cvh-msrc-third').checked;
      M.month = month; M.items = []; M.shown = 60; M.note = '';
      const list = $('cvh-msrc-list');
      const tryOrder = pref === 'cvrf' ? ['cvrf', 'sug'] : ['sug', 'cvrf'];
      let done = false, errors = [];
      for (const src of tryOrder) {
        list.innerHTML = `<div class="cvh-empty"><span class="cvh-spin"></span> loading ${month} from the ${src === 'sug' ? 'Security Update Guide API' : 'CVRF document (~20 MB, can take 10s+)'}…</div>`;
        if (src === 'sug') {
          let filter = `releaseNumber eq '${month}'`;
          if (!third) filter += ` and isMariner eq false and issuingCna eq 'Microsoft'`;
          let url = `https://api.msrc.microsoft.com/sug/v2.0/en-US/vulnerability?$filter=${encodeURIComponent(filter)}&$top=500`;
          let pages = 0, ok = true;
          const items = [];
          while (url && pages < 8) {
            const r = await getProxied(url, { timeout: 30000 });
            pages++;
            if (!r.ok) { errors.push(`Update Guide API: ${why(r)}`); ok = false; break; }
            items.push(...(r.data.value || []).map(fromSug));
            url = r.data['@odata.nextLink'] || null;
          }
          if (ok) { M.items = items; M.src = 'sug'; done = true; }
        } else {
          const r = await getProxied(`https://api.msrc.microsoft.com/cvrf/v3.0/cvrf/${month}`, { timeout: 60000 });
          if (r.ok && r.data.Vulnerability) {
            let items = r.data.Vulnerability.map(fromCvrf);
            if (!third) items = items.filter(x => x.cna === 'Microsoft' && x.tag !== 'Mariner');
            M.items = items; M.src = 'cvrf'; done = true;
          } else if (r.status === 404) {
            errors.push(`CVRF: no document for ${month} yet`);
          } else errors.push(`CVRF: ${why(r)}`);
        }
        if (done) break;
      }
      M.loading = false;
      if (!done) {
        $('cvh-msrc-stats').innerHTML = '';
        list.innerHTML = `<div class="cvh-error">Couldn't load ${esc(month)}.<br><span class="cvh-small">${errors.map(esc).join('<br>')}</span></div>`;
        return;
      }
      if (errors.length) M.note = `fell back to ${M.src === 'sug' ? 'the Update Guide API' : 'the CVRF document'} (${errors.join('; ')})`;
      msrcRender();
    }

    function msrcRender() {
      const sev = $('cvh-msrc-sev').value, onlyEx = $('cvh-msrc-ex').checked, q = $('cvh-msrc-filter').value.trim().toLowerCase();
      const all = M.items;
      let items = all.filter(x => (!sev || String(x.sev).toLowerCase() === sev) && (!onlyEx || x.exploited || x.disclosed)
        && (!q || [x.id, x.title, x.tag].some(s => String(s || '').toLowerCase().includes(q))));
      items.sort((a, b) => (b.exploited - a.exploited) || (b.disclosed - a.disclosed) || ((b.score || 0) - (a.score || 0)));
      const srcLabel = M.src === 'sug' ? 'Security Update Guide API' : 'CVRF document';
      const n = f => all.filter(f).length;
      $('cvh-msrc-stats').innerHTML = `
        <div class="cvh-tiles cvh-tiles-sm">
          <div class="cvh-tile"><div class="cvh-tile-label">CVEs ${tag('msrc', srcLabel)}</div><div class="cvh-tile-val">${all.length}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">critical</div><div class="cvh-tile-val cvh-c-crit">${n(x => x.sev === 'Critical')}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">exploited</div><div class="cvh-tile-val ${n(x => x.exploited) ? 'cvh-hot' : ''}">${n(x => x.exploited)}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">disclosed</div><div class="cvh-tile-val">${n(x => x.disclosed)}</div></div>
        </div>
        <div class="cvh-small cvh-dim">${esc(M.month)} · ${esc(srcLabel)} · ${items.length} shown${M.note ? ' · ' + esc(M.note) : ''}</div>`;

      if (!items.length) { $('cvh-msrc-list').innerHTML = `<div class="cvh-empty">Nothing matches those filters.</div>`; return; }
      $('cvh-msrc-list').innerHTML = items.slice(0, M.shown).map(x => `<details class="cvh-item ${x.exploited ? 'cvh-item-hot' : ''}" data-msrc="${esc(x.id)}">
          <summary>
            <div class="cvh-row-top">${sevBadge(x.sev, x.score)} ${cveBtn(x.id)}
              ${x.exploited ? '<span class="cvh-flag">exploited</span>' : ''}${x.disclosed ? '<span class="cvh-flag cvh-flag-soft">disclosed</span>' : ''}
              <span class="cvh-date">${esc(x.impact || '')}</span></div>
            <div class="cvh-row-title">${esc(x.title)}</div>
            ${x.tag ? `<div class="cvh-pkgs"><span class="cvh-pill">${esc(x.tag)}</span>${x.cna && x.cna !== 'Microsoft' ? `<span class="cvh-pill">CNA: ${esc(x.cna)}</span>` : ''}</div>` : ''}
          </summary>
          <div class="cvh-item-body">
            ${x.desc ? `<p class="cvh-small">${esc(x.desc)}</p>` : ''}
            ${x.vector ? `<div class="cvh-vector cvh-small">${esc(x.vector)}</div>` : ''}
            <div class="cvh-small cvh-msrc-kbs">${x.kbs && x.kbs.length ? 'Updates: ' + x.kbs.slice(0, 12).map(k => link('https://support.microsoft.com/help/' + k, 'KB' + k)).join(' ') : ''}</div>
            <div class="cvh-small">${link('https://msrc.microsoft.com/update-guide/vulnerability/' + x.id, 'open in Update Guide')}</div>
          </div>
        </details>`).join('') +
        (items.length > M.shown ? `<div class="cvh-pager"><button type="button" id="cvh-msrc-more">show ${Math.min(60, items.length - M.shown)} more (${items.length - M.shown} left)</button></div>` : '');
      const more = $('cvh-msrc-more');
      if (more) more.onclick = () => { M.shown += 60; msrcRender(); };
    }

    // Lazy: fetch products + KB articles when a Patch Tuesday item is opened (Update Guide only).
    async function msrcExpand(el) {
      const id = el.dataset.msrc, box = el.querySelector('.cvh-msrc-kbs');
      if (!box || box.dataset.loaded || M.src !== 'sug') return;
      box.dataset.loaded = '1';
      box.innerHTML = '<span class="cvh-spin"></span> loading affected products…';
      const r = await getProxied(`https://api.msrc.microsoft.com/sug/v2.0/en-US/affectedProduct?$filter=${encodeURIComponent(`cveNumber eq '${id}'`)}`);
      if (!r.ok) { box.innerHTML = `<span class="cvh-dim">products unavailable (${esc(why(r))})</span>`; return; }
      const prods = r.data.value || [];
      const kbs = new Map();
      prods.forEach(p => (p.kbArticles || []).forEach(k => { if (k.articleName && !kbs.has(k.articleName)) kbs.set(k.articleName, k.articleUrl || ('https://support.microsoft.com/help/' + k.articleName)); }));
      const names = [...new Set(prods.map(p => p.product))];
      box.innerHTML = `${names.length ? `<strong>${names.length} product${names.length > 1 ? 's' : ''}:</strong> ${names.slice(0, 10).map(esc).join(' · ')}${names.length > 10 ? ` <span class="cvh-dim">+${names.length - 10}</span>` : ''}<br>` : ''}
        ${kbs.size ? 'Updates: ' + [...kbs.entries()].slice(0, 12).map(([k, u]) => link(u, /^\d+$/.test(k) ? 'KB' + k : k)).join(' · ') : ''}`;
    }

    // =================================================================
    // CISA KEV
    // =================================================================
    const V = { data: null, src: '', days: 0, loading: false };

    async function kevEnsure() {
      if (V.data) return true;
      const tries = [
        ['GitHub mirror (cisagov/kev-data)', () => getJSON('https://raw.githubusercontent.com/cisagov/kev-data/develop/known_exploited_vulnerabilities.json', { timeout: 30000 })],
        ['cisa.gov via proxy', () => getProxied('https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json', { timeout: 30000 })],
      ];
      const errs = [];
      for (const [label, fn] of tries) {
        const r = await fn();
        if (r.ok && r.data && r.data.vulnerabilities) { V.data = r.data; V.src = label + (errs.length ? ` (after: ${errs.join('; ')})` : ''); return true; }
        errs.push(`${label}: ${why(r)}`);
      }
      $('cvh-kev-list').innerHTML = `<div class="cvh-error">Couldn't load the KEV catalogue.<br><span class="cvh-small">${errs.map(esc).join('<br>')}</span></div>`;
      return false;
    }

    async function kevLoad(days) {
      if (V.loading) return;
      V.loading = true; V.days = days;
      setActive('cvh-kev-range', days);
      if (!V.data) $('cvh-kev-list').innerHTML = `<div class="cvh-empty"><span class="cvh-spin"></span> loading the KEV catalogue…</div>`;
      const ok = await kevEnsure();
      V.loading = false;
      if (ok) kevRender();
    }

    function kevRender() {
      const q = $('cvh-kev-filter').value.trim().toLowerCase(), ransom = $('cvh-kev-ransom').checked;
      const cutoff = V.days ? isoDay(new Date(Date.now() - V.days * 864e5)) : '';
      const today = isoDay(new Date());
      let items = V.data.vulnerabilities.filter(v => (!cutoff || v.dateAdded >= cutoff)
        && (!ransom || v.knownRansomwareCampaignUse === 'Known')
        && (!q || [v.cveID, v.vendorProject, v.product, v.vulnerabilityName].some(s => String(s || '').toLowerCase().includes(q))));
      items.sort((a, b) => b.dateAdded.localeCompare(a.dateAdded) || b.cveID.localeCompare(a.cveID));
      const vendors = new Map();
      items.forEach(v => vendors.set(v.vendorProject, (vendors.get(v.vendorProject) || 0) + 1));
      const topV = [...vendors.entries()].sort((a, b) => b[1] - a[1]).slice(0, 5);
      $('cvh-kev-stats').innerHTML = `
        <div class="cvh-tiles cvh-tiles-sm">
          <div class="cvh-tile"><div class="cvh-tile-label">${V.days ? 'added' : 'entries'} ${tag('kev')}</div><div class="cvh-tile-val">${items.length}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">ransomware</div><div class="cvh-tile-val cvh-c-crit">${items.filter(v => v.knownRansomwareCampaignUse === 'Known').length}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">top vendor</div><div class="cvh-tile-val cvh-tile-text">${topV[0] ? esc(topV[0][0]) : '–'}</div></div>
          <div class="cvh-tile"><div class="cvh-tile-label">catalogue</div><div class="cvh-tile-val cvh-tile-text">v${esc(V.data.catalogVersion)}</div></div>
        </div>
        <div class="cvh-small cvh-dim">${V.data.count} entries total · source: ${esc(V.src)}${topV.length > 1 ? ' · most listed: ' + topV.map(([v, c]) => esc(v) + ' (' + c + ')').join(', ') : ''}</div>`;
      if (!items.length) { $('cvh-kev-list').innerHTML = `<div class="cvh-empty">Nothing added in that window matches.</div>`; return; }
      $('cvh-kev-list').innerHTML = items.slice(0, 200).map(v => `<details class="cvh-item">
          <summary>
            <div class="cvh-row-top">${cveBtn(v.cveID)}
              ${v.knownRansomwareCampaignUse === 'Known' ? '<span class="cvh-flag">ransomware</span>' : ''}
              <span class="cvh-date">added ${esc(fmtDate(v.dateAdded))}</span></div>
            <div class="cvh-row-title">${esc(v.vulnerabilityName)}</div>
            <div class="cvh-pkgs"><span class="cvh-pill">${esc(v.vendorProject)} · ${esc(v.product)}</span>
              <span class="cvh-pill ${v.dueDate < today ? '' : 'cvh-pill-warn'}" title="US federal agencies' remediation deadline">due ${esc(fmtDate(v.dueDate))}</span></div>
          </summary>
          <div class="cvh-item-body">
            <p class="cvh-small">${esc(v.shortDescription)}</p>
            <p class="cvh-small"><strong>Required action:</strong> ${esc(v.requiredAction)}</p>
            ${(v.cwes || []).length ? `<div class="cvh-small">${v.cwes.map(esc).join(' ')}</div>` : ''}
            ${v.notes ? `<div class="cvh-small cvh-refs-inline">${String(v.notes).split(/\s*;\s*/).filter(u => /^https?:/.test(u)).slice(0, 5).map(u => link(u)).join('<br>')}</div>` : ''}
          </div>
        </details>`).join('') + (items.length > 200 ? `<div class="cvh-small cvh-dim">showing newest 200 of ${items.length} — use the filter to narrow</div>` : '');
    }

    // =================================================================
    // wiring
    // =================================================================
    function setActive(groupId, val) {
      document.querySelectorAll(`#${groupId} [data-range]`).forEach(b => b.classList.toggle('active', Number(b.dataset.range) === val));
    }

    function openLookup(id) {
      const tabLink = document.querySelector('.cve-secondary-nav a[data-cve-tab="cve-lookup"]');
      if (tabLink && !tabLink.classList.contains('active')) tabLink.click();
      startLookup(id);
      const box = $('cve-lookup');
      if (box) box.scrollIntoView({ behavior: 'smooth', block: 'start' });
    }

    let inited = false;
    function init() {
      if (inited) return;
      inited = true;
      msrcMonthOptions();

      $('cvh-lookup-form').addEventListener('submit', e => { e.preventDefault(); startLookup($('cvh-q').value); });
      document.querySelectorAll('.cvh-examples [data-q]').forEach(b => b.addEventListener('click', () => {
        if (b.dataset.mode) $('cvh-mode').value = b.dataset.mode;
        startLookup(b.dataset.q);
      }));

      // Delegated clicks inside the CVE section
      $('cve').addEventListener('click', e => {
        const cve = e.target.closest('.cvh-cvebtn');
        if (cve) { e.preventDefault(); e.stopPropagation(); openLookup(cve.dataset.cve); return; }
        const chip = e.target.closest('.cvh-chip-fail');
        if (chip && L.id) { runSource(chip.dataset.src, L.id); return; }
        const kw = e.target.closest('[data-kw]');
        if (kw && !kw.disabled) { keywordSearch(K.q, Number(kw.dataset.kw)); $('cve-lookup').scrollIntoView({ block: 'start' }); return; }
        const g = e.target.closest('#cvh-ghsa-range [data-range]');
        if (g) { ghsaLoad(Number(g.dataset.range)); return; }
        const day = e.target.closest('[data-day]');
        if (day && G.items.length) { G.day = day.dataset.day && G.day !== day.dataset.day ? day.dataset.day : null; ghsaRender(); return; }
        const k = e.target.closest('#cvh-kev-range [data-range]');
        if (k) { kevLoad(Number(k.dataset.range)); return; }
      });

      // Lazy KB lookup when a Patch Tuesday item opens
      $('cvh-msrc-list').addEventListener('toggle', e => { if (e.target.open && e.target.dataset.msrc) msrcExpand(e.target); }, true);

      $('cvh-msrc-load').addEventListener('click', msrcLoad);
      ['cvh-msrc-sev', 'cvh-msrc-ex'].forEach(id => $(id).addEventListener('change', () => { M.shown = 60; if (M.items.length) msrcRender(); }));
      $('cvh-msrc-filter').addEventListener('input', () => { M.shown = 60; if (M.items.length) msrcRender(); });
      $('cvh-msrc-third').addEventListener('change', () => { if (M.items.length) msrcLoad(); });

      ['cvh-ghsa-sev', 'cvh-ghsa-eco', 'cvh-ghsa-type'].forEach(id => $(id).addEventListener('change', () => { if (G.days) ghsaLoad(G.days); }));
      $('cvh-ghsa-filter').addEventListener('input', () => { if (G.items.length) ghsaRender(); });

      $('cvh-kev-filter').addEventListener('input', () => { if (V.data) kevRender(); });
      $('cvh-kev-ransom').addEventListener('change', () => { if (V.data) kevRender(); });
    }

    // Deep link: /dashboard/#cve=CVE-2024-3094 opens the CVE tab and runs the lookup
    function fromHash() {
      const m = location.hash.match(/^#cve=(CVE-\d{4}-\d{4,})$/i);
      if (!m) return;
      const tabLink = document.querySelector('.dashboard-tabs a[data-tab="cve"]');
      if (tabLink && !tabLink.classList.contains('active')) tabLink.click();
      init();
      openLookup(m[1].toUpperCase());
    }

    return { init, openLookup, fromHash };
  })();

  window.addEventListener('hashchange', cveHub.fromHash);
  if (document.readyState === 'loading') document.addEventListener('DOMContentLoaded', cveHub.fromHash);
  else cveHub.fromHash();

  // Initialize flags
  window.cveToolsInitialized = false;

  // Domain Intelligence script
          let currentDomain = '';

        // Main analysis function
        async function analyzeDomain() {
            const domain = document.getElementById('domain-input').value.trim();
            if (!domain) {
                alert('Please enter a domain');
                return;
            }

            // Clean domain input
            currentDomain = domain.replace(/^https?:\/\//, '').replace(/\/$/, '');
            
            // Show results grid and disable button
            document.getElementById('results-grid').style.display = 'grid';
            document.getElementById('analyze-btn').disabled = true;
            document.getElementById('analyze-btn').textContent = 'Analyzing...';

            // Reset all content areas to loading
            const contentAreas = ['dns-content', 'cert-content', 'archive-content', 'summary-content'];
            contentAreas.forEach(id => {
                document.getElementById(id).innerHTML = '<div class="loading">Analyzing...</div>';
            });

            // Run all analyses in parallel
            await Promise.all([
                analyzeDNS(),
                analyzeCertificates(),
                analyzeArchive(),
                generateSummary()
            ]);

            // Re-enable button
            document.getElementById('analyze-btn').disabled = false;
            document.getElementById('analyze-btn').textContent = 'Analyze Domain';
        }

        // DNS Analysis
        async function analyzeDNS() {
            try {
                const response = await fetch(`https://cloudflare-dns.com/dns-query?name=${currentDomain}&type=A`, {
                    headers: { 'Accept': 'application/dns-json' }
                });
                const data = await response.json();
                
                let html = '';
                if (data.Status === 0 && data.Answer) {
                    html += `<div><span class="domain-status-indicator domain-status-online"></span><strong>Domain Resolves</strong></div>`;
                    html += `<h4>IP Addresses (${data.Answer.length}):</h4>`;
                    data.Answer.forEach(record => {
                        html += `<div class="domain-dns-record">${record.data} (TTL: ${record.TTL}s)</div>`;
                    });
                } else {
                    html += `<div><span class="status-indicator status-offline"></span><strong>Domain Does Not Resolve</strong></div>`;
                    html += `<div class="error">No A records found for ${currentDomain}</div>`;
                }
                
                document.getElementById('dns-content').innerHTML = html;
            } catch (error) {
                document.getElementById('dns-content').innerHTML = 
                    `<div class="error">DNS lookup failed: ${error.message}</div>`;
            }
        }

        // Certificate Analysis
        async function analyzeCertificates() {
            try {
                const response = await fetch(proxied(`https://crt.sh/?q=${currentDomain}&output=json`));
                const data = await response.json();
                
                // Store certificate count globally for summary
                window.certificateCount = (data && data.length > 0) ? data.length : 0;
                
                let html = '';
                if (data && data.length > 0) {
                    // Sort by most recent first
                    const sortedCerts = data.sort((a, b) => new Date(b.entry_timestamp) - new Date(a.entry_timestamp));
                    const recentCerts = sortedCerts.slice(0, 10); // Show top 10
                    
                    html += `<div><strong>Found ${data.length} certificates (showing 10 most recent)</strong></div><br>`;
                    
                    recentCerts.forEach(cert => {
                        const entryDate = new Date(cert.entry_timestamp).toLocaleDateString();
                        const notBefore = new Date(cert.not_before).toLocaleDateString();
                        const notAfter = new Date(cert.not_after).toLocaleDateString();
                        
                        html += `<div class="domain-cert-item">`;
                        html += `<div class="domain-cert-cn">${cert.common_name}</div>`;
                        html += `<div class="domain-cert-dates">Valid: ${notBefore} - ${notAfter}</div>`;
                        html += `<div class="domain-cert-issuer">Issuer: ${cert.issuer_name.split(',')[0]}</div>`;
                        html += `<div class="domain-cert-dates">Logged: ${entryDate}</div>`;
                        html += `</div>`;
                    });
                } else {
                    html = '<div class="error">No certificates found in transparency logs</div>';
                }
                
                document.getElementById('cert-content').innerHTML = html;
            } catch (error) {
                window.certificateCount = 0;
                document.getElementById('cert-content').innerHTML = 
                    `<div class="error">Certificate lookup failed: ${error.message}</div>`;
            }
        }

        // Wayback Machine Analysis
        async function analyzeArchive() {
            try {
                const response = await fetch(`https://archive.org/wayback/available?url=https://${currentDomain}`);
                const data = await response.json();
                
                let html = '';
                if (data.archived_snapshots && data.archived_snapshots.closest && data.archived_snapshots.closest.available) {
                    const snapshot = data.archived_snapshots.closest;
                    const archiveDate = new Date(
                        snapshot.timestamp.substr(0,4) + '-' + 
                        snapshot.timestamp.substr(4,2) + '-' + 
                        snapshot.timestamp.substr(6,2)
                    ).toLocaleDateString();
                    
                    html += `<div class="domain-archive-info">`;
                    html += `<div><span class="status-indicator status-online"></span><strong>Archive Available</strong></div>`;
                    html += `<div><strong>Last Archived:</strong> ${archiveDate}</div>`;
                    html += `<a href="${snapshot.url}" target="_blank" class="domain-archive-link">View Archive</a>`;
                    html += `</div>`;
                } else {
                    html += `<div class="domain-archive-info">`;
                    html += `<div><span class="status-indicator status-offline"></span><strong>No Archive Found</strong></div>`;
                    html += `<div>This domain has not been archived by the Wayback Machine</div>`;
                    html += `</div>`;
                }
                
                document.getElementById('archive-content').innerHTML = html;
            } catch (error) {
                document.getElementById('archive-content').innerHTML = 
                    `<div class="error">Archive lookup failed: ${error.message}</div>`;
            }
        }

        // Generate Summary
        async function generateSummary() {
            // Wait a moment for other analyses to complete
            await new Promise(resolve => setTimeout(resolve, 1500));
            
            let html = `<div><strong>Domain:</strong> ${currentDomain}</div><br>`;
            
            // Check DNS status
            const dnsContent = document.getElementById('dns-content').innerHTML;
            const dnsOnline = dnsContent.includes('status-online');
            
            // Get certificate count from global variable
            const certCount = window.certificateCount || 0;
            
            // Check archive status
            const archiveContent = document.getElementById('archive-content').innerHTML;
            const archiveAvailable = archiveContent.includes('status-online');
            
            html += `<div><strong>Status:</strong> ${dnsOnline ? '🟢 Online' : '🔴 Offline'}</div>`;
            html += `<div><strong>SSL Certificates:</strong> ${certCount} found</div>`;
            html += `<div><strong>Archive Status:</strong> ${archiveAvailable ? '📚 Archived' : '❌ Not Archived'}</div><br>`;
            
            // Risk assessment
            html += `<div><strong>Assessment:</strong></div>`;
            if (dnsOnline && certCount > 0) {
                html += `<div style="color: var(--db-low);">✓ Active domain with SSL certificates</div>`;
            } else if (dnsOnline) {
                html += `<div style="color: var(--db-med);">⚠ Domain resolves but no certificates found</div>`;
            } else {
                html += `<div style="color: var(--db-crit);">⚠ Domain does not resolve</div>`;
            }
            
            document.getElementById('summary-content').innerHTML = html;
        }

        // Allow Enter key to trigger analysis
        document.getElementById('domain-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                analyzeDomain();
            }
        });
</script>
