---
title: projects
permalink: /projects/
layout: default
---

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

