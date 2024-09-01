---
title: projects
permalink: /projects/
layout: default
---

<style>
.gists {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.gist {
  flex: 1 1 200px; /* Adjust as needed */
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 4px;
  background: #f9f9f9;
}

.gist-link {
  text-decoration: none;
  color: inherit;
}

.gist-link:hover {
  background-color: #e0e0e0;
  border-radius: 4px;
  padding: 8px;
}
</style>

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

<h2>GitHub Gists</h2>

<div id="gists-container"></div>

<script>
  const gists = [
    {
      id: "b8eac1a5e5ac46d15ac8dee805388fc4", // Replace with your Gist ID
      description: "Sample Gist 1"
    },
    // Add more gists here
  ];

  const container = document.getElementById('gists-container');

  gists.forEach(gist => {
    const gistElement = document.createElement('div');
    gistElement.className = 'gist';

    const gistTitle = document.createElement('h3');
    gistTitle.textContent = gist.description;

    const gistContent = document.createElement('div');
    gistContent.textContent = 'Loading...';

    gistElement.appendChild(gistTitle);
    gistElement.appendChild(gistContent);
    container.appendChild(gistElement);

    // Fetch the Gist content
    fetch(`https://api.github.com/gists/${gist.id}`)
      .then(response => response.json())
      .then(data => {
        const files = data.files;
        const fileContent = Object.keys(files).map(fileName => {
          return files[fileName].content;
        }).join('\n\n');

        gistContent.textContent = fileContent;
      })
      .catch(error => {
        gistContent.textContent = 'Failed to load Gist content';
      });
  });
</script>
