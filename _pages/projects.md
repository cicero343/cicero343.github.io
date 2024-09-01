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

<script>
document.addEventListener("DOMContentLoaded", function() {
  fetch('https://api.github.com/users/cicero343/gists')
    .then(response => response.json())
    .then(data => {
      const container = document.querySelector('.gists');
      container.innerHTML = ''; // Clear existing content

      data.forEach(gist => {
        const gistElement = document.createElement('div');
        gistElement.className = 'gist';
        gistElement.innerHTML = `
          <a href="${gist.html_url}" target="_blank" class="gist-link">
            <p>${gist.description || 'No Description'}</p>
          </a>
        `;
        container.appendChild(gistElement);
      });
    })
    .catch(error => console.error('Error fetching Gists:', error));
});
</script>



## cicero343's GitHub 

{% if site.data.repositories.github_users %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    {% include repository/repo_user.html username=user %}
  {% endfor %}
</div>
{% endif %}

---

## GitHub Repositories

{% if site.data.repositories.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}

---

## GitHub Gists

{% if site.data.gists %}
<div class="gists d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for gist in site.data.gists %}
    <div class="gist">
      <a href="{{ https://gist.github.com/cicero343/b8eac1a5e5ac46d15ac8dee805388fc4 }}" target="_blank" class="gist-link">
        <p>{{ gist.description }}</p>
      </a>
    </div>
  {% endfor %}
</div>
{% endif %}

