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
:where(#dashboard-app, .nvd-popup-overlay) :where(input, select, textarea, button) {
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

:where(#dashboard-app, .nvd-popup-overlay) button {
  background: var(--chrome);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 6px 14px;
  font-size: 0.85rem;
  cursor: pointer;
  transition: background-color 0.15s, color 0.15s, border-color 0.15s;
}

:where(#dashboard-app, .nvd-popup-overlay) button:hover:not(:disabled) {
  color: var(--accent);
  border-color: var(--accent);
}

:where(#dashboard-app, .nvd-popup-overlay) button:disabled {
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

/* Tool header bar (shared look for Domain / NVD / GHSA / MSRC / CVEDB) */
.domain-header,
.nvd-header,
.cve-header,
.msrc-header,
.shodan-header,
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
.nvd-header h1,
.cve-header h1,
.msrc-header h1,
.shodan-header h1,
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
.nvd-header p,
.cve-header p,
.msrc-header p,
.shodan-header p,
.currency-header p {
  color: var(--text-dim);
  font-size: 0.78rem;
  margin: 4px 0 0 15px;
  opacity: 1;
}

/* Small callouts / info boxes */
.msrc-api-info,
.shodan-disclaimer {
  background: var(--db-tint);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 4px;
  padding: 10px 14px;
  margin: 0 0 16px;
  font-size: 0.8rem;
  color: var(--text);
  text-align: left;
  line-height: 1.6;
}

.msrc-api-info p { color: var(--text); margin: 0; font-size: 0.8rem; }
.msrc-api-info code,
.shodan-disclaimer code { font-size: 0.85em; }
.shodan-disclaimer strong { color: var(--heading); }

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

.close-modal,
.nvd-popup-close {
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

.close-modal:hover,
.nvd-popup-close:hover { background: rgba(0, 0, 0, 0.75) !important; color: #fff !important; }

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
   CVE Tracker — GHSA calendar
   ============================================================= */
.cve-tracker-container {
  color: var(--text);
  font-size: 14px;
}

.cve-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  padding: 10px 12px;
  margin-bottom: 16px;
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  flex-wrap: wrap;
}

.cve-filter-group {
  display: flex;
  align-items: center;
  gap: 8px;
}

.cve-filter-label {
  color: var(--text-dim);
  font-weight: 600;
  font-size: 0.8rem;
}

.cve-filter-select { font-size: 0.8rem !important; padding: 4px 8px !important; }

.cve-calendar-nav {
  display: flex;
  align-items: center;
  gap: 12px;
  position: relative;
}

.cve-nav-btn {
  padding: 4px 10px !important;
  font-size: 0.8rem !important;
}

.cve-current-month {
  font-weight: bold;
  color: var(--heading);
  min-width: 120px;
  text-align: center;
  font-size: 0.9em;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2px;
  position: relative;
}

.cve-month-text { color: var(--heading); }

.cve-year-text {
  color: var(--accent);
  font-size: 0.85em;
  text-decoration: underline;
  cursor: pointer;
}
.cve-year-text:hover { color: var(--link-hover); }

.cve-year-picker {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 6px;
  z-index: 1000;
  display: none;
  max-height: 200px;
  overflow-y: auto;
  min-width: 100px;
  margin-top: 5px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.25);
}

.cve-year-picker.cve-show { display: block; }

.cve-year-option {
  padding: 4px 10px;
  cursor: pointer;
  color: var(--text);
  text-align: center;
  border-radius: 3px;
}

.cve-year-option:hover,
.cve-year-option.cve-current {
  background: var(--db-tint);
  color: var(--accent);
}

.cve-dashboard {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 16px;
  margin: 0 auto;
  height: calc(100vh - 160px);
}

.cve-main-panel,
.cve-side-panel {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 16px;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  min-width: 0;
}

.cve-side-panel { max-height: calc(100vh - 160px); }

.cve-panel-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  margin-bottom: 14px;
  padding-bottom: 10px;
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
}

.cve-panel-title {
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--heading);
  font-size: 0.95rem;
  font-weight: 600;
}

.cve-api-status {
  padding: 1px 8px;
  border-radius: 3px;
  font-size: 0.68rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  border: 1px solid currentColor;
  white-space: nowrap;
}

.cve-api-live  { color: var(--db-low);  background: var(--db-tint); }
.cve-api-error { color: var(--db-crit); background: transparent; }

.cve-calendar-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  margin-top: 4px;
}

/* The JS never removes .cve-loading from #cve-calendar-content, so once the
   grid is rendered undo the fixed 150px centred box (the old design hid this
   with a big margin-top). */
#cve-calendar-content.cve-loading:has(.cve-calendar-grid) {
  display: block;
  height: auto;
}

.cve-calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 3px;
  flex: 1;
}

.cve-calendar-header {
  background: var(--db-bar);
  padding: 6px 4px;
  text-align: center;
  font-weight: bold;
  color: var(--text-dim);
  border-radius: 3px;
  font-size: 0.75em;
}

.cve-calendar-day {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 3px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: border-color 0.15s ease, transform 0.15s ease;
  position: relative;
  min-height: 45px;
  padding: 3px;
  color: var(--text);
}

.cve-calendar-day:hover {
  border-color: var(--accent);
  transform: scale(1.04);
  z-index: 5;
}

.cve-calendar-day.selected {
  border: 2px solid var(--accent);
  transform: scale(1.04);
}

.cve-calendar-day.other-month { opacity: 0.35; }

.cve-calendar-day.today {
  border: 2px solid var(--accent-2);
}

.cve-day-number {
  font-size: 0.85em;
  font-weight: bold;
  margin-bottom: 2px;
}

.cve-day-count {
  font-size: 0.68em;
  background: var(--chrome);
  border: 1px solid var(--border);
  padding: 0 4px;
  border-radius: 3px;
  min-width: 16px;
  text-align: center;
  line-height: 1.4;
}

/* Heatmap: accent for light activity, warming up to red */
.cve-day-heat-0 { background: var(--bg) !important; }
.cve-day-heat-1 { background: color-mix(in srgb, var(--db-low)  14%, var(--bg)) !important; }
.cve-day-heat-2 { background: color-mix(in srgb, var(--db-low)  30%, var(--bg)) !important; }
.cve-day-heat-3 { background: color-mix(in srgb, var(--db-med)  32%, var(--bg)) !important; }
.cve-day-heat-4 { background: color-mix(in srgb, var(--db-high) 36%, var(--bg)) !important; }
.cve-day-heat-5 { background: color-mix(in srgb, var(--db-crit) 40%, var(--bg)) !important; }

.cve-stats-summary {
  display: flex;
  gap: 10px;
  margin-bottom: 14px;
  flex-shrink: 0;
}

.cve-stat-box {
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 8px;
  border-radius: 4px;
  text-align: center;
  flex: 1;
}

.cve-stat-number {
  font-size: 1.3em;
  font-weight: bold;
  color: var(--heading);
  margin-bottom: 2px;
}
.cve-stat-box:first-child .cve-stat-number { color: var(--db-crit); }
.cve-stat-box:nth-child(2) .cve-stat-number { color: var(--db-high); }

.cve-stat-label {
  font-size: 0.75em;
  color: var(--text-dim);
}

.cve-loading {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 150px;
  color: var(--text-dim);
  font-size: 0.9em;
}

.cve-spinner,
.msrc-spinner {
  width: 24px;
  height: 24px;
  border: 3px solid var(--border);
  border-top: 3px solid var(--accent);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-right: 12px;
}

.cve-error {
  color: var(--db-crit);
  text-align: center;
  padding: 30px;
  font-size: 0.9em;
}

.cve-no-advisories {
  text-align: center;
  color: var(--text-dim);
  padding: 30px;
  font-style: italic;
  font-size: 0.85em;
}

.cve-advisory-item {
  background: var(--bg);
  border: 1px solid var(--border);
  border-left: 3px solid var(--db-crit);
  border-radius: 4px;
  padding: 10px 12px;
  margin-bottom: 8px;
  transition: border-color 0.15s ease, transform 0.15s ease;
  cursor: pointer;
}

.cve-advisory-item:hover {
  border-color: var(--accent);
  transform: translateX(2px);
}

.cve-advisory-item.expanded { border-color: var(--accent); }

/* Severity badges (shared look across GHSA / NVD / MSRC / CVEDB) */
.cve-severity-badge,
.nvd-cvss-badge,
.msrc-cve-severity,
.shodan-badge,
.shodan-cvss-tag {
  display: inline-block;
  padding: 1px 8px;
  border-radius: 3px;
  font-size: 0.7rem;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 0.3px;
  border: 1px solid currentColor;
  background: transparent;
  white-space: nowrap;
}

.cve-severity-critical, .nvd-cvss-critical, .msrc-severity-critical,
.shodan-badge.kev, .shodan-badge.epss-high {
  color: var(--db-crit);
  background: color-mix(in srgb, var(--db-crit) 10%, transparent);
}
.cve-severity-high, .nvd-cvss-high, .msrc-severity-important {
  color: var(--db-high);
  background: color-mix(in srgb, var(--db-high) 10%, transparent);
}
.cve-severity-medium, .nvd-cvss-medium, .msrc-severity-moderate,
.shodan-badge.epss-medium {
  color: var(--db-med);
  background: color-mix(in srgb, var(--db-med) 10%, transparent);
}
.cve-severity-low, .nvd-cvss-low, .msrc-severity-low,
.shodan-badge.epss-low {
  color: var(--db-low);
  background: color-mix(in srgb, var(--db-low) 10%, transparent);
}
.nvd-cvss-none, .msrc-severity-unknown {
  color: var(--text-dim);
}
.shodan-badge.cvss, .shodan-cvss-tag {
  color: var(--db-info);
  background: color-mix(in srgb, var(--db-info) 10%, transparent);
}

.cve-advisory-details {
  display: none;
  margin-top: 10px;
  padding-top: 10px;
  border-top: 1px solid var(--border);
}

.cve-advisory-details.cve-show { display: block; }

.cve-selected-date-info {
  background: var(--db-tint);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  padding: 10px 12px;
  border-radius: 4px;
  margin-bottom: 12px;
  flex-shrink: 0;
}

.cve-selected-date {
  font-size: 0.95em;
  font-weight: bold;
  color: var(--heading);
  margin-bottom: 2px;
}

.cve-date-summary {
  font-size: 0.8em;
  color: var(--text-dim);
}

.cve-advisory-list {
  flex: 1;
  overflow-y: auto;
  padding-right: 5px;
}

.cve-advisory-list::-webkit-scrollbar { width: 4px; }
.cve-advisory-list::-webkit-scrollbar-track { background: var(--chrome); border-radius: 2px; }
.cve-advisory-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

.cve-advisory-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 8px;
  margin-bottom: 6px;
}

.cve-advisory-title {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.cve-advisory-id {
  font-size: 0.85em;
  font-weight: bold;
  color: var(--accent);
}

.cve-id {
  font-size: 0.75em;
  color: var(--accent-2);
}

.cve-advisory-summary {
  font-size: 0.78em;
  line-height: 1.4;
  color: var(--text);
  margin-bottom: 6px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.cve-detail-row {
  display: flex;
  margin: 5px 0;
  font-size: 0.75em;
}

.cve-detail-label {
  font-weight: bold;
  color: var(--text-dim);
  min-width: 80px;
}

.cve-detail-value {
  color: var(--text);
  word-break: break-word;
}

.cve-external-link,
.cve-external-link:visited {
  display: inline-block;
  margin-top: 8px;
  padding: 3px 10px;
  border: 1px solid var(--accent);
  border-radius: 3px;
  color: var(--accent);
  text-decoration: none;
  font-size: 0.75em;
}

.cve-external-link:hover {
  background: var(--accent);
  color: var(--db-ink);
  text-decoration: none;
}

/* =============================================================
   CVE Tracker — MSRC
   ============================================================= */
.msrc-tracker-container { color: var(--text); }

.msrc-loading {
  position: absolute;
  top: 50%;
  right: 14px;
  transform: translateY(-50%);
  display: none;
}

.msrc-loading .msrc-spinner { margin-right: 0; }

.msrc-controls { margin-bottom: 16px; }

.msrc-stats {
  display: flex;
  gap: 10px;
  align-items: stretch;
}

.msrc-stat-item {
  flex: 1;
  background: var(--chrome);
  border: 1px solid var(--border);
  padding: 8px 12px;
  border-radius: 4px;
  text-align: center;
  min-width: 80px;
}

.msrc-stat-number {
  font-size: 1.3rem;
  font-weight: bold;
  color: var(--heading);
}
.msrc-stat-item:nth-child(2) .msrc-stat-number { color: var(--db-crit); }

.msrc-stat-label {
  font-size: 0.72rem;
  color: var(--text-dim);
  margin-top: 2px;
}

.msrc-demo-section > h2 {
  font-size: 1rem !important;
  color: var(--heading) !important;
  margin: 0 0 12px !important;
}

.msrc-demo-controls {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
  align-items: center;
}

.msrc-demo-btn.msrc-primary {
  background: var(--accent);
  border-color: var(--accent);
  color: var(--db-ink);
}
.msrc-demo-btn.msrc-primary:hover:not(:disabled) { color: var(--db-ink); filter: brightness(1.1); }

.msrc-filter-controls {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 10px 12px;
  margin-bottom: 16px;
  display: flex;
  gap: 16px;
  align-items: center;
  flex-wrap: wrap;
}

.msrc-filter-group {
  display: flex;
  align-items: center;
  gap: 8px;
}

.msrc-filter-group label {
  font-weight: 600;
  color: var(--text-dim);
  font-size: 0.8rem;
}

.msrc-pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding: 16px 0 0;
  margin-top: 16px;
  border-top: 1px solid var(--border);
}

.msrc-pagination-info {
  margin: 0 10px;
  font-weight: 600;
  color: var(--text-dim);
  font-size: 0.85rem;
}

.msrc-cve-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 12px;
  margin-top: 16px;
}

.msrc-cve-item {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent-2);
  border-radius: 4px;
  padding: 14px;
  transition: border-color 0.15s ease, transform 0.15s ease;
  cursor: pointer;
  min-width: 0;
}

.msrc-cve-item:hover {
  transform: translateY(-2px);
  border-color: var(--accent);
}

.msrc-cve-item:active { transform: translateY(-1px); }

.msrc-external-link-icon {
  opacity: 0;
  transition: opacity 0.2s ease;
  margin-left: 8px;
  font-size: 0.9rem;
  color: var(--accent);
}

.msrc-cve-item:hover .msrc-external-link-icon { opacity: 1; }

.msrc-cve-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 8px;
  flex-wrap: wrap;
  gap: 8px;
}

.msrc-cve-id {
  font-weight: bold;
  color: var(--accent);
  font-size: 0.95rem;
}

.msrc-cve-date {
  color: var(--text-dim);
  font-size: 0.78rem;
}

.msrc-cve-title {
  margin-bottom: 8px;
  color: var(--heading);
  line-height: 1.4;
  font-size: 0.85rem;
}

.msrc-cve-description {
  margin-top: 8px;
  color: var(--text-dim);
  font-size: 0.8rem;
  line-height: 1.4;
}

.msrc-no-data {
  grid-column: 1 / -1;
  text-align: center;
  color: var(--text-dim);
  font-style: italic;
  padding: 36px;
  background: var(--chrome);
  border: 1px dashed var(--border);
  border-radius: 4px;
  font-size: 0.85rem;
}

.msrc-error,
.msrc-success,
.msrc-results-summary {
  padding: 10px 14px;
  border-radius: 4px;
  margin: 12px 0;
  font-size: 0.85rem;
  border: 1px solid currentColor;
  border-left-width: 3px;
}

.msrc-error   { color: var(--db-crit); background: color-mix(in srgb, var(--db-crit) 8%, transparent); }
.msrc-success { color: var(--db-low);  background: var(--db-tint); }

.msrc-results-summary {
  color: var(--text);
  border-color: var(--border);
  border-left-color: var(--accent);
  background: var(--db-tint);
}

/* =============================================================
   CVE Tracker — NVD
   ============================================================= */
.nvd-status-badge {
  display: inline-block;
  color: var(--db-low);
  border: 1px solid currentColor;
  background: var(--db-tint);
  padding: 1px 8px;
  border-radius: 3px;
  font-size: 0.72rem;
  font-weight: 600;
  margin: 8px 0 0 15px;
}

.nvd-search-section {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 16px;
  margin-bottom: 16px;
}

.nvd-input-group { margin-bottom: 14px; }

.nvd-input-group label {
  display: block;
  margin-bottom: 4px;
  font-weight: 600;
  color: var(--text-dim);
  font-size: 0.78rem;
}

.nvd-input-group input,
.nvd-input-group select {
  width: 100%;
  box-sizing: border-box;
  padding: 8px 12px;
  font-size: 0.88rem;
}

.nvd-grid-controls {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 12px;
  margin-bottom: 16px;
}

.nvd-button,
.shodan-search-btn {
  background: var(--accent) !important;
  border-color: var(--accent) !important;
  color: var(--db-ink) !important;
  font-weight: 600;
}
.nvd-button:hover:not(:disabled),
.shodan-search-btn:hover:not(:disabled) { filter: brightness(1.1); }

.nvd-results-container {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 16px;
  display: none;
  font-size: 0.85rem;
}

.nvd-vulnerability-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent-2);
  border-radius: 4px;
  padding: 12px 14px;
  margin-bottom: 10px;
  cursor: pointer;
  transition: border-color 0.15s ease, transform 0.15s ease;
}

.nvd-vulnerability-card:hover {
  transform: translateY(-1px);
  border-color: var(--accent);
}

.nvd-card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
  margin-bottom: 8px;
}

.nvd-cve-id {
  font-size: 0.95em;
  font-weight: bold;
  color: var(--accent);
}

.nvd-card-description {
  color: var(--text);
  font-size: 0.8rem;
  line-height: 1.45;
  margin-bottom: 8px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.nvd-card-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
  font-size: 0.72rem;
  color: var(--text-dim);
}

.nvd-click-hint {
  color: var(--accent);
  font-weight: 600;
  border: 1px solid var(--border);
  padding: 0 6px;
  border-radius: 3px;
}

.nvd-loading {
  text-align: center;
  color: var(--text-dim);
  font-style: italic;
  padding: 30px;
}

.nvd-error {
  color: var(--db-crit);
  background: color-mix(in srgb, var(--db-crit) 8%, transparent);
  border: 1px solid currentColor;
  border-left-width: 3px;
  padding: 12px 14px;
  border-radius: 4px;
}

/* NVD popup (lives outside #dashboard-app) */
.nvd-popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 1000;
  display: none;
  overflow-y: auto;
  padding: 20px;
  box-sizing: border-box;
}

.nvd-popup-content {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 10px;
  max-width: 800px;
  width: 100%;
  margin: 0 auto;
  position: relative;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.4);
  top: 0;
  font-size: 0.88rem;
}

.nvd-popup-content h2,
.nvd-popup-content h3 { margin-top: 0; }

.nvd-popup-close { color: #fff; }

.nvd-popup-body { padding: 24px; }

/* =============================================================
   CVE Tracker — Shodan CVEDB
   ============================================================= */
.shodan-search-section {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 16px;
  margin-bottom: 16px;
}

.shodan-search-controls {
  display: grid;
  grid-template-columns: 1fr 120px;
  gap: 12px;
  margin-bottom: 0;
  align-items: end;
}

.shodan-form-group {
  display: flex;
  flex-direction: column;
}

.shodan-form-group label {
  font-weight: 600;
  margin-bottom: 4px;
  color: var(--text-dim);
  font-size: 0.78rem;
}

.shodan-form-group select,
.shodan-form-group input {
  padding: 8px 12px;
  font-size: 0.88rem;
}

.shodan-search-btn { padding: 8px 14px !important; }

.shodan-disclaimer { margin: 14px 0 0; }

.shodan-results-section { padding: 0; }

.shodan-loading {
  text-align: center;
  padding: 40px;
  color: var(--text-dim);
}

.shodan-loading::after {
  content: '';
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 3px solid var(--border);
  border-top: 3px solid var(--accent);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-left: 10px;
  vertical-align: middle;
}

.shodan-error {
  color: var(--db-crit);
  background: color-mix(in srgb, var(--db-crit) 8%, transparent);
  border: 1px solid currentColor;
  border-left-width: 3px;
  padding: 12px 14px;
  border-radius: 4px;
  margin-bottom: 16px;
}

.shodan-results-summary {
  background: var(--db-tint);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  padding: 10px 14px;
  border-radius: 4px;
  margin-bottom: 16px;
}

.shodan-vulnerability-card,
.shodan-list-item {
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent-2);
  border-radius: 4px;
  padding: 18px;
  margin-bottom: 16px;
}

.shodan-cve-header,
.shodan-list-item-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 14px;
  flex-wrap: wrap;
  gap: 10px;
}

.shodan-cve-id,
.shodan-list-item-cve {
  font-size: 1.1em;
  font-weight: 700;
  color: var(--accent);
}

.shodan-badges {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}

.shodan-vulnerability-summary,
.shodan-list-item-summary {
  margin-bottom: 18px;
  line-height: 1.6;
  color: var(--text);
  font-size: 0.88em;
}

.shodan-metrics {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 10px;
  margin-bottom: 18px;
}

.shodan-metric {
  text-align: center;
  padding: 10px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 4px;
}

.shodan-metric-value {
  font-size: 1.3em;
  font-weight: 700;
  color: var(--heading);
  display: block;
}

.shodan-metric-label {
  font-size: 0.75em;
  color: var(--text-dim);
  margin-top: 2px;
}

.shodan-proposed-action {
  background: var(--db-tint);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  padding: 10px 14px;
  border-radius: 4px;
  margin-bottom: 16px;
}

.shodan-proposed-action h4 {
  color: var(--accent);
  margin: 0 0 6px;
  font-size: 0.9em;
}

.shodan-proposed-action p {
  color: var(--text);
  margin: 0;
  line-height: 1.5;
  font-size: 0.85em;
}

.shodan-published-date {
  color: var(--text-dim);
  font-size: 0.8em;
  margin-top: 12px;
}

.shodan-additional-info { margin: 18px 0; }

.shodan-expand-btn { margin-bottom: 12px; }

.shodan-details-section {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 14px;
  margin-top: 12px;
}

.shodan-detail-block { margin-bottom: 16px; }

.shodan-detail-block h4 {
  color: var(--heading);
  margin: 0 0 8px;
  font-size: 0.9em;
}

.shodan-cpe-list {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.shodan-cpe-tag {
  background: var(--chrome);
  border: 1px solid var(--border);
  padding: 1px 6px;
  border-radius: 3px;
  font-size: 0.75em;
  word-break: break-all;
}

.shodan-cpe-more,
.shodan-ref-more {
  color: var(--text-dim);
  font-style: italic;
  font-size: 0.85em;
}

.shodan-ref-more { margin: 5px 0 0 0; }

.shodan-references-list {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.shodan-reference-link,
.shodan-reference-link:visited {
  color: var(--accent);
  text-decoration: none;
  padding: 6px 10px;
  background: var(--chrome);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: 3px;
  font-size: 0.8em;
  word-break: break-all;
}

.shodan-reference-link:hover { border-color: var(--accent); text-decoration: none; }

.shodan-cvss-versions {
  display: flex;
  gap: 8px;
}

.shodan-external-links {
  display: flex;
  gap: 8px;
  margin: 18px 0 10px;
  flex-wrap: wrap;
}

.shodan-external-link,
.shodan-external-link:visited {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  color: var(--accent);
  border: 1px solid var(--accent);
  text-decoration: none;
  padding: 4px 12px;
  border-radius: 3px;
  font-size: 0.85em;
  font-weight: 600;
}

.shodan-external-link:hover {
  background: var(--accent);
  color: var(--db-ink);
  text-decoration: none;
}

.shodan-no-results {
  text-align: center;
  padding: 36px 20px;
  color: var(--text-dim);
  background: var(--chrome);
  border: 1px dashed var(--border);
  border-radius: 4px;
  font-size: 0.85rem;
}

.shodan-no-results h3 {
  margin: 0 0 10px;
  color: var(--heading);
  font-size: 1rem;
}

.shodan-results-list {
  display: grid;
  gap: 12px;
}

.shodan-list-item-metrics {
  display: flex;
  gap: 10px;
  font-size: 0.8em;
}

.shodan-list-metric {
  background: var(--bg);
  border: 1px solid var(--border);
  padding: 2px 8px;
  border-radius: 3px;
  font-weight: 600;
}

/* =============================================================
   Responsive
   ============================================================= */
@media (max-width: 1200px) {
  .cve-dashboard {
    grid-template-columns: 1fr;
    gap: 14px;
    height: auto;
  }

  .cve-main-panel { min-height: 380px; }

  .cve-controls {
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }

  .msrc-cve-grid { grid-template-columns: 1fr; }

  .msrc-demo-controls,
  .msrc-filter-controls {
    flex-direction: column;
    align-items: stretch;
  }

  .msrc-filter-group { justify-content: space-between; }

  .nvd-grid-controls {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .shodan-search-controls { grid-template-columns: 1fr; }

  .shodan-metrics { grid-template-columns: repeat(2, 1fr); }
}

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


  .cve-main-panel { min-height: 350px; }

  .cve-calendar-day {
    min-height: 34px;
    font-size: 0.85em;
    padding: 2px;
  }

  .cve-day-number { font-size: 0.75em; margin-bottom: 1px; }
  .cve-day-count  { font-size: 0.55em; padding: 0 3px; }
  .cve-calendar-grid { gap: 2px; }

  .msrc-stats { flex-wrap: wrap; }

  .nvd-card-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 6px;
  }

  .nvd-popup-overlay { padding: 10px; }
  .nvd-popup-body { padding: 16px 8px; }

  .shodan-cve-header {
    flex-direction: column;
    align-items: flex-start;
  }

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
    <a href="#" class="active" data-cve-tab="nvd">NVD Lookup</a>
    <a href="#" data-cve-tab="ghsa">GHSA Tracker</a>
    <a href="#" data-cve-tab="msrc">MSRC Tracker</a>
    <a href="#" data-cve-tab="shodan">Shodan CVEDB</a>
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

    <!-- CVE Tracker Tab (Container for sub-tabs) -->
    <section id="cve" class="tab-content">
      
      <!-- NVD Lookup Sub-tab -->
      <div id="nvd" class="cve-sub-tab active">
        <div class="nvd-container">
          <div class="nvd-inner-container">
            <div class="nvd-header">
              <h1>🛡️ NVD Vulnerability Lookup</h1>
              <div class="nvd-status-badge">✅ Live API - NIST National Vulnerability Database</div>
              <p>Real-time vulnerability data from the official US government database</p>
            </div>
            
            <div class="nvd-search-section">
              <div class="nvd-input-group">
                <label for="nvd-searchType">Search Type:</label>
                <select id="nvd-searchType" onchange="nvdTool.updatePlaceholder()">
                  <option value="cve">Specific CVE ID</option>
                  <option value="keyword">Keyword Search</option>
                </select>
              </div>
              
              <div class="nvd-input-group">
                <label for="nvd-searchInput">Search Term:</label>
                <input type="text" id="nvd-searchInput" placeholder="CVE-2024-3094" value="CVE-2024-3094">
              </div>
              
              <div class="nvd-grid-controls">
                <div class="nvd-input-group" style="margin-bottom: 0;">
                  <label for="nvd-resultsPerPage">Results Per Page:</label>
                  <select id="nvd-resultsPerPage">
                    <option value="10">10 results</option>
                    <option value="20" selected>20 results</option>
                    <option value="50">50 results</option>
                    <option value="100">100 results</option>
                  </select>
                </div>
                
                <div class="nvd-input-group" style="margin-bottom: 0;">
                  <label for="nvd-cvssFilter">CVSS Severity Filter:</label>
                  <select id="nvd-cvssFilter">
                    <option value="">All Severities</option>
                    <option value="CRITICAL">Critical (9.0-10.0)</option>
                    <option value="HIGH">High (7.0-8.9)</option>
                    <option value="MEDIUM">Medium (4.0-6.9)</option>
                    <option value="LOW">Low (0.1-3.9)</option>
                  </select>
                </div>
                
                <div class="nvd-input-group" style="margin-bottom: 0;">
                  <label for="nvd-sortBy">Sort By:</label>
                  <select id="nvd-sortBy">
                    <option value="published" selected>Published Date</option>
                    <option value="modified">Last Modified</option>
                  </select>
                </div>
              </div>
              
              <button onclick="nvdTool.searchNVD()" id="nvd-searchBtn" class="nvd-button">Search NVD Database</button>
            </div>
            
            <div id="nvd-results" class="nvd-results-container"></div>
          </div>
        </div>
      </div>

      <!-- GHSA Tracker Sub-tab -->
      <div id="ghsa" class="cve-sub-tab">
        <div class="cve-tracker-container">
          <div class="cve-header">
            <h1>📅 GitHub Security Advisory Calendar</h1>
            <p>Interactive vulnerability timeline and analysis</p>
          </div>

          <div class="cve-controls">
            <div class="cve-filter-group">
              <label class="cve-filter-label">Severity:</label>
              <select id="cve-severity-filter" class="cve-filter-select">
                <option value="">All Severities</option>
                <option value="critical">Critical</option>
                <option value="high">High</option>
                <option value="medium">Medium</option>
                <option value="low">Low</option>
              </select>
            </div>
            <div class="cve-filter-group">
              <label class="cve-filter-label">Type:</label>
              <select id="cve-type-filter" class="cve-filter-select">
                <option value="reviewed">Reviewed</option>
                <option value="unreviewed">Unreviewed</option>
                <option value="malware">Malware</option>
              </select>
            </div>
            <div class="cve-calendar-nav">
              <button class="cve-nav-btn" onclick="cveTool.changeMonth(-1)">‹ Prev</button>
              <div class="cve-current-month" id="cve-current-month-container">
                <div class="cve-month-text" id="cve-current-month">Loading...</div>
                <div class="cve-year-text" id="cve-current-year" onclick="cveTool.toggleYearPicker()">2025</div>
                <div class="cve-year-picker" id="cve-year-picker"></div>
              </div>
              <button class="cve-nav-btn" onclick="cveTool.changeMonth(1)">Next ›</button>
            </div>
          </div>

          <div class="cve-dashboard">
            <!-- Main Panel - Calendar -->
            <div class="cve-main-panel">
              <div class="cve-panel-header">
                <div class="cve-panel-title">
                  <span>📅</span>
                  Security Advisory Calendar
                </div>
                <div id="cve-github-status" class="cve-api-status cve-api-error">Loading</div>
              </div>
              
              <div class="cve-calendar-container">
                <div id="cve-calendar-content" class="cve-loading">
                  <div class="cve-spinner"></div>
                  Loading security advisory data...
                </div>
              </div>
            </div>

            <!-- Side Panel - Selected Date Details -->
            <div class="cve-side-panel">
              <div class="cve-panel-header">
                <div class="cve-panel-title">
                  <span>🔍</span>
                  Advisory Details
                </div>
              </div>
              
              <div class="cve-stats-summary">
                <div class="cve-stat-box">
                  <div class="cve-stat-number" id="cve-critical-count">0</div>
                  <div class="cve-stat-label">Critical</div>
                </div>
                <div class="cve-stat-box">
                  <div class="cve-stat-number" id="cve-high-count">0</div>
                  <div class="cve-stat-label">High</div>
                </div>
              </div>
              
              <div id="cve-advisory-details" style="flex: 1; overflow-y: auto; display: flex; flex-direction: column;">
                <div class="cve-no-advisories">
                  Click on a calendar date to view security advisories for that day
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- MSRC Tracker Sub-tab -->
      <div id="msrc" class="cve-sub-tab">
        <div class="msrc-tracker-container">
          <div class="msrc-header">
            <h1>Microsoft Security Response Center</h1>
            <p>CVE Dashboard - MSRC API Integration Page</p>
            <div class="msrc-loading" id="msrc-loading">
              <div class="msrc-spinner"></div>
            </div>
          </div>

          <div class="msrc-api-info">
            <p>The MSRC API doesn't allow direct browser calls, so this tab goes through a small Cloudflare Worker proxy (or the public <code>CorsProxy.io</code> if no Worker is configured).</p>
            <p><strong>Note:</strong> a full month of MSRC data is large (~20&nbsp;MB), so loading can take a few seconds.</p>
          </div>

          <div class="msrc-controls">
            <div class="msrc-stats">
              <div class="msrc-stat-item">
                <div class="msrc-stat-number" id="msrc-totalCves">-</div>
                <div class="msrc-stat-label">Total CVEs</div>
              </div>
              <div class="msrc-stat-item">
                <div class="msrc-stat-number" id="msrc-criticalCount">-</div>
                <div class="msrc-stat-label">Critical</div>
              </div>
              <div class="msrc-stat-item">
                <div class="msrc-stat-number" id="msrc-apiCalls">0</div>
                <div class="msrc-stat-label">API Calls</div>
              </div>
            </div>
          </div>

          <div class="msrc-demo-section">
            <h2>Microsoft Security Updates Browser</h2>
            
            <div class="msrc-demo-controls">
              <button class="msrc-demo-btn" onclick="msrcTool.previousMonth()">← Previous Month</button>
              <select class="msrc-month-selector" id="msrc-monthSelector" onchange="msrcTool.onMonthSelectorChange()">
                <!-- Dynamically populated -->
              </select>
              <button class="msrc-demo-btn" onclick="msrcTool.nextMonth()">Next Month →</button>
              <button class="msrc-demo-btn msrc-primary" onclick="msrcTool.fetchMonthData()">Load Security Updates</button>
            </div>

            <div class="msrc-filter-controls" id="msrc-filterControls" style="display: none;">
              <div class="msrc-filter-group">
                <label for="msrc-severityFilter">Severity:</label>
                <select class="msrc-filter-select" id="msrc-severityFilter" onchange="msrcTool.applyFilters()">
                  <option value="all">All Severities</option>
                  <option value="critical">Critical Only</option>
                  <option value="important">Important Only</option>
                  <option value="moderate">Moderate Only</option>
                  <option value="low">Low Only</option>
                </select>
              </div>
              <div class="msrc-filter-group">
                <label for="msrc-pageSize">Show:</label>
                <select class="msrc-filter-select" id="msrc-pageSize" onchange="msrcTool.applyFilters()">
                  <option value="20">20 per page</option>
                  <option value="50">50 per page</option>
                  <option value="100">100 per page</option>
                  <option value="all">All results</option>
                </select>
              </div>
              <div class="msrc-filter-group">
                <button class="msrc-demo-btn" onclick="msrcTool.resetFilters()">Reset Filters</button>
              </div>
            </div>

            <div id="msrc-resultsSummary" style="display: none;"></div>
            <div id="msrc-messageArea"></div>
            
            <div class="msrc-cve-grid" id="msrc-cveGrid">
              <div class="msrc-no-data">
                Select a month and click "Load Security Updates" to fetch CVE data.
              </div>
            </div>
            
            <div class="msrc-pagination" id="msrc-pagination" style="display: none;">
              <button class="msrc-pagination-btn" id="msrc-prevPage" onclick="msrcTool.changePage(-1)">Previous</button>
              <span class="msrc-pagination-info" id="msrc-paginationInfo"></span>
              <button class="msrc-pagination-btn" id="msrc-nextPage" onclick="msrcTool.changePage(1)">Next</button>
            </div>
          </div>
        </div>
      </div>

      <!-- Shodan CVEDB Sub-tab -->
      <div id="shodan" class="cve-sub-tab">
        <div class="shodan-container">
          <div class="shodan-inner-container">
            <div class="shodan-header">
              <h1>CVEDB Dashboard</h1>
              <p>Powered by Shodan - CVE Lookup with EPSS Risk Intelligence & KEV Status</p>
            </div>

            <div class="shodan-search-section">
              <div class="shodan-search-controls">
                <div class="shodan-form-group">
                  <label for="shodan-searchQuery">CVE ID</label>
                  <input type="text" id="shodan-searchQuery" placeholder="Enter CVE-2024-1234...">
                </div>
                <button class="shodan-search-btn" onclick="shodanTool.performSearch()">Search</button>
              </div>

              <div class="shodan-disclaimer">
                The CVEDB API doesn't allow direct browser calls, so lookups go through a small Cloudflare Worker proxy (or the public <code>CorsProxy.io</code> if no Worker is configured).
              </div>
            </div>

            <div class="shodan-results-section">
              <div id="shodan-results">
                <div class="shodan-no-results">
                  <h3>Welcome to CVEDB Dashboard</h3>
                  <p>Search for vulnerabilities by CVE ID to get started.</p>
                  <p><strong>Examples:</strong> CVE-2024-21413, CVE-2021-44228, CVE-2023-23397</p>
                </div>
              </div>
            </div>
          </div>
        </div>
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

<!-- NVD Popup Overlay - Moved outside dashboard-content to avoid width restrictions -->
<div id="nvd-popupOverlay" class="nvd-popup-overlay" onclick="nvdTool.closePopup(event)">
  <div class="nvd-popup-content" onclick="event.stopPropagation()">
    <button class="nvd-popup-close" onclick="nvdTool.closePopup()">&times;</button>
    <div class="nvd-popup-body">
      <div id="nvd-popupContent"></div>
    </div>
  </div>
</div>

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
      setTimeout(() => {
        cveTool.initDashboard();
        msrcTool.init();
        nvdTool.init();
        shodanTool.init();
      }, 100);
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
      nvdTool.closePopup();
    }
  });

  // NVD Tool functionality
  const nvdTool = {
    currentResults: [],
    totalResults: 0,
    currentPage: 0,
    currentSearch: null,

    init: function() {
      console.log('Initializing NVD Tool...');
      this.updatePlaceholder();
      
      // Add event listeners
      document.getElementById('nvd-searchInput').addEventListener('keypress', (e) => {
        if (e.key === 'Enter') {
          this.searchNVD();
        }
      });
    },

    async searchNVD() {
      const searchType = document.getElementById('nvd-searchType').value;
      const searchInput = document.getElementById('nvd-searchInput').value.trim();
      const resultsPerPage = parseInt(document.getElementById('nvd-resultsPerPage').value);
      const cvssFilter = document.getElementById('nvd-cvssFilter').value;
      const resultsDiv = document.getElementById('nvd-results');
      const searchBtn = document.getElementById('nvd-searchBtn');
      
      if (!searchInput) {
        this.showError('Please enter search criteria');
        return;
      }
      
      // Reset pagination
      this.currentPage = 0;
      this.currentResults = [];
      this.currentSearch = { searchType, searchInput, resultsPerPage, cvssFilter };
      
      // Show loading
      resultsDiv.style.display = 'block';
      resultsDiv.innerHTML = '<div class="nvd-loading">🔍 Searching NIST NVD database...</div>';
      searchBtn.disabled = true;
      
      try {
        let apiUrl;
        
        switch(searchType) {
          case 'cve':
            if (!searchInput.match(/^CVE-\d{4}-\d+$/)) {
              this.showError('Please enter a valid CVE ID (format: CVE-YYYY-NNNN)');
              return;
            }
            apiUrl = `https://services.nvd.nist.gov/rest/json/cves/2.0?cveId=${searchInput}`;
            break;
            
          case 'keyword':
            apiUrl = `https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=${encodeURIComponent(searchInput)}&resultsPerPage=${resultsPerPage}`;
            if (cvssFilter) {
              apiUrl += `&cvssV3Severity=${cvssFilter}`;
            }
            break;
        }
        
        const response = await fetch(apiUrl);
        
        if (!response.ok) {
          throw new Error(`HTTP ${response.status}: ${response.statusText}`);
        }
        
        const data = await response.json();
        this.currentResults = data.vulnerabilities || [];
        this.totalResults = data.totalResults || 0;
        
        this.displayResults();
        
      } catch (error) {
        console.error('NVD API error:', error);
        this.showError(`Search failed: ${error.message}`);
      } finally {
        searchBtn.disabled = false;
      }
    },

    displayResults() {
      const resultsDiv = document.getElementById('nvd-results');
      
      if (this.currentResults.length === 0) {
        this.showError('No vulnerabilities found for your search criteria');
        return;
      }
      
      let html = '';
      
      // Show limitation note for keyword searches
      if (this.currentSearch.searchType === 'keyword') {
        html += `
          <div style="background: color-mix(in srgb, var(--db-med) 10%, transparent); border: 1px solid var(--db-med); border-radius: 4px; padding: 10px 14px; margin-bottom: 14px;">
            <strong>ℹ️ Search Limitations:</strong> Keyword Search may not find all relevant CVEs - searches description text but not all product names
          </div>
        `;
      }
      
      // Search results header
      html += `
        <div style="margin-bottom: 16px; padding: 10px 14px; background: var(--db-tint); border: 1px solid var(--border); border-radius: 4px; border-left: 3px solid var(--accent);">
          <strong>📊 Search Results:</strong> Found ${this.totalResults.toLocaleString()} vulnerabilities
          <br><small>Showing ${this.currentResults.length} results</small>
        </div>
      `;
      
      // Add vulnerability cards
      this.currentResults.forEach(vuln => {
        const cve = vuln.cve;
        html += this.createCompactCard(cve);
      });
      
      // Add pagination for multi-page results
      if (this.totalResults > this.currentSearch.resultsPerPage) {
        const totalPages = Math.ceil(this.totalResults / this.currentSearch.resultsPerPage);
        const hasNext = (this.currentPage + 1) * this.currentSearch.resultsPerPage < this.totalResults;
        
        html += `
          <div style="text-align: center; margin-top: 20px; padding: 14px; background: var(--bg); border: 1px solid var(--border); border-radius: 4px;">
            <div style="display: flex; justify-content: center; align-items: center; gap: 15px; flex-wrap: wrap; margin-bottom: 15px;">
              <button onclick="nvdTool.goToPage(${this.currentPage - 1})" ${this.currentPage === 0 ? 'disabled' : ''} 
                      style="padding: 10px 20px;">← Previous</button>
              
              <span style="color: var(--text-dim); font-weight: 600;">
                Page ${this.currentPage + 1} of ${totalPages}
              </span>
              
              <button onclick="nvdTool.goToPage(${this.currentPage + 1})" ${!hasNext ? 'disabled' : ''} 
                      style="padding: 10px 20px;">Next →</button>
            </div>
            
            <div style="color: var(--text-dim); font-size: 0.8rem;">
              Showing ${this.currentResults.length} of ${this.totalResults.toLocaleString()} total results
            </div>
          </div>
        `;
      }
      
      resultsDiv.innerHTML = html;
    },

    async goToPage(pageNumber) {
      if (pageNumber < 0) return;
      
      const startIndex = pageNumber * this.currentSearch.resultsPerPage;
      if (startIndex >= this.totalResults) return;
      
      this.currentPage = pageNumber;
      
      const resultsDiv = document.getElementById('nvd-results');
      resultsDiv.innerHTML = '<div class="nvd-loading">📖 Loading page ' + (pageNumber + 1) + '...</div>';
      
      try {
        let apiUrl;
        
        switch(this.currentSearch.searchType) {
          case 'keyword':
            apiUrl = `https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=${encodeURIComponent(this.currentSearch.searchInput)}&resultsPerPage=${this.currentSearch.resultsPerPage}&startIndex=${startIndex}`;
            if (this.currentSearch.cvssFilter) {
              apiUrl += `&cvssV3Severity=${this.currentSearch.cvssFilter}`;
            }
            break;
            
          default:
            return;
        }
        
        const response = await fetch(apiUrl);
        if (!response.ok) {
          throw new Error(`HTTP ${response.status}: ${response.statusText}`);
        }
        
        const data = await response.json();
        this.currentResults = data.vulnerabilities || [];
        
        this.displayResults();
        
        // Scroll to top of results
        document.getElementById('nvd-results').scrollIntoView({ behavior: 'smooth' });
        
      } catch (error) {
        this.showError(`Failed to load page: ${error.message}`);
      }
    },

    createCompactCard(cve) {
      const cvssData = this.extractCVSSData(cve);
      const cvssClass = this.getCVSSClass(cvssData.score);
      const description = cve.descriptions?.find(d => d.lang === 'en')?.value || 'No description available';
      const publishedDate = cve.published ? new Date(cve.published).toLocaleDateString('en-GB') : 'Unknown';
      
      return `
        <div class="nvd-vulnerability-card" onclick="nvdTool.showCVEDetails('${cve.id.replace(/'/g, "\\'")}')">
          <div class="nvd-card-header">
            <div class="nvd-cve-id">${cve.id}</div>
            ${cvssData.score ? `<div class="nvd-cvss-badge ${cvssClass}">${cvssData.severity} - ${cvssData.score}</div>` : ''}
          </div>
          
          <div class="nvd-card-description">
            ${description}
          </div>
          
          <div class="nvd-card-meta">
            <div>
              <span>📅 ${publishedDate}</span>
              <span style="margin-left: 15px;">🔗 ${cve.references?.length || 0} refs</span>
            </div>
            <div class="nvd-click-hint">Click for details</div>
          </div>
        </div>
      `;
    },

    showCVEDetails(cveId) {
      const cve = this.currentResults.find(vuln => vuln.cve.id === cveId)?.cve;
      if (!cve) return;
      
      const cvssData = this.extractCVSSData(cve);
      const cvssClass = this.getCVSSClass(cvssData.score);
      const description = cve.descriptions?.find(d => d.lang === 'en')?.value || 'No description available';
      
      const publishedDate = cve.published ? new Date(cve.published).toLocaleDateString('en-GB', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }) : 'Unknown';
      
      const modifiedDate = cve.lastModified ? new Date(cve.lastModified).toLocaleDateString('en-GB', {
        year: 'numeric', 
        month: 'long',
        day: 'numeric'
      }) : 'Unknown';
      
      const popupContentHTML = `
        <div>
          <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; flex-wrap: wrap; gap: 15px;">
            <h2 style="color: var(--accent); margin: 0; font-size: 1.2rem;">${cve.id}</h2>
            <div style="display: flex; gap: 10px;">
              ${cvssData.score ? `<div class="nvd-cvss-badge ${cvssClass}">${cvssData.severity} - ${cvssData.score}</div>` : ''}
              ${cvssData.version ? `<div class="nvd-cvss-badge nvd-cvss-none">CVSS ${cvssData.version}</div>` : ''}
            </div>
          </div>
          
          <div style="margin-bottom: 25px;">
            <h3 style="margin-bottom: 10px; color: var(--heading); font-size: 1rem;">🔍 Full Description</h3>
            <div style="line-height: 1.6; color: var(--text); font-size: 0.9rem; padding: 14px; background: var(--chrome); border: 1px solid var(--border); border-radius: 4px; border-left: 3px solid var(--accent);">
              ${description}
            </div>
          </div>
          
          <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px; margin-bottom: 25px;">
            <div style="background: var(--chrome); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px;">
              <div style="font-weight: 600; color: var(--text-dim); margin-bottom: 4px; font-size: 0.72rem;">📅 PUBLISHED</div>
              <div style="color: var(--heading);">${publishedDate}</div>
            </div>
            
            <div style="background: var(--chrome); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px;">
              <div style="font-weight: 600; color: var(--text-dim); margin-bottom: 4px; font-size: 0.72rem;">📄 MODIFIED</div>
              <div style="color: var(--heading);">${modifiedDate}</div>
            </div>
            
            <div style="background: var(--chrome); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px;">
              <div style="font-weight: 600; color: var(--text-dim); margin-bottom: 4px; font-size: 0.72rem;">⚡ CVSS SCORE</div>
              <div style="color: var(--heading);">${cvssData.score || 'Not scored'}</div>
            </div>
            
            <div style="background: var(--chrome); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px;">
              <div style="font-weight: 600; color: var(--text-dim); margin-bottom: 4px; font-size: 0.72rem;">🎯 SEVERITY</div>
              <div style="color: var(--heading);">${cvssData.severity || 'Unknown'}</div>
            </div>
          </div>
          
          ${cvssData.vector ? `
            <div style="margin-bottom: 25px;">
              <h3 style="margin-bottom: 10px; color: var(--heading); font-size: 1rem;">🔢 CVSS Vector</h3>
              <div style="background: var(--chrome); color: var(--text); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px; font-size: 0.8rem; word-break: break-all;">
                ${cvssData.vector}
              </div>
            </div>
          ` : ''}
          
          ${cve.references && cve.references.length > 0 ? `
            <div>
              <h3 style="margin-bottom: 10px; color: var(--heading); font-size: 1rem;">🔗 References (${cve.references.length})</h3>
              <div style="max-height: 200px; overflow-y: auto; background: var(--chrome); border: 1px solid var(--border); padding: 10px 12px; border-radius: 4px;">
                ${cve.references.map(ref => 
                  `<a href="${ref.url}" target="_blank" style="display: block; color: var(--accent); text-decoration: none; margin: 5px 0; padding: 6px 10px; background: var(--bg); border: 1px solid var(--border); border-radius: 3px; word-break: break-all; font-size: 0.8rem;" onmouseover="this.style.background='#dbeafe'" onmouseout="this.style.background='white'">
                    ${ref.url.length > 70 ? ref.url.substring(0, 70) + '...' : ref.url}
                  </a>`
                ).join('')}
              </div>
            </div>
          ` : ''}
        </div>
      `;
      
      // Set popup content
      document.getElementById('nvd-popupContent').innerHTML = popupContentHTML;
      
      // Show popup using exact same method as recipe modal
      const popup = document.getElementById('nvd-popupOverlay');
      popup.style.display = 'block';
      document.body.style.overflow = 'hidden';
    },

    closePopup(event) {
      if (event && event.target !== document.getElementById('nvd-popupOverlay')) return;
      
      document.getElementById('nvd-popupOverlay').style.display = 'none';
      document.body.style.overflow = 'auto';
    },

    extractCVSSData(cve) {
      let cvssData = { score: null, severity: null, vector: null, version: null };
      
      const metrics = cve.metrics;
      if (metrics?.cvssMetricV31 && metrics.cvssMetricV31.length > 0) {
        const cvss = metrics.cvssMetricV31[0].cvssData;
        cvssData = {
          score: cvss.baseScore,
          severity: cvss.baseSeverity,
          vector: cvss.vectorString,
          version: '3.1'
        };
      } else if (metrics?.cvssMetricV30 && metrics.cvssMetricV30.length > 0) {
        const cvss = metrics.cvssMetricV30[0].cvssData;
        cvssData = {
          score: cvss.baseScore,
          severity: cvss.baseSeverity,
          vector: cvss.vectorString,
          version: '3.0'
        };
      } else if (metrics?.cvssMetricV2 && metrics.cvssMetricV2.length > 0) {
        const cvss = metrics.cvssMetricV2[0].cvssData;
        cvssData = {
          score: cvss.baseScore,
          severity: this.getSeverityFromV2Score(cvss.baseScore),
          vector: cvss.vectorString,
          version: '2.0'
        };
      }
      
      return cvssData;
    },

    getSeverityFromV2Score(score) {
      if (score >= 7.0) return 'HIGH';
      if (score >= 4.0) return 'MEDIUM';
      return 'LOW';
    },

    getCVSSClass(score) {
      if (!score) return 'nvd-cvss-none';
      if (score >= 9.0) return 'nvd-cvss-critical';
      if (score >= 7.0) return 'nvd-cvss-high';
      if (score >= 4.0) return 'nvd-cvss-medium';
      return 'nvd-cvss-low';
    },

    showError(message) {
      const resultsDiv = document.getElementById('nvd-results');
      resultsDiv.style.display = 'block';
      resultsDiv.innerHTML = `<div class="nvd-error">⚠ ${message}</div>`;
    },

    updatePlaceholder() {
      const searchType = document.getElementById('nvd-searchType').value;
      const input = document.getElementById('nvd-searchInput');
      
      switch(searchType) {
        case 'cve':
          input.placeholder = 'CVE-2024-3094';
          break;
        case 'keyword':
          input.placeholder = 'log4j, openssl, apache, etc.';
          break;
      }
    }
  };

  // CVE Tracker functionality (GHSA)
  const cveTool = {
    currentDate: new Date(),
    advisoriesData: [],
    advisoriesByDate: {},
    selectedDate: null,
    isLoading: false,

    toggleYearPicker: function() {
      const yearPicker = document.getElementById('cve-year-picker');
      const isVisible = yearPicker.classList.contains('cve-show');
      
      if (isVisible) {
        yearPicker.classList.remove('cve-show');
      } else {
        const currentYear = new Date().getFullYear();
        const displayedYear = this.currentDate.getFullYear();
        
        const startYear = currentYear - 10;
        const endYear = currentYear + 5;
        
        let yearHTML = '';
        for (let year = endYear; year >= startYear; year--) {
          const isDisplayedYear = year === displayedYear;
          yearHTML += `
            <div class="cve-year-option ${isDisplayedYear ? 'cve-current' : ''}" 
                 onclick="cveTool.selectYear(${year})">${year}</div>
          `;
        }
        
        yearPicker.innerHTML = yearHTML;
        yearPicker.classList.add('cve-show');
      }
    },

    selectYear: function(year) {
      this.currentDate.setFullYear(year);
      document.getElementById('cve-year-picker').classList.remove('cve-show');
      this.loadAdvisoriesForMonth();
    },

    generateCalendar: function(year, month) {
      const firstDay = new Date(year, month, 1);
      const lastDay = new Date(year, month + 1, 0);
      const firstDayOfWeek = firstDay.getDay();
      const daysInMonth = lastDay.getDate();
      
      const monthNames = [
        'January', 'February', 'March', 'April', 'May', 'June',
        'July', 'August', 'September', 'October', 'November', 'December'
      ];
      
      document.getElementById('cve-current-month').textContent = monthNames[month];
      document.getElementById('cve-current-year').textContent = year;

      let calendarHTML = `
        <div class="cve-calendar-grid">
          <div class="cve-calendar-header">Sun</div>
          <div class="cve-calendar-header">Mon</div>
          <div class="cve-calendar-header">Tue</div>
          <div class="cve-calendar-header">Wed</div>
          <div class="cve-calendar-header">Thu</div>
          <div class="cve-calendar-header">Fri</div>
          <div class="cve-calendar-header">Sat</div>
      `;

      // Previous month's trailing days
      const prevMonth = new Date(year, month - 1, 0);
      for (let i = firstDayOfWeek - 1; i >= 0; i--) {
        const day = prevMonth.getDate() - i;
        calendarHTML += `
          <div class="cve-calendar-day other-month">
            <div class="cve-day-number">${day}</div>
          </div>
        `;
      }

      // Current month days
      const today = new Date();
      for (let day = 1; day <= daysInMonth; day++) {
        const currentDateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        const advisoryCount = this.advisoriesByDate[currentDateStr] ? this.advisoriesByDate[currentDateStr].length : 0;
        
        const isToday = today.getFullYear() === year && 
                       today.getMonth() === month && 
                       today.getDate() === day;
        
        const heatLevel = Math.min(Math.floor(advisoryCount / 3) + (advisoryCount > 0 ? 1 : 0), 5);
        const todayClass = isToday ? 'today' : '';
        
        calendarHTML += `
          <div class="cve-calendar-day cve-day-heat-${heatLevel} ${todayClass}" 
               onclick="cveTool.selectDate('${currentDateStr}')"
               data-date="${currentDateStr}">
            <div class="cve-day-number">${day}</div>
            ${advisoryCount > 0 ? `<div class="cve-day-count">${advisoryCount}</div>` : ''}
          </div>
        `;
      }

      // Next month's leading days
      const remainingCells = 42 - (firstDayOfWeek + daysInMonth);
      for (let day = 1; day <= remainingCells && remainingCells < 7; day++) {
        calendarHTML += `
          <div class="cve-calendar-day other-month">
            <div class="cve-day-number">${day}</div>
          </div>
        `;
      }

      calendarHTML += '</div>';
      document.getElementById('cve-calendar-content').innerHTML = calendarHTML;
    },

    changeMonth: function(direction) {
      if (this.isLoading) return;
      this.currentDate.setMonth(this.currentDate.getMonth() + direction);
      this.loadAdvisoriesForMonth();
    },

    selectDate: function(dateStr) {
      document.querySelectorAll('.cve-calendar-day.selected').forEach(el => {
        el.classList.remove('selected');
      });
      
      const dayElement = document.querySelector(`[data-date="${dateStr}"]`);
      if (dayElement) {
        dayElement.classList.add('selected');
      }
      
      this.selectedDate = dateStr;
      this.displayAdvisoriesForDate(dateStr);
    },

    displayAdvisoriesForDate: function(dateStr) {
      const advisories = this.advisoriesByDate[dateStr] || [];
      const formattedDate = new Date(dateStr + 'T00:00:00').toLocaleDateString('en-US', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      });

      let html = `
        <div class="cve-selected-date-info">
          <div class="cve-selected-date">${formattedDate}</div>
          <div class="cve-date-summary">${advisories.length} security advisories</div>
        </div>
      `;

      if (advisories.length === 0) {
        html += '<div class="cve-no-advisories">No security advisories published on this date</div>';
      } else {
        html += '<div class="cve-advisory-list" style="flex: 1; overflow-y: auto;">';
        advisories.forEach((advisory, index) => {
          const severity = advisory.severity || 'unknown';
          const severityClass = `cve-severity-${severity.toLowerCase()}`;
          const cveId = advisory.cve_id || advisory.identifiers?.find(id => id.type === 'CVE')?.value || null;
          
          html += `
            <div class="cve-advisory-item" onclick="cveTool.toggleAdvisoryDetails(${index}, '${dateStr}')">
              <div class="cve-advisory-header">
                <div class="cve-advisory-title">
                  <div class="cve-advisory-id">${advisory.ghsa_id}</div>
                  ${cveId ? `<div class="cve-id">${cveId}</div>` : ''}
                </div>
                <div class="cve-severity-badge ${severityClass}">${severity}</div>
              </div>
              
              <div class="cve-advisory-summary">
                ${advisory.summary}
              </div>
              
              <div class="cve-advisory-details" id="cve-details-${dateStr}-${index}">
                ${advisory.cvss?.score ? `
                  <div class="cve-detail-row">
                    <div class="cve-detail-label">CVSS:</div>
                    <div class="cve-detail-value">${advisory.cvss.score}/10</div>
                  </div>
                ` : ''}
                ${advisory.cwes?.length ? `
                  <div class="cve-detail-row">
                    <div class="cve-detail-label">CWEs:</div>
                    <div class="cve-detail-value">${advisory.cwes.slice(0, 2).map(cwe => cwe.name).join(', ')}</div>
                  </div>
                ` : ''}
                ${advisory.vulnerabilities?.length ? `
                  <div class="cve-detail-row">
                    <div class="cve-detail-label">Affected:</div>
                    <div class="cve-detail-value">${advisory.vulnerabilities[0].package?.name} (${advisory.vulnerabilities[0].package?.ecosystem})</div>
                  </div>
                ` : ''}
                ${advisory.html_url ? `
                  <a href="${advisory.html_url}" target="_blank" class="cve-external-link">
                    View Full Advisory →
                  </a>
                ` : ''}
              </div>
            </div>
          `;
        });
        html += '</div>';
      }

      const advisoryDetailsContainer = document.getElementById('cve-advisory-details');
      advisoryDetailsContainer.innerHTML = html;
      advisoryDetailsContainer.style.flex = '1';
      advisoryDetailsContainer.style.overflowY = 'auto';
      advisoryDetailsContainer.style.display = 'flex';
      advisoryDetailsContainer.style.flexDirection = 'column';
    },

    toggleAdvisoryDetails: function(index, dateStr) {
      const details = document.getElementById(`cve-details-${dateStr}-${index}`);
      const item = details.closest('.cve-advisory-item');
      
      if (details.classList.contains('cve-show')) {
        details.classList.remove('cve-show');
        item.classList.remove('expanded');
      } else {
        document.querySelectorAll('.cve-advisory-details.cve-show').forEach(el => {
          el.classList.remove('cve-show');
          if (el.closest('.cve-advisory-item')) {
            el.closest('.cve-advisory-item').classList.remove('expanded');
          }
        });
        
        details.classList.add('cve-show');
        item.classList.add('expanded');
      }
    },

    loadAdvisoriesForMonth: async function() {
      if (this.isLoading) return;
      this.isLoading = true;

      try {
        const year = this.currentDate.getFullYear();
        const month = this.currentDate.getMonth();
        
        const startDate = `${year}-${String(month + 1).padStart(2, '0')}-01`;
        const endDate = `${year}-${String(month + 1).padStart(2, '0')}-${new Date(year, month + 1, 0).getDate()}`;
        
        const severity = document.getElementById('cve-severity-filter').value;
        const type = document.getElementById('cve-type-filter').value;
        
        console.log('🔍 Fetching CVE advisories for date range:', { startDate, endDate, severity, type });
        
        this.advisoriesData = [];
        this.advisoriesByDate = {};
        
        let baseUrl = `https://api.github.com/advisories?published=${startDate}..${endDate}&sort=published&direction=desc`;
        if (severity) baseUrl += `&severity=${severity}`;
        if (type) baseUrl += `&type=${type}`;
        
        let page = 1;
        let hasMore = true;
        const maxPages = 5;
        
        while (hasMore && page <= maxPages) {
          const url = `${baseUrl}&per_page=100&page=${page}`;
          console.log(`📄 Fetching CVE page ${page}...`);
          
          if (page > 1) {
            await new Promise(resolve => setTimeout(resolve, 200));
          }
          
          const response = await fetch(url);
          
          if (!response.ok) {
            if (response.status === 403) {
              throw new Error(`Rate limit exceeded. Please wait a moment and try again.`);
            }
            throw new Error(`GitHub API returned ${response.status}: ${response.statusText}`);
          }
          
          const data = await response.json();
          
          if (data.length === 0) {
            hasMore = false;
          } else {
            this.advisoriesData.push(...data);
            
            const linkHeader = response.headers.get('Link');
            hasMore = linkHeader && linkHeader.includes('rel="next"');
            page++;
          }
        }
        
        console.log(`✅ Successfully loaded ${this.advisoriesData.length} CVE advisories from ${page - 1} pages`);
        
        this.processAdvisoriesData();
        
        document.getElementById('cve-github-status').className = 'cve-api-status cve-api-live';
        document.getElementById('cve-github-status').textContent = 'Live';
        
        this.generateCalendar(year, month);
        this.updateStats();
        
      } catch (error) {
        console.error('⚠ GitHub CVE API Error:', error);
        document.getElementById('cve-calendar-content').innerHTML = `
          <div class="cve-error">
            <strong>Unable to load security advisories</strong><br>
            ${error.message}
          </div>
        `;
        document.getElementById('cve-github-status').className = 'cve-api-status cve-api-error';
        document.getElementById('cve-github-status').textContent = 'Error';
      } finally {
        this.isLoading = false;
      }
    },

    processAdvisoriesData: function() {
      this.advisoriesByDate = {};
      
      this.advisoriesData.forEach(advisory => {
        const publishedDate = new Date(advisory.published_at).toISOString().split('T')[0];
        
        if (!this.advisoriesByDate[publishedDate]) {
          this.advisoriesByDate[publishedDate] = [];
        }
        
        this.advisoriesByDate[publishedDate].push(advisory);
      });
    },

    updateStats: function() {
      const criticalCount = this.advisoriesData.filter(advisory => 
        (advisory.severity || '').toLowerCase() === 'critical'
      ).length;
      
      const highCount = this.advisoriesData.filter(advisory => 
        (advisory.severity || '').toLowerCase() === 'high'
      ).length;
      
      document.getElementById('cve-critical-count').textContent = criticalCount;
      document.getElementById('cve-high-count').textContent = highCount;
    },

    initDashboard: async function() {
      console.log('🚀 Initializing CVE tracker dashboard...');
      
      document.addEventListener('click', (event) => {
        const yearPicker = document.getElementById('cve-year-picker');
        const monthContainer = document.getElementById('cve-current-month-container');
        
        if (yearPicker && monthContainer && !monthContainer.contains(event.target)) {
          yearPicker.classList.remove('cve-show');
        }
      });
      
      await this.loadAdvisoriesForMonth();
      
      console.log('✅ CVE Dashboard initialization complete');
    }
  };

  // MSRC Tracker functionality
  const msrcTool = {
    apiCallCount: 0,
    currentCveData: [],
    filteredCveData: [],
    currentDate: new Date(),
    currentPage: 1,
    pageSize: 20,

    monthNames: ['January', 'February', 'March', 'April', 'May', 'June',
                'July', 'August', 'September', 'October', 'November', 'December'],

    showLoading: function(show = true) {
      document.getElementById('msrc-loading').style.display = show ? 'block' : 'none';
    },

    updateApiCallCount: function() {
      document.getElementById('msrc-apiCalls').textContent = this.apiCallCount;
    },

    showMessage: function(message, type = 'info') {
      const messageArea = document.getElementById('msrc-messageArea');
      if (!messageArea) return;
      
      if (!message || message === '') {
        messageArea.innerHTML = '';
        messageArea.style.display = 'none';
        return;
      }
      
      const className = type === 'error' ? 'msrc-error' : type === 'success' ? 'msrc-success' : 'msrc-api-info';
      messageArea.innerHTML = `<div class="${className}">${message}</div>`;
      messageArea.style.display = 'block';
    },

    populateMonthSelector: function() {
      const selector = document.getElementById('msrc-monthSelector');
      const options = [];

      for (let i = 0; i < 24; i++) {
        const date = new Date();
        date.setMonth(date.getMonth() - i);
        
        const year = date.getFullYear();
        const monthIndex = date.getMonth();
        const monthName = this.monthNames[monthIndex];
        
        const shortMonth = monthName.substring(0, 3);
        const apiFormat = `${year}-${shortMonth}`;
        const displayFormat = `${monthName} ${year}`;
        
        options.push({
          value: apiFormat,
          label: displayFormat,
          date: new Date(date)
        });
      }

      selector.innerHTML = options.map(opt => 
        `<option value="${opt.value}">${opt.label}</option>`
      ).join('');

      const currentYear = new Date().getFullYear();
      const currentMonthName = this.monthNames[new Date().getMonth()];
      const currentShort = currentMonthName.substring(0, 3);
      const currentApiFormat = `${currentYear}-${currentShort}`;
      
      selector.value = currentApiFormat;
      this.currentDate = new Date();
    },

    onMonthSelectorChange: function() {
      const selector = document.getElementById('msrc-monthSelector');
      const selectedValue = selector.value;
      
      const [year, shortMonth] = selectedValue.split('-');
      const monthIndex = this.monthNames.findIndex(month => month.startsWith(shortMonth));
      
      this.currentDate = new Date(parseInt(year), monthIndex, 1);
      
      console.log('Month selector changed:', selectedValue, '-> Date:', this.currentDate);
    },

    previousMonth: function() {
      this.currentDate.setMonth(this.currentDate.getMonth() - 1);
      this.updateMonthSelector();
    },

    nextMonth: function() {
      this.currentDate.setMonth(this.currentDate.getMonth() + 1);
      this.updateMonthSelector();
    },

    updateMonthSelector: function() {
      const selector = document.getElementById('msrc-monthSelector');
      const year = this.currentDate.getFullYear();
      const monthName = this.monthNames[this.currentDate.getMonth()];
      const shortMonth = monthName.substring(0, 3);
      const apiFormat = `${year}-${shortMonth}`;
      
      if (!selector.querySelector(`option[value="${apiFormat}"]`)) {
        const displayFormat = `${monthName} ${year}`;
        const option = new Option(displayFormat, apiFormat);
        selector.appendChild(option);
      }
      
      selector.value = apiFormat;
      console.log('Updated month selector to:', apiFormat);
    },

    getMSRCUrl: function(cveId) {
      return `https://msrc.microsoft.com/update-guide/vulnerability/${cveId}`;
    },

    fetchMonthData: async function() {
      const monthSelector = document.getElementById('msrc-monthSelector');
      const selectedMonth = monthSelector.value;
      
      if (!selectedMonth) {
        this.showMessage('Please select a month first.', 'error');
        return;
      }

      this.showLoading(true);
      this.showMessage('Fetching data from MSRC API via CORS proxy...', 'info');

      console.log('Fetching data for:', selectedMonth);

      try {
        const targetUrl = `https://api.msrc.microsoft.com/cvrf/v3.0/cvrf/${selectedMonth}`;
        const proxyUrl = proxied(targetUrl);

        console.log('Target URL:', targetUrl);

        const response = await fetch(proxyUrl, {
          headers: {
            'Accept': 'application/json',
            'Origin': window.location.origin
          },
          signal: AbortSignal.timeout(30000)
        });

        this.apiCallCount++;
        this.updateApiCallCount();

        if (!response.ok) {
          if (response.status === 404) {
            this.showMessage(`No security updates found for ${selectedMonth}. This month may not have any published updates yet.`, 'error');
            this.displayCVEs([]);
            return;
          }
          if (response.status === 429) {
            this.showMessage('Rate limit exceeded on the CORS proxy. Please wait a few minutes before trying again.', 'error');
            this.displayCVEs([]);
            return;
          }
          if (response.status >= 500) {
            this.showMessage('The CORS proxy service appears to be experiencing issues. You can try again later or access the data directly at <a href="https://msrc.microsoft.com/update-guide" target="_blank">Microsoft Security Update Guide</a>.', 'error');
            this.displayCVEs([]);
            return;
          }
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        const responseText = await response.text();
        
        if (responseText.trim().startsWith('<') || responseText.includes('<!DOCTYPE')) {
          if (responseText.includes('blocked') || responseText.includes('403') || responseText.includes('access denied')) {
            this.showMessage('Access blocked by CORS proxy. The service may have restrictions in your region. You can access the data directly at <a href="https://msrc.microsoft.com/update-guide" target="_blank">Microsoft Security Update Guide</a>.', 'error');
          } else {
            this.showMessage('The CORS proxy returned an error page instead of data. The service may be temporarily unavailable.', 'error');
          }
          this.displayCVEs([]);
          return;
        }

        const data = JSON.parse(responseText);
        console.log('MSRC API Response parsed successfully');

        if (!data.Vulnerability || !Array.isArray(data.Vulnerability)) {
          throw new Error('No Vulnerability array found in response');
        }

        console.log(`Found ${data.Vulnerability.length} vulnerabilities in API response`);
        const cves = this.parseMSRCData(data);
        this.currentCveData = cves;
        this.filteredCveData = [...cves];
        this.currentPage = 1;
        
        const filterControls = document.getElementById('msrc-filterControls');
        if (filterControls) {
          filterControls.style.display = cves.length > 0 ? 'flex' : 'none';
        }
        
        this.displayCurrentPage();
        this.updateStats();
        this.updateResultsSummary();

        this.showMessage('', 'info');

      } catch (error) {
        console.error('Error fetching CVE data:', error);
        
        if (error.name === 'AbortError') {
          this.showMessage('Request timed out. The CORS proxy service may be slow or unavailable. You can access the data directly at <a href="https://msrc.microsoft.com/update-guide" target="_blank">Microsoft Security Update Guide</a>.', 'error');
        } else if (error.message.includes('Failed to fetch') || error.message.includes('NetworkError')) {
          this.showMessage('Network error: Unable to reach the CORS proxy service. Please check your internet connection or try again later. Alternatively, visit <a href="https://msrc.microsoft.com/update-guide" target="_blank">Microsoft Security Update Guide</a> directly.', 'error');
        } else if (error.message.includes('JSON')) {
          this.showMessage('Invalid response format received from the API. The CORS proxy may be experiencing issues.', 'error');
        } else {
          this.showMessage(`Failed to fetch data: ${error.message}. If this persists, you can access the data directly at <a href="https://msrc.microsoft.com/update-guide" target="_blank">Microsoft Security Update Guide</a>.`, 'error');
        }
        
        this.displayCVEs([]);
      } finally {
        this.showLoading(false);
      }
    },

    parseMSRCData: function(data) {
      console.log('Parsing MSRC data...');
      
      if (!data.Vulnerability || !Array.isArray(data.Vulnerability)) {
        console.error('No Vulnerability array found');
        return [];
      }

      const vulnerabilities = data.Vulnerability;
      const cves = [];
      
      const selectedMonth = document.getElementById('msrc-monthSelector').value;
      const [selectedYear, selectedShortMonth] = selectedMonth.split('-');
      const selectedMonthIndex = this.monthNames.findIndex(month => month.startsWith(selectedShortMonth));
      
      console.log(`Filtering for month: ${selectedYear}-${selectedShortMonth} (index: ${selectedMonthIndex})`);
      
      const defaultReleaseDate = data.DocumentTracking ? 
        new Date(data.DocumentTracking.CurrentReleaseDate || data.DocumentTracking.InitialReleaseDate) : 
        new Date();

      vulnerabilities.forEach((vuln, index) => {
        const cveId = vuln.CVE || '';
        
        if (!cveId || !cveId.startsWith('CVE-') || cveId === 'CVE-' || cveId.length < 8) {
          return;
        }
        
        let title = 'Security Update';
        if (vuln.Title && vuln.Title.Value) {
          title = vuln.Title.Value;
        }
        
        if (title === 'Security Update' || title === '' || title === 'Unknown') {
          return;
        }

        let cveDate = defaultReleaseDate;
        if (vuln.RevisionHistory && Array.isArray(vuln.RevisionHistory)) {
          const initialRevision = vuln.RevisionHistory.find(rev => 
            rev.Description && rev.Description.Value && 
            rev.Description.Value.toLowerCase().includes('published')
          );
          
          if (initialRevision && initialRevision.Date) {
            cveDate = new Date(initialRevision.Date);
          } else if (vuln.RevisionHistory.length > 0 && vuln.RevisionHistory[0].Date) {
            cveDate = new Date(vuln.RevisionHistory[0].Date);
          }
        }

        const cveYear = cveDate.getFullYear();
        const cveMonth = cveDate.getMonth();
        
        if (cveYear != selectedYear || cveMonth != selectedMonthIndex) {
          console.log(`Filtering out CVE ${cveId}: published ${cveDate.toLocaleDateString()} (not in ${selectedYear}-${selectedShortMonth})`);
          return;
        }

        let maxScore = null;
        if (vuln.CVSSScoreSets && Array.isArray(vuln.CVSSScoreSets)) {
          vuln.CVSSScoreSets.forEach(scoreSet => {
            if (scoreSet.BaseScore && (!maxScore || scoreSet.BaseScore > maxScore)) {
              maxScore = scoreSet.BaseScore;
            }
          });
        }

        let severityText = 'Unknown';
        if (vuln.Threats && Array.isArray(vuln.Threats)) {
          const severityThreat = vuln.Threats.find(threat => 
            threat.Type === 3 || 
            (threat.Description && threat.Description.Value && 
             (threat.Description.Value.includes('Critical') || 
              threat.Description.Value.includes('Important') ||
              threat.Description.Value.includes('Moderate') ||
              threat.Description.Value.includes('Low')))
          );
          if (severityThreat && severityThreat.Description && severityThreat.Description.Value) {
            severityText = severityThreat.Description.Value;
          }
        }

        let description = '';
        if (vuln.Notes && Array.isArray(vuln.Notes)) {
          const descNote = vuln.Notes.find(note => note.Type === 1);
          if (descNote && descNote.Value) {
            description = descNote.Value;
          }
        }

        cves.push({
          id: cveId,
          title: title,
          date: cveDate,
          severity: maxScore,
          severityText: severityText,
          description: description
        });
      });

      cves.sort((a, b) => b.date - a.date);

      console.log(`Successfully parsed ${cves.length} CVEs for ${selectedYear}-${selectedShortMonth} (filtered out ${vulnerabilities.length - cves.length} from other months)`);
      return cves;
    },

    updateResultsSummary: function() {
      const summaryDiv = document.getElementById('msrc-resultsSummary');
      if (!summaryDiv) return;
      
      const total = this.currentCveData.length;
      const filtered = this.filteredCveData.length;
      const severityFilterSelect = document.getElementById('msrc-severityFilter');
      const severityFilter = severityFilterSelect ? severityFilterSelect.value : 'all';
      
      let message = `Showing ${filtered} of ${total} CVEs`;
      if (severityFilter !== 'all') {
        message += ` (filtered by ${severityFilter} severity)`;
      }
      
      summaryDiv.innerHTML = `<div class="msrc-results-summary">${message}</div>`;
      summaryDiv.style.display = total > 0 ? 'block' : 'none';
    },

    applyFilters: function() {
      const severityFilterSelect = document.getElementById('msrc-severityFilter');
      const pageSizeSelect = document.getElementById('msrc-pageSize');
      
      if (!severityFilterSelect || !pageSizeSelect) return;
      
      const severityFilter = severityFilterSelect.value;
      const pageSizeValue = pageSizeSelect.value;
      
      this.pageSize = pageSizeValue === 'all' ? this.currentCveData.length : parseInt(pageSizeValue);
      
      this.filteredCveData = this.currentCveData.filter(cve => {
        if (severityFilter === 'all') return true;
        
        const category = this.getSeverityCategory(cve.severity);
        return category === severityFilter;
      });
      
      this.currentPage = 1;
      this.displayCurrentPage();
      this.updateResultsSummary();
    },

    resetFilters: function() {
      const severityFilterSelect = document.getElementById('msrc-severityFilter');
      const pageSizeSelect = document.getElementById('msrc-pageSize');
      
      if (severityFilterSelect) severityFilterSelect.value = 'all';
      if (pageSizeSelect) pageSizeSelect.value = '20';
      
      this.pageSize = 20;
      this.filteredCveData = [...this.currentCveData];
      this.currentPage = 1;
      this.displayCurrentPage();
      this.updateResultsSummary();
    },

    changePage: function(delta) {
      const totalPages = Math.ceil(this.filteredCveData.length / this.pageSize);
      const newPage = this.currentPage + delta;
      
      if (newPage >= 1 && newPage <= totalPages) {
        this.currentPage = newPage;
        this.displayCurrentPage();
      }
    },

    displayCurrentPage: function() {
      const totalPages = Math.ceil(this.filteredCveData.length / this.pageSize);
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = Math.min(startIndex + this.pageSize, this.filteredCveData.length);
      const currentPageData = this.filteredCveData.slice(startIndex, endIndex);
      
      this.displayCVEs(currentPageData);
      this.updatePaginationControls(totalPages);
    },

    updatePaginationControls: function(totalPages) {
      const paginationDiv = document.getElementById('msrc-pagination');
      const prevBtn = document.getElementById('msrc-prevPage');
      const nextBtn = document.getElementById('msrc-nextPage');
      const infoDiv = document.getElementById('msrc-paginationInfo');
      
      if (!paginationDiv || !prevBtn || !nextBtn || !infoDiv) return;
      
      if (totalPages <= 1) {
        paginationDiv.style.display = 'none';
      } else {
        paginationDiv.style.display = 'flex';
        prevBtn.disabled = this.currentPage <= 1;
        nextBtn.disabled = this.currentPage >= totalPages;
        infoDiv.textContent = `Page ${this.currentPage} of ${totalPages}`;
      }
    },

    displayCVEs: function(cves) {
      const grid = document.getElementById('msrc-cveGrid');
      
      if (cves.length === 0) {
        grid.innerHTML = '<div class="msrc-no-data">No security updates found for the selected period.</div>';
        return;
      }

      let html = '';
      cves.forEach(cve => {
        const severity = this.getSeverityCategory(cve.severity);
        const severityDisplay = cve.severity ? 
          `${cve.severityText} (CVSS: ${cve.severity})` : 
          cve.severityText;

        const msrcUrl = this.getMSRCUrl(cve.id);

        html += `
          <div class="msrc-cve-item" onclick="window.open('${msrcUrl}', '_blank')">
            <div class="msrc-cve-header">
              <div class="msrc-cve-id">
                ${cve.id}
                <span class="msrc-external-link-icon">🔗</span>
              </div>
              <div class="msrc-cve-date">${cve.date.toLocaleDateString()}</div>
            </div>
            <div class="msrc-cve-title">${cve.title}</div>
            <div class="msrc-cve-severity msrc-severity-${severity}">${severityDisplay}</div>
            ${cve.description ? `
              <div class="msrc-cve-description">
                ${cve.description.substring(0, 300)}${cve.description.length > 300 ? '...' : ''}
              </div>
            ` : ''}
          </div>
        `;
      });

      grid.innerHTML = html;
    },

    getSeverityCategory: function(score) {
      if (!score) return 'unknown';
      if (score >= 9.0) return 'critical';
      if (score >= 7.0) return 'important';
      if (score >= 4.0) return 'moderate';
      return 'low';
    },

    updateStats: function() {
      const criticalCves = this.currentCveData.filter(cve => this.getSeverityCategory(cve.severity) === 'critical');
      
      document.getElementById('msrc-totalCves').textContent = this.currentCveData.length;
      document.getElementById('msrc-criticalCount').textContent = criticalCves.length;
    },

    init: function() {
      console.log('Initializing MSRC CVE Dashboard...');
      this.updateApiCallCount();
      this.populateMonthSelector();
    }
  };

  // Shodan CVEDB Tool functionality
  const shodanTool = {
    allResults: [],

    init: function() {
      console.log('Initializing Shodan CVEDB Tool...');
      
      // Add event listener for Enter key
      document.getElementById('shodan-searchQuery').addEventListener('keypress', (e) => {
        if (e.key === 'Enter') {
          this.performSearch();
        }
      });
    },

    async performSearch() {
      const query = document.getElementById('shodan-searchQuery').value.trim();
      
      if (!query) {
        alert('Please enter a CVE ID');
        return;
      }

      const resultsDiv = document.getElementById('shodan-results');
      resultsDiv.innerHTML = '<div class="shodan-loading">Searching CVEDB...</div>';

      try {
        // Remove CVE- prefix if present for cleaner lookup
        const cveId = query.toUpperCase().replace(/^CVE-/, '');
        const targetUrl = `https://cvedb.shodan.io/cve/CVE-${cveId}`;

        // Use CORS proxy (Worker if configured, else CorsProxy.io)
        const url = proxied(targetUrl);

        console.log('Fetching URL:', url); // Debug log
        
        const response = await fetch(url);
        
        console.log('Response status:', response.status); // Debug log
        console.log('Response headers:', response.headers); // Debug log
        
        if (!response.ok) {
          const errorText = await response.text();
          console.log('Error response:', errorText); // Debug log
          throw new Error(`HTTP ${response.status}: ${response.statusText} - ${errorText}`);
        }

        const responseText = await response.text();
        console.log('Raw response:', responseText); // Debug log
        
        const data = JSON.parse(responseText);
        
        // Handle single CVE result
        if (data.cve_id || data.cve) {
          this.allResults = [data];
          this.displayResults();
        } else {
          throw new Error('CVE not found in database');
        }
        
      } catch (error) {
        console.error('Search error:', error);
        resultsDiv.innerHTML = `
          <div class="shodan-error">
            <h4>CVE Search Error</h4>
            <p>${error.message}</p>
            <p><strong>Common issues:</strong></p>
            <ul>
              <li>CVE might not exist in CVEDB (try a well-known CVE like CVE-2024-21413)</li>
              <li>Check that CVE format is correct (CVE-YYYY-NNNNN)</li>
              <li>CORS proxy might be temporarily unavailable</li>
            </ul>
            <p><strong>Examples:</strong> CVE-2024-21413, CVE-2021-44228, CVE-2023-23397</p>
          </div>
        `;
      }
    },

    displayResults() {
      const resultsDiv = document.getElementById('shodan-results');
      
      if (this.allResults.length === 0) {
        resultsDiv.innerHTML = `
          <div class="shodan-no-results">
            <h3>No Results Found</h3>
            <p>CVE not found in the CVEDB database.</p>
          </div>
        `;
        return;
      }

      // Since we only have one result, show detailed view
      let html = this.renderDetailedCard(this.allResults[0]);
      resultsDiv.innerHTML = html;
    },

    renderDetailedCard(item) {
      const epssLevel = this.getEPSSLevel(item.epss);
      const publishedDate = item.published_time ? new Date(item.published_time).toLocaleDateString() : 'Unknown';

      return `
        <div class="shodan-vulnerability-card">
          <div class="shodan-cve-header">
            <div class="shodan-cve-id">${item.cve_id || item.cve || 'Unknown CVE'}</div>
            <div class="shodan-badges">
              ${item.kev ? '<span class="shodan-badge kev">🚨 KEV</span>' : ''}
              ${item.epss ? `<span class="shodan-badge epss-${epssLevel}">EPSS ${(item.epss * 100).toFixed(1)}%</span>` : ''}
              ${item.cvss ? `<span class="shodan-badge cvss">CVSS ${item.cvss}</span>` : ''}
            </div>
          </div>

          <div class="shodan-vulnerability-summary">
            ${item.summary || 'No summary available'}
          </div>

          <div class="shodan-metrics">
            <div class="shodan-metric">
              <span class="shodan-metric-value">${item.cvss || 'N/A'}</span>
              <div class="shodan-metric-label">CVSS Score</div>
            </div>
            <div class="shodan-metric">
              <span class="shodan-metric-value">${item.epss ? (item.epss * 100).toFixed(2) + '%' : 'N/A'}</span>
              <div class="shodan-metric-label">EPSS (Exploit Probability)</div>
            </div>
            <div class="shodan-metric">
              <span class="shodan-metric-value">${item.ranking_epss ? (item.ranking_epss * 100).toFixed(1) + '%' : 'N/A'}</span>
              <div class="shodan-metric-label">EPSS Percentile</div>
            </div>
            <div class="shodan-metric">
              <span class="shodan-metric-value">${item.kev ? 'YES' : 'NO'}</span>
              <div class="shodan-metric-label">CISA KEV Listed</div>
            </div>
          </div>

          ${item.propose_action ? `
            <div class="shodan-proposed-action">
              <h4>🔧 Recommended Action</h4>
              <p>${item.propose_action}</p>
            </div>
          ` : ''}

          <div class="shodan-additional-info">
            <button class="shodan-expand-btn" onclick="shodanTool.toggleDetails('${item.cve_id || item.cve}')">
              <span id="shodan-toggle-text-${(item.cve_id || item.cve).replace(/[^a-zA-Z0-9]/g, '')}">Show More Details</span>
            </button>
            
            <div class="shodan-details-section" id="shodan-details-${(item.cve_id || item.cve).replace(/[^a-zA-Z0-9]/g, '')}" style="display: none;">
              
              ${item.cpes && item.cpes.length > 0 ? `
                <div class="shodan-detail-block">
                  <h4>📦 Affected Products (CPEs)</h4>
                  <div class="shodan-cpe-list">
                    ${item.cpes.slice(0, 10).map(cpe => `<span class="shodan-cpe-tag">${cpe}</span>`).join('')}
                    ${item.cpes.length > 10 ? `<span class="shodan-cpe-more">... and ${item.cpes.length - 10} more</span>` : ''}
                  </div>
                </div>
              ` : ''}

              ${item.references && item.references.length > 0 ? `
                <div class="shodan-detail-block">
                  <h4>🔗 References & Advisories</h4>
                  <div class="shodan-references-list">
                    ${item.references.slice(0, 5).map(ref => `
                      <a href="${ref}" target="_blank" class="shodan-reference-link">
                        ${ref.length > 60 ? ref.substring(0, 60) + '...' : ref}
                      </a>
                    `).join('')}
                    ${item.references.length > 5 ? `<p class="shodan-ref-more">... and ${item.references.length - 5} more references</p>` : ''}
                  </div>
                </div>
              ` : ''}

              ${item.cvss_v2 ? `
                <div class="shodan-detail-block">
                  <h4>📊 Additional CVSS Scores</h4>
                  <div class="shodan-cvss-versions">
                    <span class="shodan-cvss-tag">CVSS v2: ${item.cvss_v2}</span>
                    ${item.cvss_v3 ? `<span class="shodan-cvss-tag">CVSS v3: ${item.cvss_v3}</span>` : ''}
                  </div>
                </div>
              ` : ''}
            </div>
          </div>

          <div class="shodan-external-links">
            <a href="https://cvedb.shodan.io/cve/${item.cve_id || item.cve}" target="_blank" class="shodan-external-link">
              🌐 View on CVEDB Shodan
            </a>
            <a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=${item.cve_id || item.cve}" target="_blank" class="shodan-external-link">
              📋 View on CVE MITRE
            </a>
          </div>

          <div class="shodan-published-date">
            📅 Published: ${publishedDate}
            ${item.ransomware_campaign && item.ransomware_campaign !== 'Unknown' ? 
              `| 🦠 Ransomware: ${item.ransomware_campaign}` : ''}
          </div>
        </div>
      `;
    },

    renderListItem(item) {
      const epssLevel = this.getEPSSLevel(item.epss);
      const publishedDate = item.published_time ? new Date(item.published_time).toLocaleDateString() : 'Unknown';

      return `
        <div class="shodan-list-item">
          <div class="shodan-list-item-header">
            <div class="shodan-list-item-cve">${item.cve_id || item.cve || 'Unknown CVE'}</div>
            <div class="shodan-badges">
              ${item.kev ? '<span class="shodan-badge kev">KEV</span>' : ''}
              ${item.epss ? `<span class="shodan-badge epss-${epssLevel}">EPSS ${(item.epss * 100).toFixed(1)}%</span>` : ''}
            </div>
          </div>
          <div class="shodan-list-item-summary">
            ${item.summary ? item.summary.substring(0, 200) + (item.summary.length > 200 ? '...' : '') : 'No summary available'}
          </div>
          <div class="shodan-list-item-metrics">
            <span class="shodan-list-metric">CVSS: ${item.cvss || 'N/A'}</span>
            <span class="shodan-list-metric">EPSS: ${item.epss ? (item.epss * 100).toFixed(2) + '%' : 'N/A'}</span>
            <span class="shodan-list-metric">Published: ${publishedDate}</span>
          </div>
        </div>
      `;
    },

    getEPSSLevel(epss) {
      if (!epss) return 'low';
      if (epss >= 0.7) return 'high';
      if (epss >= 0.3) return 'medium';
      return 'low';
    },

    toggleDetails(cveId) {
      const cleanId = cveId.replace(/[^a-zA-Z0-9]/g, '');
      const detailsSection = document.getElementById(`shodan-details-${cleanId}`);
      const toggleText = document.getElementById(`shodan-toggle-text-${cleanId}`);
      
      if (detailsSection.style.display === 'none') {
        detailsSection.style.display = 'block';
        toggleText.textContent = 'Hide Details';
      } else {
        detailsSection.style.display = 'none';
        toggleText.textContent = 'Show More Details';
      }
    }
  };

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
