---
title: projects
permalink: /projects/
layout: default
---

<style>
  .gists {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.gist {
  flex: 1 1 calc(50% - 1rem);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 1rem;
  border-radius: 4px;
  background-color: var(--bg-color-light);
}

.gist-link {
  text-decoration: none;
  color: var(--txt-color);
}

.gist-link:hover {
  text-decoration: underline;
}

@media (max-width: 768px) {
  .gist {
    flex: 1 1 100%;
  }
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
      <a href="{{ gist.url }}" target="_blank" class="gist-link">
        <p>{{ gist.description }}</p>
      </a>
    </div>
  {% endfor %}
</div>
{% endif %}

