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
        }

        [data-theme="dark"] .gist {
            background-color: var(--gist-bg-dark);
            border: 1px solid var(--gist-border-dark);
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

        .gist-card {
            border: 1px solid #e1e4e8;
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(27, 31, 35, 0.12), 0 8px 24px rgba(27, 31, 35, 0.12);
            overflow: hidden;
            transition: transform 0.2s;
        }

        .gist-card:hover {
            transform: scale(1.05);
        }

        .repo-img-dark {
            width: 100%;
            height: auto;
            border-bottom: 1px solid #e1e4e8;
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
            const gistCard = document.createElement('div');
            gistCard.className = 'gist-card';

            gistCard.innerHTML = `
              <div class="repo p-2 text-center">
                <a href="${gist.html_url}">
                  <img class="repo-img-dark w-100" alt="${gist.description || 'No Description'}" 
                       src="https://github-readme-stats.vercel.app/api/pin/?username=${username}&repo=${gist.id}&theme=transparent&show_owner=true&title_color=2be4ea&icon_color=fed33f&text_color=e8615a&bg_color=1e181e65&border_color=9c3230&border_radius=2&langs_count=5" />
                </a>
              </div>
            `;

            container.appendChild(gistCard);
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
