---
title: projects
permalink: /projects/
layout: default
---

## cicero343's GitHub 

{% if site.data.github_users %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.github_users %}
    {% include repository/repo_user.html username=user %}
  {% endfor %}
</div>
{% endif %}

---

<!--
## GitHub Repositories

{% if site.data.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.github_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}
-->

## GitHub Gists

<div id="gists-container">
  <!-- The Gists will be loaded here dynamically by JavaScript -->
</div>

<script>
  async function fetchGists() {
    const username = 'cicero343'; // Replace with your GitHub username
    const response = await fetch(`https://api.github.com/users/${username}/gists`);
    const gists = await response.json();

    const container = document.getElementById('gists-container');
    
    gists.forEach(gist => {
      const gistDiv = document.createElement('div');
      gistDiv.className = 'gist';

      // Limit to first 5 lines of the first file in the Gist
      const fileName = Object.keys(gist.files)[0];
      const file = gist.files[fileName];

      gistDiv.innerHTML = `
        <h3>${gist.description || 'No Description'}</h3>
        <pre><code>${file.content.split('\n').slice(0, 5).join('\n')}...</code></pre>
        <a href="${gist.html_url}" target="_blank">View on GitHub</a>
      `;

      container.appendChild(gistDiv);
    });
  }

  fetchGists();
</script>

<style>
  .gist {
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    background-color: #f9f9f9;
  }

  .gist h3 {
    margin-top: 0;
  }

  .gist pre {
    background-color: #f1f1f1;
    padding: 10px;
    border-radius: 4px;
    overflow-x: auto;
  }

  .gist a {
    display: inline-block;
    margin-top: 10px;
    color: #0366d6;
    text-decoration: none;
    font-weight: bold;
  }

  .gist a:hover {
    text-decoration: underline;
  }
</style>
