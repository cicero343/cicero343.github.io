---
title: projects
permalink: /projects/
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Projects</title>
    <style>
        /* Default light mode settings */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
            --container-bg-color: white; /* Default content container background in light mode */
            --container-txt-color: #000000; /* Default content container text color in light mode */
            --link-color-light: blue; /* Blue links in light mode */
            --link-hover-color-light: darkblue; /* Darker blue on hover in light mode */
            --link-color-dark: #00ff00; /* Green links in dark mode */
            --link-hover-color-dark: #00cc00; /* Slightly darker green on hover in dark mode */
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --container-bg-color: #333333; /* Grey background for the content container in dark mode */
            --container-txt-color: #00ff00; /* Green text color in the content container in dark mode */
        }

        /* Apply the variables to the body */
        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
        }

        /* Link styling */
        a:link, a:visited {
            color: var(--link-color-light); /* Default blue for light mode links */
        }

        a:hover {
            color: var(--link-hover-color-light); /* Hover color in light mode */
        }

        a:active {
            color: var(--link-color-light); /* Active link color in light mode */
        }

        /* Dark mode overrides */
        [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
            color: var(--link-color-dark); /* Green links in dark mode */
        }

        [data-theme="dark"] a:hover {
            color: var(--link-hover-color-dark); /* Hover color in dark mode */
        }

        [data-theme="dark"] a:active {
            color: var (--link-color-dark); /* Maintain green when clicked in dark mode */
        }

        /* Wrap content in a container to apply custom styles */
        .content-container {
            background-color: var(--container-bg-color);
            color: var(--container-txt-color);
            margin: 0 auto;
            padding: 1rem;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            max-width: 90%; /* Ensures the content doesn't touch the edges */
        }

        /* Adjust the container width for different screen sizes */
        @media only screen and (max-width: 768px) {
            .content-container {
                max-width: 95%;
            }
        }

        @media only screen and (max-width: 480px) {
            .content-container {
                max-width: 98%;
            }
        }

        /* Styles for the theme toggle */
        .theme-toggle-container {
            margin-bottom: 20px; /* Space below the button, adjust as needed */
        }
    </style>
</head>
<body>
    <div class="theme-toggle-container">
        <button id="theme-toggle">Toggle Dark Mode</button>
    </div>

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

    <div class="content-container">
    <div id="gists-container">
      <!-- Gists will be loaded here -->
    </div>

    <script>
      async function fetchGists() {
        try {
          const username = 'cicero343'; // Your GitHub username
          const response = await fetch(`https://api.github.com/users/${username}/gists`);
          const gists = await response.json();

          if (gists.length === 0) {
            document.getElementById('gists-container').innerText = 'No Gists found.';
            return;
          }

          const container = document.getElementById('gists-container');
          gists.forEach(gist => {
            const gistDiv = document.createElement('div');
            gistDiv.className = 'gist';

            const fileName = Object.keys(gist.files)[0];
            const file = gist.files[fileName];

            gistDiv.innerHTML = `
              <h3>${gist.description || 'No Description'}</h3>
              <pre><code>Loading preview...</code></pre>
              <a href="${gist.html_url}" target="_blank">View on GitHub</a>
            `;

            container.appendChild(gistDiv);

            // Fetch the raw content to display the first 5 lines
            fetch(file.raw_url)
              .then(response => response.text())
              .then(content => {
                const codeElement = gistDiv.querySelector('code');
                codeElement.textContent = content.split('\n').slice(0, 5).join('\n') + '...';
              })
              .catch(error => {
                gistDiv.querySelector('code').textContent = 'Unable to load preview';
              });
          });
        } catch (error) {
          document.getElementById('gists-container').innerText = 'Failed to load Gists.';
        }
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
</div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const themeToggleButton = document.getElementById('theme-toggle');
            const currentTheme = localStorage.getItem('theme');

            if (currentTheme) {
                document.documentElement.setAttribute('data-theme', currentTheme);
            }

            themeToggleButton.addEventListener('click', () => {
                const newTheme = document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
                document.documentElement.setAttribute('data-theme', newTheme);
                localStorage.setItem('theme', newTheme);
            });
        });
    </script>
</body>
</html>
