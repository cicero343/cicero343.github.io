---
title: Posts
permalink: /posts/
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Posts</title>
    <style>
        /* Ensure dark mode settings are included */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
            --container-bg-color: white;
            --container-txt-color: #000000;
            --link-color-light: blue;
            --link-hover-color-light: darkblue;
            --link-color-dark: #00ff00;
            --link-hover-color-dark: #00cc00;
            --header-color-dark: #00ff00; /* Green header color in dark mode */
        }

        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --container-bg-color: #333333;
            --container-txt-color: #00ff00;
        }

        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
            margin: 0;
            padding: 0;
        }

        .theme-toggle-container {
            margin: 1rem; /* Adjust as needed */
            padding: 0;
        }

        .posts-container {
            margin: 1rem auto;
            padding: 1rem;
            background-color: var(--container-bg-color);
            color: var(--container-txt-color);
            border-radius: 10px;
            max-width: 90%;
        }

        .post {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: var(--container-bg-color);
        }

        .post h2 {
            margin-top: 0;
        }

        .post .date {
            font-size: 0.9em;
            color: #666;
            margin-bottom: 10px;
        }

        a:link, a:visited {
            color: var(--link-color-light);
        }

        a:hover {
            color: var(--link-hover-color-light);
        }

        a:active {
            color: var(--link-color-light);
        }

        [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
            color: var(--link-color-dark);
        }

        [data-theme="dark"] a:hover {
            color: var(--link-hover-color-dark);
        }

        [data-theme="dark"] a:active {
            color: var(--link-color-dark);
        }

        [data-theme="dark"] .post {
            background-color: #333333;
        }

        /* Styling for the page title */
        .page-title {
            margin: 1rem 0;
            padding-left: 1rem; /* Align to the left with padding */
            color: var(--txt-color); /* Normal color in light mode */
        }

        [data-theme="dark"] .page-title {
            color: var(--header-color-dark); /* Green header color in dark mode */
        }
    </style>
</head>
<body>

    <div class="theme-toggle-container">
        <button id="theme-toggle">Toggle Dark Mode</button>
    </div>

    <h1 class="page-title">Posts</h1>
    <hr>
    <div class="posts-container">
        {% for post in site.posts %}
          <div class="post">
            <div class="date">{{ post.date | date: "%B %d, %Y" }}</div>
            <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
            <p>{{ post.excerpt }}</p>
          </div>
        {% endfor %}
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