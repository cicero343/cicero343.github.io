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

  /* Secondary CVE Navigation */
  .cve-secondary-nav {
    display: none;
    justify-content: center;
    background: #1976d2;
    padding: 8px;
    flex-wrap: wrap;
    border-top: 1px solid rgba(255,255,255,0.2);
  }

  .cve-secondary-nav.show {
    display: flex;
  }

  .cve-secondary-nav a {
    color: white;
    padding: 8px 16px;
    text-decoration: none;
    margin: 3px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9em;
    background: rgba(255,255,255,0.1);
  }

  .cve-secondary-nav a.active,
  .cve-secondary-nav a:hover {
    background: rgba(255,255,255,0.2);
  }

  @media (max-width: 768px) {
    .cve-secondary-nav {
      padding: 6px 4px;
    }
    
    .cve-secondary-nav a {
      flex: 0 0 calc(50% - 8px);
      width: calc(50% - 8px);
      padding: 10px 4px;
      margin: 2px;
      font-size: 0.75em;
      text-align: center;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      box-sizing: border-box;
    }
  }

  @media (max-width: 480px) {
    .cve-secondary-nav a {
      flex: 0 0 calc(50% - 6px);
      width: calc(50% - 6px);
      padding: 8px 2px;
      margin: 1px;
      font-size: 0.7em;
    }
  }

/* Secondary Tools Navigation */
  .tools-secondary-nav {
    display: none;
    justify-content: center;
    background: #1976d2;
    padding: 8px;
    flex-wrap: wrap;
    border-top: 1px solid rgba(255,255,255,0.2);
  }

  .tools-secondary-nav.show {
    display: flex;
  }

  .tools-secondary-nav a {
    color: white;
    padding: 8px 16px;
    text-decoration: none;
    margin: 3px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9em;
    background: rgba(255,255,255,0.1);
  }

  .tools-secondary-nav a.active,
  .tools-secondary-nav a:hover {
    background: rgba(255,255,255,0.2);
  }

  @media (max-width: 768px) {
  .tools-secondary-nav {
      padding: 6px 4px;
    }
    
  .tools-secondary-nav a {
      flex: 0 0 calc(50% - 8px);
      width: calc(50% - 8px);
      padding: 10px 4px;
      margin: 2px;
      font-size: 0.75em;
      text-align: center;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      box-sizing: border-box;
    }
  }

  @media (max-width: 480px) {
  .tools-secondary-nav a {
      flex: 0 0 calc(50% - 6px);
      width: calc(50% - 6px);
      padding: 8px 2px;
      margin: 1px;
      font-size: 0.7em;
    }
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

  /* CVE Sub-tab styles */
  .cve-sub-tab {
    display: none;
  }

  .cve-sub-tab.active {
    display: block;
  }

  /* Tools Sub-tab styles */
  .tools-sub-tab {
    display: none;
  }

  .tools-sub-tab.active {
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

 /* Currency Exchange Dashboard Styles */
.currency-exchange-container {
  max-width: 480px;
  margin: 0 auto;
  padding: 8px 16px 16px 16px;
}

.currency-header {
  text-align: center;
  margin-bottom: 16px;
}

.currency-header h2 {
  font-size: 24px;
  font-weight: 600;
  color: #212529;
  margin-bottom: 2px;
}

.currency-header p {
  font-size: 14px;
  color: #6c757d;
  margin-bottom: 0;
}

.currency-control-panel {
  background: white;
  border-radius: 12px;
  padding: 16px;
  margin-bottom: 16px;
  border: 1px solid #e9ecef;
}

.currency-controls {
  display: grid;
  grid-template-columns: 80px 1fr auto; /* Amount, Currency, Convert button */
  gap: 8px;
  align-items: end;
}

.currency-control-group select, .currency-control-group input {
  width: 100%;
  padding: 6px 8px;
  border: 1px solid #ced4da;
  border-radius: 6px;
  font-size: 14px;
  background: white;
  color: #495057;
  box-sizing: border-box;
}

.currency-control-group input[type="number"] {
  text-align: center;
  max-width: 80px; /* Constrains the amount field */
}

.currency-convert-btn {
  padding: 8px 14px;
  background: #0d6efd;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  white-space: nowrap;
}

.currency-convert-btn:hover {
  background: #0b5ed7;
}

.currency-convert-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.currency-rates-container {
  background: white;
  border-radius: 12px;
  border: 1px solid #e9ecef;
  overflow: hidden;
}

.currency-rates-header {
  background: #f8f9fa;
  padding: 16px 20px;
  border-bottom: 1px solid #e9ecef;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.currency-base-amount {
  font-size: 18px;
  font-weight: 600;
  color: #212529;
}

.currency-last-updated {
  font-size: 12px;
  color: #6c757d;
  text-align: right;
}

.currency-rate-row {
  display: flex;
  align-items: center;
  padding: 14px 20px;
  border-bottom: 1px solid #f1f3f4;
}

.currency-rate-row:last-child {
  border-bottom: none;
}

.currency-rate-row:active {
  background-color: #f8f9fa;
}

.currency-flag {
  width: 24px;
  height: 18px;
  border: 1px solid #ccc;
  border-radius: 3px;
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
  font-size: 15px;
  color: #212529;
  line-height: 1.2;
  min-width: 45px; /* Ensures consistent spacing */
}

.currency-name {
  color: #6c757d;
  font-size: 12px;
  line-height: 1.2;
}

.currency-rate-value {
  font-size: 16px;
  font-weight: 600;
  color: #212529;
  text-align: right;
  font-variant-numeric: tabular-nums;
}

.currency-loading, .currency-error {
  text-align: center;
  padding: 32px 20px;
  color: #6c757d;
  font-size: 14px;
}

.currency-error {
  color: #dc3545;
  background: #f8d7da;
}

/* Dark mode styles */
[data-theme="dark"] .currency-header h2 {
  color: #00ff00 !important;
}

[data-theme="dark"] .currency-header p {
  color: #00aa00 !important;
}

[data-theme="dark"] .currency-control-panel,
[data-theme="dark"] .currency-rates-container,
[data-theme="dark"] .currency-rates-header {
  background: #111 !important;
  border-color: #333 !important;
}

[data-theme="dark"] .currency-control-group label,
[data-theme="dark"] .currency-base-amount,
[data-theme="dark"] .currency-code {
  color: #00ff00 !important;
}

[data-theme="dark"] .currency-control-group select,
[data-theme="dark"] .currency-control-group input {
  background: #111 !important;
  color: #00ff00 !important;
  border-color: #333 !important;
}

[data-theme="dark"] .currency-last-updated,
[data-theme="dark"] .currency-name {
  color: #00aa00 !important;
}

[data-theme="dark"] .currency-rate-value {
  color: #00ff00 !important;
}

[data-theme="dark"] .currency-convert-btn {
  background: #006400 !important;
  color: #00ff00 !important;
}

/* Mobile styles */
@media (max-width: 576px) {
  .currency-control-panel {
    padding: 10px;
  }
  .currency-controls {
    grid-template-columns: 60px 1fr auto; /* Smaller amount field on mobile */
    gap: 6px;
  }
  .currency-convert-btn {
    padding: 8px 12px;
    font-size: 13px;
  }

  .currency-rate-row {
    padding: 16px;
  }

  .currency-rates-header {
    padding: 16px;
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
  }

  .currency-last-updated {
    text-align: left;
  }
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

  /* CVE Tracker Styles */
  .cve-tracker-container {
    background: linear-gradient(135deg, #0f0f23 0%, #1a1a3a 100%);
    color: #ffffff;
    min-height: 100vh;
    font-size: 14px;
    margin: -20px;
    padding: 0;
    border-radius: 0;
  }

  .cve-header {
    background: rgba(0, 0, 0, 0.3);
    padding: 20px;
    text-align: center;
    border-bottom: 2px solid #00ff88;
    backdrop-filter: blur(10px);
  }

  .cve-header h1 {
    font-size: 2.2em;
    color: #00ff88;
    text-shadow: 0 0 20px rgba(0, 255, 136, 0.5);
    margin-bottom: 8px;
  }

  .cve-header p {
    color: #cccccc;
    font-size: 1em;
  }

  .cve-controls {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 15px;
    padding: 15px;
    background: rgba(0, 0, 0, 0.2);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    flex-wrap: wrap;
  }

  .cve-filter-group {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .cve-filter-label {
    color: #00ff88;
    font-weight: bold;
    font-size: 0.9em;
  }

  .cve-filter-select {
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(0, 255, 136, 0.3);
    border-radius: 6px;
    padding: 6px 10px;
    color: #ffffff;
    font-size: 13px;
  }

  .cve-filter-select option {
    background: #1a1a3a;
    color: #ffffff;
  }

  .cve-calendar-nav {
    display: flex;
    align-items: center;
    gap: 12px;
    background: rgba(0, 255, 136, 0.1);
    padding: 8px 15px;
    border-radius: 15px;
    border: 1px solid rgba(0, 255, 136, 0.3);
    position: relative;
  }

  .cve-nav-btn {
    background: transparent;
    border: 1px solid #00ff88;
    color: #00ff88;
    padding: 6px 12px;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 13px;
  }

  .cve-nav-btn:hover {
    background: #00ff88;
    color: #000;
  }

  .cve-current-month {
    font-weight: bold;
    color: #00ff88;
    min-width: 120px;
    text-align: center;
    font-size: 0.95em;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
    position: relative;
  }

  .cve-month-text {
    color: #00ff88;
  }

  .cve-year-text {
    color: #4ecdc4;
    font-size: 0.85em;
    text-decoration: underline;
    cursor: pointer;
    transition: color 0.3s ease;
  }

  .cve-year-text:hover {
    color: #00ff88;
  }

  .cve-year-picker {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    background: rgba(26, 26, 58, 0.98);
    border: 1px solid rgba(0, 255, 136, 0.3);
    border-radius: 8px;
    padding: 10px;
    z-index: 1000;
    display: none;
    max-height: 200px;
    overflow-y: auto;
    min-width: 100px;
    margin-top: 5px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  }

  .cve-year-picker.cve-show {
    display: block;
  }

  .cve-year-option {
    padding: 5px 10px;
    cursor: pointer;
    color: #cccccc;
    text-align: center;
    border-radius: 4px;
    transition: all 0.3s ease;
  }

  .cve-year-option:hover {
    background: rgba(0, 255, 136, 0.2);
    color: #00ff88;
  }

  .cve-year-option.cve-current {
    background: rgba(0, 255, 136, 0.3);
    color: #00ff88;
  }

  .cve-dashboard {
    display: grid;
    grid-template-columns: 1.4fr 1fr;
    gap: 20px;
    padding: 20px;
    max-width: 1600px;
    margin: 0 auto;
    height: calc(100vh - 160px);
  }

  .cve-main-panel {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 15px;
    padding: 20px;
    border: 1px solid rgba(0, 255, 136, 0.2);
    backdrop-filter: blur(10px);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }

  .cve-side-panel {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 15px;
    padding: 20px;
    border: 1px solid rgba(0, 255, 136, 0.2);
    backdrop-filter: blur(10px);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    max-height: calc(100vh - 160px);
  }

  .cve-panel-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    flex-shrink: 0;
  }

  .cve-panel-title {
    display: flex;
    align-items: center;
    gap: 10px;
    color: #00ff88;
    font-size: 1.3em;
    font-weight: 600;
  }

  .cve-api-status {
    padding: 5px 12px;
    border-radius: 15px;
    font-size: 0.8em;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .cve-api-live {
    background: #00ff88;
    color: #000;
    box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
  }

  .cve-api-error {
    background: #ff6b6b;
    color: #fff;
  }

  .cve-calendar-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    margin-top: 80px;
  }

  @media (max-width: 1200px) {
    .cve-calendar-container {
      margin-top: 40px;
    }
  }

  .cve-calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 2px;
    flex: 1;
  }

  .cve-calendar-header {
    background: rgba(0, 255, 136, 0.2);
    padding: 8px 5px;
    text-align: center;
    font-weight: bold;
    color: #00ff88;
    border-radius: 6px;
    font-size: 0.8em;
  }

  .cve-calendar-day {
    background: rgba(255, 255, 255, 0.03);
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative;
    min-height: 45px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    padding: 3px;
  }

  .cve-calendar-day:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: scale(1.05);
    z-index: 5;
  }

  .cve-calendar-day.selected {
    background: rgba(0, 255, 136, 0.3);
    border-color: #00ff88;
    transform: scale(1.05);
  }

  .cve-calendar-day.other-month {
    opacity: 0.3;
  }

  .cve-calendar-day.today {
    border: 2px solid #4ecdc4;
    box-shadow: 0 0 8px rgba(78, 205, 196, 0.3);
  }

  .cve-day-number {
    font-size: 0.9em;
    font-weight: bold;
    margin-bottom: 2px;
  }

  .cve-day-count {
    font-size: 0.7em;
    background: rgba(0, 0, 0, 0.6);
    padding: 1px 4px;
    border-radius: 8px;
    min-width: 16px;
    text-align: center;
  }

  .cve-day-heat-0 { background: rgba(255, 255, 255, 0.03) !important; }
  .cve-day-heat-1 { background: rgba(0, 255, 136, 0.2) !important; }
  .cve-day-heat-2 { background: rgba(0, 255, 136, 0.4) !important; }
  .cve-day-heat-3 { background: rgba(255, 183, 0, 0.4) !important; }
  .cve-day-heat-4 { background: rgba(255, 121, 0, 0.4) !important; }
  .cve-day-heat-5 { background: rgba(255, 107, 107, 0.4) !important; }

  .cve-stats-summary {
    display: flex;
    gap: 12px;
    margin-bottom: 15px;
    flex-shrink: 0;
  }

  .cve-stat-box {
    background: rgba(255, 255, 255, 0.03);
    padding: 10px;
    border-radius: 10px;
    text-align: center;
    border: 1px solid rgba(255, 255, 255, 0.1);
    flex: 1;
  }

  .cve-stat-number {
    font-size: 1.4em;
    font-weight: bold;
    color: #00ff88;
    margin-bottom: 3px;
  }

  .cve-stat-label {
    font-size: 0.8em;
    color: #cccccc;
  }

  .cve-loading {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 150px;
    color: #666;
    font-size: 1em;
  }

  .cve-spinner {
    width: 30px;
    height: 30px;
    border: 3px solid rgba(0, 255, 136, 0.1);
    border-top: 3px solid #00ff88;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin-right: 12px;
  }

  .cve-error {
    color: #ff6b6b;
    text-align: center;
    padding: 30px;
    font-size: 1em;
  }

  .cve-no-advisories {
    text-align: center;
    color: #666;
    padding: 30px;
    font-style: italic;
    font-size: 0.9em;
  }

  .cve-advisory-item {
    background: rgba(255, 255, 255, 0.03);
    border-radius: 10px;
    padding: 12px;
    margin-bottom: 10px;
    border-left: 3px solid #ff6b6b;
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .cve-advisory-item:hover {
    background: rgba(255, 255, 255, 0.08);
    transform: translateX(3px);
    box-shadow: 0 3px 15px rgba(0, 0, 0, 0.3);
  }

  .cve-advisory-item.expanded {
    background: rgba(255, 255, 255, 0.08);
  }

  .cve-severity-badge {
    padding: 3px 8px;
    border-radius: 10px;
    font-size: 0.7em;
    font-weight: bold;
    text-transform: uppercase;
  }

  .cve-severity-critical {
    background: #ff6b6b;
    color: white;
  }

  .cve-severity-high {
    background: #ff8c00;
    color: white;
  }

  .cve-severity-medium {
    background: #ffa500;
    color: black;
  }

  .cve-severity-low {
    background: #00ff88;
    color: black;
  }

  .cve-advisory-details {
    display: none;
    margin-top: 10px;
    padding-top: 10px;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }

  .cve-advisory-details.cve-show {
    display: block;
  }

  .cve-selected-date-info {
    background: rgba(0, 255, 136, 0.1);
    padding: 12px;
    border-radius: 10px;
    margin-bottom: 15px;
    border: 1px solid rgba(0, 255, 136, 0.3);
    flex-shrink: 0;
  }

  .cve-selected-date {
    font-size: 1.1em;
    font-weight: bold;
    color: #00ff88;
    margin-bottom: 3px;
  }

  .cve-date-summary {
    font-size: 0.85em;
    color: #cccccc;
  }

  .cve-advisory-list {
    flex: 1;
    overflow-y: auto;
    padding-right: 5px;
  }

  .cve-advisory-list::-webkit-scrollbar {
    width: 4px;
  }

  .cve-advisory-list::-webkit-scrollbar-track {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 2px;
  }

  .cve-advisory-list::-webkit-scrollbar-thumb {
    background: rgba(0, 255, 136, 0.3);
    border-radius: 2px;
  }

  .cve-advisory-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 8px;
  }

  .cve-advisory-title {
    display: flex;
    flex-direction: column;
    gap: 3px;
  }

  .cve-advisory-id {
    font-size: 0.9em;
    font-weight: bold;
    color: #00ff88;
  }

  .cve-id {
    font-size: 0.75em;
    color: #4ecdc4;
    font-family: monospace;
  }

  .cve-advisory-summary {
    font-size: 0.8em;
    line-height: 1.3;
    color: #e0e0e0;
    margin-bottom: 8px;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .cve-detail-row {
    display: flex;
    margin: 6px 0;
    font-size: 0.75em;
  }

  .cve-detail-label {
    font-weight: bold;
    color: #00ff88;
    min-width: 80px;
  }

  .cve-detail-value {
    color: #cccccc;
    word-break: break-word;
  }

  .cve-external-link {
    display: inline-block;
    margin-top: 8px;
    padding: 6px 12px;
    background: rgba(0, 255, 136, 0.1);
    border: 1px solid #00ff88;
    border-radius: 15px;
    color: #00ff88;
    text-decoration: none;
    font-size: 0.75em;
    transition: all 0.3s ease;
  }

  .cve-external-link:hover {
    background: #00ff88;
    color: #000;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  /* MSRC Tracker Styles */
  .msrc-tracker-container {
    max-width: none;
    margin: -20px;
    padding: 0;
    background: white;
    border-radius: 0;
    box-shadow: none;
  }

  .msrc-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 30px;
    text-align: center;
    position: relative;
  }

  .msrc-header h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    font-weight: 300;
  }

  .msrc-header p {
    font-size: 1.1rem;
    opacity: 0.9;
  }

  .msrc-loading {
    position: absolute;
    top: 50%;
    right: 30px;
    transform: translateY(-50%);
    display: none;
  }

  .msrc-spinner {
    width: 30px;
    height: 30px;
    border: 3px solid rgba(255, 255, 255, 0.3);
    border-top: 3px solid white;
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }

  .msrc-controls {
    padding: 20px 30px;
    background: #f8f9fa;
    border-bottom: 1px solid #e9ecef;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 15px;
  }

  .msrc-stats {
    display: flex;
    gap: 20px;
    align-items: center;
  }

  .msrc-stat-item {
    background: white;
    padding: 10px 15px;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    min-width: 80px;
  }

  .msrc-stat-number {
    font-size: 1.5rem;
    font-weight: bold;
    color: #667eea;
  }

  .msrc-stat-label {
    font-size: 0.8rem;
    color: #666;
    margin-top: 2px;
  }

  .msrc-api-info {
    background: #e3f2fd;
    padding: 15px 30px;
    border-left: 4px solid #2196f3;
    margin: 20px 30px;
    border-radius: 10px;
    text-align: center;
  }

  .msrc-api-info p {
    color: #1976d2;
    margin: 0;
    font-size: 0.9rem;
  }

  .msrc-api-info code {
    background: rgba(25, 118, 210, 0.1);
    padding: 2px 6px;
    border-radius: 4px;
    font-family: 'Courier New', monospace;
  }

  .msrc-filter-controls {
    background: #f8f9fa;
    padding: 20px 30px;
    border-bottom: 1px solid #e9ecef;
    display: flex;
    gap: 20px;
    align-items: center;
    flex-wrap: wrap;
  }

  .msrc-filter-group {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .msrc-filter-group label {
    font-weight: 600;
    color: #333;
    font-size: 0.9rem;
  }

  .msrc-filter-select {
    padding: 8px 12px;
    border: 2px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
    background: white;
  }

  .msrc-filter-select:focus {
    border-color: #667eea;
    outline: none;
  }

  .msrc-pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    padding: 20px;
    background: #f8f9fa;
    border-top: 1px solid #e9ecef;
  }

  .msrc-pagination-btn {
    background: #667eea;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.3s ease;
  }

  .msrc-pagination-btn:hover {
    background: #5a67d8;
  }

  .msrc-pagination-btn:disabled {
    background: #ccc;
    cursor: not-allowed;
  }

  .msrc-pagination-info {
    margin: 0 20px;
    font-weight: 600;
    color: #333;
  }

  .msrc-demo-controls {
    display: flex;
    gap: 15px;
    margin-bottom: 20px;
    flex-wrap: wrap;
    align-items: center;
  }

  .msrc-demo-btn {
    background: #28a745;
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.3s ease;
  }

  .msrc-demo-btn:hover {
    background: #218838;
    transform: translateY(-1px);
  }

  .msrc-demo-btn:disabled {
    background: #ccc;
    cursor: not-allowed;
    transform: none;
  }

  .msrc-month-selector {
    padding: 8px 12px;
    border: 2px solid #667eea;
    border-radius: 8px;
    font-size: 14px;
  }

  .msrc-cve-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 20px;
    margin-top: 20px;
  }

  .msrc-cve-item {
    background: white;
    border-radius: 10px;
    padding: 20px;
    border-left: 4px solid #667eea;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .msrc-cve-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
    border-left-color: #5a67d8;
  }

  .msrc-cve-item:active {
    transform: translateY(-1px);
  }

  .msrc-external-link-icon {
    opacity: 0;
    transition: opacity 0.3s ease;
    margin-left: 8px;
    font-size: 0.9rem;
    color: #667eea;
  }

  .msrc-cve-item:hover .msrc-external-link-icon {
    opacity: 1;
  }

  .msrc-cve-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 10px;
    flex-wrap: wrap;
    gap: 10px;
  }

  .msrc-cve-id {
    font-weight: bold;
    color: #667eea;
    font-size: 1.1rem;
  }

  .msrc-cve-date {
    color: #666;
    font-size: 0.9rem;
  }

  .msrc-cve-title {
    margin-bottom: 10px;
    color: #333;
    line-height: 1.4;
    font-size: 1rem;
  }

  .msrc-cve-severity {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 15px;
    font-size: 0.8rem;
    font-weight: bold;
    text-transform: uppercase;
  }

  .msrc-severity-critical {
    background: #ffebee;
    color: #c62828;
  }

  .msrc-severity-important {
    background: #fff3e0;
    color: #ef6c00;
  }

  .msrc-severity-moderate {
    background: #fff8e1;
    color: #f57f17;
  }

  .msrc-severity-low {
    background: #e8f5e8;
    color: #2e7d32;
  }

  .msrc-severity-unknown {
    background: #f5f5f5;
    color: #666;
  }

  .msrc-cve-description {
    margin-top: 10px;
    color: #666;
    font-size: 0.9rem;
    line-height: 1.4;
  }

  .msrc-no-data {
    text-align: center;
    color: #666;
    font-style: italic;
    padding: 40px;
    background: white;
    border-radius: 10px;
  }

  .msrc-error {
    background: #ffebee;
    color: #c62828;
    padding: 15px;
    border-radius: 10px;
    margin: 20px 0;
    border-left: 4px solid #c62828;
  }

  .msrc-success {
    background: #e8f5e8;
    color: #2e7d32;
    padding: 15px;
    border-radius: 10px;
    margin: 20px 0;
    border-left: 4px solid #2e7d32;
  }

  .msrc-demo-section {
    padding: 30px;
  }

  .msrc-results-summary {
    background: #e8f5e8;
    padding: 15px 30px;
    border-left: 4px solid #28a745;
    margin: 0 30px 20px 30px;
    border-radius: 10px;
    font-size: 0.9rem;
    color: #155724;
  }

  /* NVD Lookup Styles */
  .nvd-container {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
    margin: -20px;
    border-radius: 0;
  }
  
  .nvd-inner-container {
    max-width: 1000px;
    margin: 0 auto;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    padding: 40px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
  }
  
  .nvd-header {
    text-align: center;
    margin-bottom: 40px;
  }
  
  .nvd-header h1.auto-adjust {
    font-size: 2.5em;
    margin-bottom: 10px;
    background: linear-gradient(45deg,
    hsl(245, 80%, 70%),
    hsl(270, 60%, 75%),
    hsl(320, 80%, 70%)
    );
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  
  .nvd-status-badge {
    display: inline-block;
    background: linear-gradient(45deg, #38a169, #2f855a);
    color: white;
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 20px;
  }
  
  .nvd-search-section {
    background: white;
    border-radius: 15px;
    padding: 30px;
    margin-bottom: 30px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.08);
  }
  
  .nvd-input-group {
    margin-bottom: 20px;
  }
  
  .nvd-input-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #2d3748;
    font-size: 16px;
  }
  
  .nvd-input-group input, .nvd-input-group select {
    width: 100%;
    padding: 15px 20px;
    border: 2px solid #e2e8f0;
    border-radius: 12px;
    font-size: 16px;
    transition: all 0.3s ease;
  }
  
  .nvd-input-group input:focus, .nvd-input-group select:focus {
    border-color: #667eea;
    outline: none;
    box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
  }
  
  .nvd-grid-controls {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 15px;
    margin-bottom: 20px;
  }
  
  .nvd-button {
    background: linear-gradient(45deg, #667eea, #764ba2);
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-right: 15px;
    margin-bottom: 10px;
  }
  
  .nvd-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
  }
  
  .nvd-button:disabled {
    background: #cbd5e0;
    cursor: not-allowed;
    transform: none;
    box-shadow: none;
  }
  
  .nvd-results-container {
    background: white;
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.08);
    display: none;
  }
  
  .nvd-vulnerability-card {
    background: #f8fafc;
    border-radius: 10px;
    padding: 18px;
    border-left: 4px solid #667eea;
    margin-bottom: 12px;
    cursor: pointer;
    transition: all 0.2s ease;
    border: 1px solid #e2e8f0;
  }
  
  .nvd-vulnerability-card:hover {
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(102, 126, 234, 0.1);
    border-left-color: #4c51bf;
    background: #f1f5f9;
  }
  
  .nvd-card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
  
  .nvd-cve-id {
    font-size: 1.1em;
    font-weight: bold;
    color: #2d3748;
    font-family: 'Monaco', monospace;
  }
  
  .nvd-cvss-badge {
    padding: 5px 12px;
    border-radius: 15px;
    font-size: 12px;
    font-weight: bold;
    color: white;
  }
  
  .nvd-cvss-critical { background: linear-gradient(45deg, #dc2626, #b91c1c); }
  .nvd-cvss-high { background: linear-gradient(45deg, #ea580c, #c2410c); }
  .nvd-cvss-medium { background: linear-gradient(45deg, #d97706, #b45309); }
  .nvd-cvss-low { background: linear-gradient(45deg, #059669, #047857); }
  .nvd-cvss-none { background: linear-gradient(45deg, #6b7280, #4b5563); }
  
  .nvd-card-description {
    color: #4b5563;
    font-size: 14px;
    line-height: 1.4;
    margin-bottom: 10px;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
  
  .nvd-card-meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 12px;
    color: #6b7280;
  }
  
  .nvd-click-hint {
    color: #667eea;
    font-weight: 600;
    background: rgba(102, 126, 234, 0.1);
    padding: 3px 8px;
    border-radius: 10px;
  }
  
  .nvd-loading {
    text-align: center;
    color: #667eea;
    font-style: italic;
    padding: 40px;
  }
  
  .nvd-error {
    background: #fef2f2;
    color: #dc2626;
    padding: 20px;
    border-radius: 10px;
    border-left: 4px solid #dc2626;
  }
  
  /* NVD Popup Styles - FIXED for proper centering */
  .nvd-popup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.8);
    z-index: 1000;
    display: none;
    overflow-y: auto;
    padding: 20px;
    box-sizing: border-box;
  }
  
  .nvd-popup-content {
    background: white;
    border-radius: 20px;
    padding: 30px;
    max-width: 800px;
    width: 100%;
    margin: 0 auto;
    position: relative;
    box-shadow: 0 25px 50px rgba(0,0,0,0.4);
    top: 0;
    transition: all 0.3s ease;
  }
  
  .nvd-popup-close {
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
    border: none;
  }

  .nvd-popup-close:hover {
    background: rgba(0, 0, 0, 0.7);
  }

  .nvd-popup-body {
    padding: 30px;
  }

  /* Shodan CVEDB Styles */
  .shodan-container {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
    margin: -20px;
    border-radius: 0;
  }

  .shodan-inner-container {
    max-width: 1400px;
    margin: 0 auto;
    background: rgba(255, 255, 255, 0.95);
    border-radius: 20px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    overflow: hidden;
  }

  .shodan-header {
    background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
    color: white;
    padding: 30px 40px;
    text-align: center;
  }

  .shodan-header h1 {
    font-size: 2.5em;
    margin-bottom: 10px;
    font-weight: 300;
  }

  .shodan-header p {
    opacity: 0.9;
    font-size: 1.1em;
  }

  .shodan-search-section {
    padding: 40px;
    background: white;
    border-bottom: 1px solid #e1e8ed;
  }

  .shodan-search-controls {
    display: grid;
    grid-template-columns: 1fr 120px;
    gap: 15px;
    margin-bottom: 30px;
    align-items: end;
  }

  .shodan-form-group {
    display: flex;
    flex-direction: column;
  }

  .shodan-form-group label {
    font-weight: 600;
    margin-bottom: 8px;
    color: #2c3e50;
    font-size: 0.9em;
  }

  .shodan-form-group select,
  .shodan-form-group input {
    padding: 12px 15px;
    border: 2px solid #e1e8ed;
    border-radius: 10px;
    font-size: 1em;
    transition: all 0.3s ease;
  }

  .shodan-form-group select:focus,
  .shodan-form-group input:focus {
    outline: none;
    border-color: #667eea;
    box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
  }

  .shodan-search-btn {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 10px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s ease;
    margin-top: 25px;
  }

  .shodan-search-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
  }

  .shodan-search-btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
    transform: none;
  }

  .shodan-disclaimer {
    background: #e8f4fd;
    border-left: 4px solid #0084ff;
    padding: 15px 20px;
    border-radius: 5px;
    margin-top: 25px;
    font-size: 0.9em;
    color: #2c3e50;
    line-height: 1.5;
  }

  .shodan-disclaimer code {
    background: rgba(0, 132, 255, 0.1);
    padding: 2px 6px;
    border-radius: 3px;
    font-family: 'Courier New', monospace;
    font-size: 0.9em;
    color: #0056b3;
  }

  .shodan-disclaimer strong {
    color: #0056b3;
  }

  .shodan-results-section {
    padding: 40px;
  }

  .shodan-loading {
    text-align: center;
    padding: 60px;
    color: #6c757d;
  }

  .shodan-loading::after {
    content: '';
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 3px solid #f3f3f3;
    border-top: 3px solid #667eea;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin-left: 10px;
  }

  .shodan-error {
    background: #fee;
    color: #c33;
    padding: 20px;
    border-radius: 10px;
    border-left: 5px solid #c33;
    margin-bottom: 20px;
  }

  .shodan-results-summary {
    background: #e8f4fd;
    border-left: 5px solid #0084ff;
    padding: 15px 20px;
    border-radius: 5px;
    margin-bottom: 30px;
    font-weight: 500;
  }

  .shodan-vulnerability-card {
    background: white;
    border-radius: 15px;
    padding: 30px;
    margin-bottom: 25px;
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
    border-left: 5px solid #667eea;
    transition: all 0.3s ease;
  }

  .shodan-vulnerability-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15);
  }

  .shodan-cve-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    flex-wrap: wrap;
    gap: 15px;
  }

  .shodan-cve-id {
    font-size: 1.5em;
    font-weight: 700;
    color: #2c3e50;
  }

  .shodan-badges {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
  }

  .shodan-badge {
    padding: 6px 12px;
    border-radius: 20px;
    font-size: 0.8em;
    font-weight: 600;
    text-transform: uppercase;
  }

  .shodan-badge.kev {
    background: #ff4757;
    color: white;
  }

  .shodan-badge.epss-high {
    background: #ff6b6b;
    color: white;
  }

  .shodan-badge.epss-medium {
    background: #ffa726;
    color: white;
  }

  .shodan-badge.epss-low {
    background: #66bb6a;
    color: white;
  }

  .shodan-badge.cvss {
    background: #5c6bc0;
    color: white;
  }

  .shodan-vulnerability-summary {
    margin-bottom: 25px;
    line-height: 1.6;
    color: #4a5568;
    font-size: 1.1em;
  }

  .shodan-metrics {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin-bottom: 25px;
  }

  .shodan-metric {
    text-align: center;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 10px;
  }

  .shodan-metric-value {
    font-size: 1.8em;
    font-weight: 700;
    color: #2c3e50;
    display: block;
  }

  .shodan-metric-label {
    font-size: 0.9em;
    color: #6c757d;
    margin-top: 5px;
  }

  .shodan-proposed-action {
    background: #e8f5e8;
    border-left: 4px solid #28a745;
    padding: 15px 20px;
    border-radius: 5px;
    margin-bottom: 20px;
  }

  .shodan-proposed-action h4 {
    color: #155724;
    margin-bottom: 8px;
    font-size: 1em;
  }

  .shodan-proposed-action p {
    color: #155724;
    margin: 0;
    line-height: 1.5;
  }

  .shodan-published-date {
    color: #6c757d;
    font-size: 0.9em;
    margin-top: 15px;
  }

  .shodan-additional-info {
    margin: 25px 0;
  }

  .shodan-expand-btn {
    background: linear-gradient(135deg, #28a745, #20c997);
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 25px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s ease;
    margin-bottom: 15px;
  }

  .shodan-expand-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(40, 167, 69, 0.4);
  }

  .shodan-details-section {
    background: #f8f9fa;
    border-radius: 10px;
    padding: 20px;
    margin-top: 15px;
  }

  .shodan-detail-block {
    margin-bottom: 20px;
  }

  .shodan-detail-block h4 {
    color: #2c3e50;
    margin-bottom: 10px;
    font-size: 1em;
  }

  .shodan-cpe-list {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .shodan-cpe-tag {
    background: #e9ecef;
    padding: 4px 8px;
    border-radius: 15px;
    font-size: 0.8em;
    font-family: 'Courier New', monospace;
  }

  .shodan-cpe-more {
    color: #6c757d;
    font-style: italic;
    font-size: 0.9em;
  }

  .shodan-references-list {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .shodan-reference-link {
    color: #0084ff;
    text-decoration: none;
    padding: 8px 12px;
    background: white;
    border-radius: 5px;
    border-left: 3px solid #0084ff;
    font-size: 0.9em;
    transition: all 0.2s ease;
  }

  .shodan-reference-link:hover {
    background: #f0f8ff;
    transform: translateX(5px);
  }

  .shodan-ref-more {
    color: #6c757d;
    font-style: italic;
    margin: 5px 0 0 0;
  }

  .shodan-cvss-versions {
    display: flex;
    gap: 10px;
  }

  .shodan-cvss-tag {
    background: #5c6bc0;
    color: white;
    padding: 6px 12px;
    border-radius: 15px;
    font-size: 0.9em;
    font-weight: 600;
  }

  .shodan-external-links {
    display: flex;
    gap: 15px;
    margin: 25px 0 15px 0;
    flex-wrap: wrap;
  }

  .shodan-external-link {
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: white;
    text-decoration: none;
    padding: 12px 20px;
    border-radius: 25px;
    font-weight: 600;
    transition: all 0.3s ease;
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }

  .shodan-external-link:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
    color: white;
    text-decoration: none;
  }

  .shodan-no-results {
    text-align: center;
    padding: 60px;
    color: #6c757d;
  }

  .shodan-no-results h3 {
    margin-bottom: 15px;
    color: #495057;
  }

  .shodan-results-list {
    display: grid;
    gap: 20px;
  }

  .shodan-list-item {
    background: white;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
    border-left: 4px solid #667eea;
    transition: all 0.3s ease;
  }

  .shodan-list-item:hover {
    transform: translateX(5px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
  }

  .shodan-list-item-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }

  .shodan-list-item-cve {
    font-weight: 700;
    color: #2c3e50;
    font-size: 1.1em;
  }

  .shodan-list-item-summary {
    color: #4a5568;
    line-height: 1.5;
    margin-bottom: 15px;
  }

  .shodan-list-item-metrics {
    display: flex;
    gap: 15px;
    font-size: 0.9em;
  }

  .shodan-list-metric {
    background: #f8f9fa;
    padding: 5px 10px;
    border-radius: 5px;
    font-weight: 600;
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

  @media (max-width: 1200px) {
    .cve-dashboard {
      grid-template-columns: 1fr;
      gap: 15px;
      height: auto;
    }
    
    .cve-main-panel {
      min-height: 380px;
    }
    
    .cve-controls {
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }

    .msrc-cve-grid {
      grid-template-columns: 1fr;
    }

    .msrc-header h1 {
      font-size: 2rem;
    }

    .msrc-demo-controls {
      flex-direction: column;
      align-items: stretch;
    }

    .msrc-filter-controls {
      flex-direction: column;
      align-items: stretch;
    }

    .msrc-filter-group {
      justify-content: space-between;
    }

    .nvd-grid-controls {
      grid-template-columns: 1fr;
      gap: 10px;
    }

    .shodan-search-controls {
      grid-template-columns: 1fr;
    }

    .shodan-metrics {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 768px) {
    .cve-calendar-container {
      margin-top: 25px;
    }
    
    .cve-main-panel {
      min-height: 350px;
    }
    
    .cve-calendar-day {
      min-height: 28px;
      font-size: 0.85em;
      padding: 2px;
    }
    
    .cve-day-number {
      font-size: 0.75em;
      margin-bottom: 1px;
    }
    
    .cve-day-count {
      font-size: 0.55em;
      padding: 1px 3px;
    }
    
    .cve-calendar-grid {
      gap: 1px;
    }
    
    .cve-header h1 {
      font-size: 1.8em;
    }

    .msrc-controls {
      flex-direction: column;
      text-align: center;
    }

    .nvd-card-header {
      flex-direction: column;
      align-items: flex-start;
      gap: 8px;
    }

    .nvd-popup-content {
      padding: 25px;
      margin: 10px;
      width: calc(100% - 20px);
    }

    .shodan-cve-header {
      flex-direction: column;
      align-items: flex-start;
    }
  }
</style>
</head>
<body>

<div id="dashboard-app">

  <!-- Primary Navigation -->
  <nav class="dashboard-tabs">
    <a href="#" class="active" data-tab="world">World</a>
    <a href="#" data-tab="cve">CVE Tracker</a>
    <a href="#" data-tab="foodbanks">UK Foodbanks</a>
    <a href="#" data-tab="exchange">Exchange Rates</a>
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
              <p style="color: #666; font-size: 1.1em;">Real-time vulnerability data from the official US government database</p>
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
            <p>This page uses <code>CorsProxy.io</code> to access the MSRC API directly from your browser.</p>
            <p><strong>Note:</strong> This relies on a free third-party proxy service. If you experience issues, the proxy may be temporarily unavailable.</p>
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
            <h2 style="margin-bottom: 20px; color: #333;">Microsoft Security Updates Browser</h2>
            
            <div class="msrc-demo-controls">
              <button class="msrc-demo-btn" onclick="msrcTool.previousMonth()">← Previous Month</button>
              <select class="msrc-month-selector" id="msrc-monthSelector" onchange="msrcTool.onMonthSelectorChange()">
                <!-- Dynamically populated -->
              </select>
              <button class="msrc-demo-btn" onclick="msrcTool.nextMonth()">Next Month →</button>
              <button class="msrc-demo-btn" onclick="msrcTool.fetchMonthData()" style="background: #28a745;">Load Security Updates</button>
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
                <button class="msrc-demo-btn" onclick="msrcTool.resetFilters()" style="background: #6c757d;">Reset Filters</button>
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
                This page uses <code>CorsProxy.io</code> to access the CVEDB API directly from your browser.<br>
                <strong>Note:</strong> This relies on a free third-party proxy service. If you experience issues, the proxy may be temporarily unavailable.
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
          <div style="background: #fef7e0; border: 1px solid #f6cc4d; border-radius: 10px; padding: 15px; margin-bottom: 20px;">
            <strong>ℹ️ Search Limitations:</strong> Keyword Search may not find all relevant CVEs - searches description text but not all product names
          </div>
        `;
      }
      
      // Search results header
      html += `
        <div style="margin-bottom: 25px; padding: 20px; background: #ebf8ff; border-radius: 10px; border-left: 4px solid #3182ce;">
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
          <div style="text-align: center; margin-top: 30px; padding: 20px; background: #f8fafc; border-radius: 10px;">
            <div style="display: flex; justify-content: center; align-items: center; gap: 15px; flex-wrap: wrap; margin-bottom: 15px;">
              <button onclick="nvdTool.goToPage(${this.currentPage - 1})" ${this.currentPage === 0 ? 'disabled' : ''} 
                      style="padding: 10px 20px;">← Previous</button>
              
              <span style="color: #4b5563; font-weight: 600;">
                Page ${this.currentPage + 1} of ${totalPages}
              </span>
              
              <button onclick="nvdTool.goToPage(${this.currentPage + 1})" ${!hasNext ? 'disabled' : ''} 
                      style="padding: 10px 20px;">Next →</button>
            </div>
            
            <div style="color: #6b7280; font-size: 14px;">
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
            <h2 style="color: #2d3748; font-family: 'Monaco', monospace; margin: 0;">${cve.id}</h2>
            <div style="display: flex; gap: 10px;">
              ${cvssData.score ? `<div class="nvd-cvss-badge ${cvssClass}">${cvssData.severity} - ${cvssData.score}</div>` : ''}
              ${cvssData.version ? `<div class="nvd-cvss-badge nvd-cvss-none">CVSS ${cvssData.version}</div>` : ''}
            </div>
          </div>
          
          <div style="margin-bottom: 25px;">
            <h3 style="margin-bottom: 15px; color: #374151;">🔍 Full Description</h3>
            <div style="line-height: 1.6; color: #374151; font-size: 16px; padding: 20px; background: #f8fafc; border-radius: 10px; border-left: 4px solid #667eea;">
              ${description}
            </div>
          </div>
          
          <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px; margin-bottom: 25px;">
            <div style="background: #f8fafc; padding: 15px; border-radius: 8px;">
              <div style="font-weight: 600; color: #4b5563; margin-bottom: 5px; font-size: 12px;">📅 PUBLISHED</div>
              <div style="color: #1f2937;">${publishedDate}</div>
            </div>
            
            <div style="background: #f8fafc; padding: 15px; border-radius: 8px;">
              <div style="font-weight: 600; color: #4b5563; margin-bottom: 5px; font-size: 12px;">📄 MODIFIED</div>
              <div style="color: #1f2937;">${modifiedDate}</div>
            </div>
            
            <div style="background: #f8fafc; padding: 15px; border-radius: 8px;">
              <div style="font-weight: 600; color: #4b5563; margin-bottom: 5px; font-size: 12px;">⚡ CVSS SCORE</div>
              <div style="color: #1f2937;">${cvssData.score || 'Not scored'}</div>
            </div>
            
            <div style="background: #f8fafc; padding: 15px; border-radius: 8px;">
              <div style="font-weight: 600; color: #4b5563; margin-bottom: 5px; font-size: 12px;">🎯 SEVERITY</div>
              <div style="color: #1f2937;">${cvssData.severity || 'Unknown'}</div>
            </div>
          </div>
          
          ${cvssData.vector ? `
            <div style="margin-bottom: 25px;">
              <h3 style="margin-bottom: 15px; color: #374151;">🔢 CVSS Vector</h3>
              <div style="background: #1a202c; color: #e2e8f0; padding: 15px; border-radius: 8px; font-family: monospace; font-size: 13px; word-break: break-all;">
                ${cvssData.vector}
              </div>
            </div>
          ` : ''}
          
          ${cve.references && cve.references.length > 0 ? `
            <div>
              <h3 style="margin-bottom: 15px; color: #374151;">🔗 References (${cve.references.length})</h3>
              <div style="max-height: 200px; overflow-y: auto; background: #f8fafc; padding: 15px; border-radius: 8px;">
                ${cve.references.map(ref => 
                  `<a href="${ref.url}" target="_blank" style="display: block; color: #3182ce; text-decoration: none; margin: 5px 0; padding: 8px 12px; background: white; border-radius: 6px; word-break: break-all;" onmouseover="this.style.background='#dbeafe'" onmouseout="this.style.background='white'">
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
        const proxyUrl = `https://corsproxy.io/?${encodeURIComponent(targetUrl)}`;

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

        // Use CORS proxy 
        const corsProxyUrl = 'https://corsproxy.io/';
        const url = corsProxyUrl + targetUrl;

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
</script>
</body>
</html>
