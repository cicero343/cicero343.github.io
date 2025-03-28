---
title: My Projects
permalink: /projects/
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Projects</title>
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
            --header-color-dark: #00ff00; /* Green header color in dark mode */
            --gist-bg-light: #f9f9f9; /* Background color for gists in light mode */
            --gist-bg-dark: #1e1e1e; /* Background color for gists in dark mode */
            --gist-border-light: #ddd; /* Border color for gists in light mode */
            --gist-border-dark: #444; /* Border color for gists in dark mode */
            --code-bg-light: #f1f1f1; /* Background color for code blocks in light mode */
            --code-bg-dark: #2e2e2e; /* Background color for code blocks in dark mode */
            --code-color-light: #000000; /* Text color for code blocks in light mode */
            --code-color-dark: #00ff00; /* Text color for code blocks in dark mode */
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --container-bg-color: #333333; /* Grey background for the content container in dark mode */
            --container-txt-color: #00ff00; /* Green text color in the content container in dark mode */
            --gist-bg-dark: #1e1e1e; /* Background color for gists in dark mode */
            --gist-border-dark: #444; /* Border color for gists in dark mode */
            --code-bg-dark: #2e2e2e; /* Background color for code blocks in dark mode */
            --code-color-dark: #00ff00; /* Text color for code blocks in dark mode */
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
            color: var(--link-color-dark); /* Maintain green when clicked in dark mode */
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
            margin-bottom: 20px; /* Add space between the containers */
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

        /* Header styling */
        h2 {
            font-size: 2em;
            font-weight: bold;
            margin: 0; /* Remove margins to ensure no gap */
            color: #333;
        }

        [data-theme="dark"] h2 {
            color: var(--header-color-dark); /* Green header color in dark mode */
        }

        .gist {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid var(--gist-border-light); /* Default border color in light mode */
            border-radius: 4px;
            background-color: var(--gist-bg-light); /* Default background color in light mode */
        }

        [data-theme="dark"] .gist {
            background-color: var(--gist-bg-dark); /* Background color in dark mode */
            border: 1px solid var(--gist-border-dark); /* Border color in dark mode */
        }

        .gist h3 {
            margin-top: 0;
        }

        .gist pre {
            background-color: var(--code-bg-light); /* Background color for code blocks in light mode */
            padding: 10px;
            border-radius: 4px;
            overflow-x: auto;
            color: var(--code-color-light); /* Text color for code blocks in light mode */
        }

        [data-theme="dark"] .gist pre {
            background-color: var(--code-bg-dark); /* Background color for code blocks in dark mode */
            color: var(--code-color-dark); /* Text color for code blocks in dark mode */
        }

        .gist code {
            color: inherit; /* Ensure the code inherits color from the pre element */
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

    /* Ensure the iframe is responsive */
    .responsive-iframe {
        width: 100%; /* Take full width of the parent container */
        max-width: 505px; /* Set a max width to keep it within standard smartphone width */
        height: 167px; /* Set the height according to your iframe content */
        border: none; /* Removes the border around the iframe */
    }

    /* Container styling without centering */
    .iframe-container {
        overflow: hidden; /* Hide overflow to prevent stretching */
    }

    </style>
</head>
<body>

    <h1> My 2D Java Game </h1>
    <hr>

    <br>
    
    <div class="iframe-container">
    <iframe
        class="responsive-iframe"
        frameborder="0"
        src="https://itch.io/embed/2997483?linkback=true&amp;dark=true">
        <a href="https://cicero343.itch.io/serenityskies">SerenitySkies by cicero343</a>
    </iframe>
    </div>

    <br>
    <h1>My GitHub Projects</h1>

    <hr>

    <br>

<!-- Repository Preview Section -->
<div class="content-container">
    <h3>IoCFinder</h3>
    <a href="https://github.com/cicero343/IoCFinder" target="_blank" class="repo-link">
        <img class="repo-img-dark fill-div" alt="IoCFinder" src="https://github-readme-stats.vercel.app/api/pin/?username=cicero343&repo=IoCFinder&theme=transparent&show_owner=true&title_color=2be4ea&icon_color=fed33f&text_color=e8615a&bg_color=1e181e65&border_color=9c3230&border_radius=2&langs_count=5">
    </a>
</div>

<div class="content-container">
    <h3>KQL-Queries</h3>
    <a href="https://github.com/cicero343/KQL-Queries" target="_blank" class="repo-link">
        <img class="repo-img-dark fill-div" alt="KQL-Queries" src="https://github-readme-stats.vercel.app/api/pin/?username=cicero343&repo=KQL-Queries&theme=transparent&show_owner=true&title_color=2be4ea&icon_color=fed33f&text_color=e8615a&bg_color=1e181e65&border_color=9c3230&border_radius=2&langs_count=5">
    </a>
</div>

<div class="content-container">
    <h3>PopupWindowsAPI</h3>
    <a href="https://github.com/cicero343/PopupWindowsAPI" target="_blank" class="repo-link">
        <img class="repo-img-dark fill-div" alt="PopupWindowsAPI" src="https://github-readme-stats.vercel.app/api/pin/?username=cicero343&repo=PopupWindowsAPI&theme=transparent&show_owner=true&title_color=2be4ea&icon_color=fed33f&text_color=e8615a&bg_color=1e181e65&border_color=9c3230&border_radius=2&langs_count=5">
    </a>
</div>

<div class="content-container">
    <h3>CyberSecBookmarks</h3>
    <a href="https://github.com/cicero343/CyberSecBookmarks" target="_blank" class="repo-link">
        <img class="repo-img-dark fill-div" alt="CyberSecBookmarks" src="https://github-readme-stats.vercel.app/api/pin/?username=cicero343&repo=CyberSecBookmarks&theme=transparent&show_owner=true&title_color=2be4ea&icon_color=fed33f&text_color=e8615a&bg_color=1e181e65&border_color=9c3230&border_radius=2&langs_count=5">
    </a>
</div>

    <div class="content-container">
        <div id="gists-container">
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

</body>
</html>
