---
title: My Gists
permalink: /gists/
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Gists</title>
    <style>
        /* Default light mode settings */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
            --container-bg-color: white;
            --container-txt-color: #000000;
            --link-color-light: blue;
            --link-hover-color-light: darkblue;
            --link-color-dark: #00ff00;
            --link-hover-color-dark: #00cc00;
            --header-color-dark: #00ff00;
            --gist-bg-light: #f9f9f9;
            --gist-bg-dark: #1e1e1e;
            --gist-border-light: #ddd;
            --gist-border-dark: #444;
            --code-bg-light: #f1f1f1;
            --code-bg-dark: #2e2e2e;
            --code-color-light: #000000;
            --code-color-dark: #00ff00;
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --container-bg-color: #333333;
            --container-txt-color: #00ff00;
        }

        /* Apply the variables to the body */
        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
        }

        /* Link styling */
        a:link, a:visited {
            color: var(--link-color-light);
        }

        a:hover {
            color: var(--link-hover-color-light);
        }

        a:active {
            color: var(--link-color-light);
        }

        /* Dark mode overrides */
        [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
            color: var(--link-color-dark);
        }

        [data-theme="dark"] a:hover {
            color: var(--link-hover-color-dark);
        }

        [data-theme="dark"] a:active {
            color: var(--link-color-dark);
        }

        /* Wrap content in a container to apply custom styles */
        .content-container {
            background-color: var(--container-bg-color);
            color: var(--container-txt-color);
            margin: 0 auto;
            padding: 1rem;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            max-width: 90%;
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
            margin: 0;
            padding: 0;
        }

        /* Header styling */
        h2 {
            font-size: 2em;
            font-weight: bold;
            margin: 0;
            color: #333;
        }

        [data-theme="dark"] h2 {
            color: var(--header-color-dark);
        }

        .gist {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid var(--gist-border-light);
            border-radius: 4px;
            background-color: var(--gist-bg-light);
            box-shadow: 0 1px 3px rgba(27, 31, 35, 0.12), 0 8px 24px rgba(27, 31, 35, 0.12);
            transition: transform 0.2s;
        }

        [data-theme="dark"] .gist {
            background-color: var(--gist-bg-dark);
            border: 1px solid var(--gist-border-dark);
        }

        .gist:hover {
            transform: scale(1.05);
        }

        .gist h3 {
            margin-top: 0;
        }

        .gist pre {
            background-color: var(--code-bg-light);
            padding: 10px;
            border-radius: 4px;
            overflow-x: auto;
            color: var(--code-color-light);
        }

        [data-theme="dark"] .gist pre {
            background-color: var(--code-bg-dark);
            color: var(--code-color-dark);
        }

        .gist code {
            color: inherit;
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

        /* Styles for the gists grid */
        .gists-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 20px;
        }
    </style>
</head>
<body>

    <div class="theme-toggle-container">
        <button id="theme-toggle">Toggle Dark Mode</button>
    </div>
    <br>
    <h1>My GitHub Gists</h1>

    <div class="content-container">
        <div id="gists-container" class="gists-grid">
            <!-- Gists will be loaded here -->
        </div>
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
