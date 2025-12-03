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
            --code-bg-light: #f4f4f4;
            --code-bg-dark: #0d1117;
            --code-color-light: #000000;
            --code-color-dark: #00ff00;
            --repo-bg-light: #ffffff;
            --repo-bg-dark: #161b22;
            --repo-border-light: #d0d7de;
            --repo-border-dark: #30363d;
            --repo-text-light: #24292f;
            --repo-text-dark: #c9d1d9;
            --repo-desc-light: #57606a;
            --repo-desc-dark: #8b949e;
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
            margin-bottom: 20px;
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
            margin: 0;
            color: #333;
        }

        [data-theme="dark"] h2 {
            color: var(--header-color-dark);
        }

        /* Repository card styling */
        .repo-card {
            background-color: var(--repo-bg-light);
            border: 1px solid var(--repo-border-light);
            border-radius: 6px;
            padding: 16px;
            margin-bottom: 16px;
            transition: box-shadow 0.2s ease;
            text-decoration: none;
            display: block;
            color: var(--repo-text-light);
        }

        [data-theme="dark"] .repo-card {
            background-color: var(--repo-bg-dark);
            border-color: var(--repo-border-dark);
            color: var(--repo-text-dark);
        }

        .repo-card:hover {
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.15);
            text-decoration: none;
        }

        [data-theme="dark"] .repo-card:hover {
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.4);
        }

        .repo-card h3 {
            margin: 0 0 8px 0;
            font-size: 1.2em;
            color: var(--link-color-light);
        }

        [data-theme="dark"] .repo-card h3 {
            color: var(--link-color-dark);
        }

        .repo-description {
            color: var(--repo-desc-light);
            margin: 8px 0;
            font-size: 0.95em;
        }

        [data-theme="dark"] .repo-description {
            color: var(--repo-desc-dark);
        }

        .repo-stats {
            display: flex;
            gap: 16px;
            font-size: 0.85em;
            color: var(--repo-desc-light);
            margin-top: 12px;
        }

        [data-theme="dark"] .repo-stats {
            color: var(--repo-desc-dark);
        }

        .repo-stat {
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .language-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            display: inline-block;
        }

        /* Gist styling */
        .gist {
            margin-bottom: 20px;
            padding: 16px;
            border: 1px solid var(--gist-border-light);
            border-radius: 6px;
            background-color: var(--gist-bg-light);
        }

        [data-theme="dark"] .gist {
            background-color: var(--gist-bg-dark);
            border-color: var(--gist-border-dark);
        }

        .gist h3 {
            margin-top: 0;
            margin-bottom: 12px;
            color: var(--container-txt-color);
        }

        .gist pre {
            background-color: var(--code-bg-light) !important;
            padding: 12px;
            border-radius: 6px;
            overflow-x: auto;
            color: var(--code-color-light) !important;
            margin: 0;
            line-height: 1.5;
        }

        [data-theme="dark"] .gist pre {
            background-color: var(--code-bg-dark) !important;
            color: var(--code-color-dark) !important;
        }

        .gist code {
            color: inherit !important;
            background-color: transparent !important;
            font-family: 'Courier New', Courier, monospace;
            font-size: 0.9em;
        }

        .gist a {
            display: inline-block;
            margin-top: 10px;
            color: var(--link-color-light);
            text-decoration: none;
            font-weight: bold;
        }

        [data-theme="dark"] .gist a {
            color: var(--link-color-dark);
        }

        .gist a:hover {
            text-decoration: underline;
        }

        /* Ensure the iframe is responsive */
        .responsive-iframe {
            width: 100%;
            max-width: 505px;
            height: 167px;
            border: none;
        }

        /* Container styling without centering */
        .iframe-container {
            overflow: hidden;
        }

        /* Loading state */
        .loading {
            text-align: center;
            padding: 20px;
            color: var(--repo-desc-light);
        }

        [data-theme="dark"] .loading {
            color: var(--repo-desc-dark);
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
<div id="repos-container">
    <div class="loading">Loading repositories...</div>
</div>

<h1>My GitHub Gists</h1>

<hr>

<br>

<div class="content-container">
    <div id="gists-container">
        <div class="loading">Loading gists...</div>
    </div>
</div>

<script>
    // Language colors mapping (common languages)
    const languageColors = {
        'JavaScript': '#f1e05a',
        'Python': '#3572A5',
        'Java': '#b07219',
        'HTML': '#e34c26',
        'CSS': '#563d7c',
        'TypeScript': '#2b7489',
        'Shell': '#89e051',
        'C++': '#f34b7d',
        'C': '#555555',
        'Go': '#00ADD8',
        'Ruby': '#701516',
        'PHP': '#4F5D95',
        'PowerShell': '#012456',
        'KQL': '#00758F'
    };

    async function fetchRepositories() {
        try {
            const username = 'cicero343';
            const repos = ['IoCFinder', 'KQL-Queries', 'CyberSecBookmarks', 'RaffleTool', 'PopupWindowsAPI'];
            const container = document.getElementById('repos-container');
            container.innerHTML = '';

            for (const repoName of repos) {
                const response = await fetch(`https://api.github.com/repos/${username}/${repoName}`);
                const repo = await response.json();

                const repoCard = document.createElement('div');
                repoCard.className = 'content-container';
                
                const languageColor = languageColors[repo.language] || '#858585';
                
                repoCard.innerHTML = `
                    <a href="${repo.html_url}" target="_blank" class="repo-card">
                        <h3>${repo.name}</h3>
                        <div class="repo-description">${repo.description || 'No description available'}</div>
                        <div class="repo-stats">
                            ${repo.language ? `
                                <span class="repo-stat">
                                    <span class="language-dot" style="background-color: ${languageColor}"></span>
                                    ${repo.language}
                                </span>
                            ` : ''}
                            <span class="repo-stat">⭐ ${repo.stargazers_count}</span>
                            <span class="repo-stat">🔀 ${repo.forks_count}</span>
                        </div>
                    </a>
                `;

                container.appendChild(repoCard);
            }
        } catch (error) {
            document.getElementById('repos-container').innerHTML = '<div class="loading">Failed to load repositories.</div>';
            console.error('Error fetching repositories:', error);
        }
    }

    async function fetchGists() {
        try {
            const username = 'cicero343';
            const response = await fetch(`https://api.github.com/users/${username}/gists`);
            const gists = await response.json();

            const container = document.getElementById('gists-container');
            
            if (gists.length === 0) {
                container.innerHTML = '<div class="loading">No Gists found.</div>';
                return;
            }

            container.innerHTML = '';

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
                        codeElement.textContent = content.split('\n').slice(0, 5).join('\n') + '\n...';
                    })
                    .catch(error => {
                        gistDiv.querySelector('code').textContent = 'Unable to load preview';
                    });
            });
        } catch (error) {
            document.getElementById('gists-container').innerHTML = '<div class="loading">Failed to load Gists.</div>';
            console.error('Error fetching gists:', error);
        }
    }

    // Load both repositories and gists when the page loads
    fetchRepositories();
    fetchGists();
</script>

</body>
</html>
