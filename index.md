---
Title: A Diary of IT Projects
---

<title>A Diary of IT Projects</title>

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
</head>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toggle Dark Mode</title>
    <style>
        /* Default light mode settings */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
        }

        /* Apply the variables to the body */
        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
        }
    </style>
</head>
<body>
    <button id="theme-toggle">Toggle Dark Mode</button>

 
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

<br>

<img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="115" height="115" style="border-radius: 20px;">
<script src="https://tryhackme.com/badge/2125035"></script>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clickable Links</title>
    <style>
        body {
            margin: 0; /* Ensure no default margin */
            padding: 0;
            font-family: Arial, sans-serif;
        }

        .link-container {
            padding: 20px; /* Add padding to the container for spacing */
        }

        .link-list {
            list-style: none;
            padding: 0;
            margin: 0; /* Ensure no default margin */
            display: flex;
            gap: 10px;
        }

        .link-list a {
            text-decoration: none;
            color: #007bff;
            font-size: 14px; /* Adjust the size here */
        }

        .link-list a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="link-container">
        <ul class="link-list">
            <li><a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank">LinkedIn</a></li>
            <li><a href="https://github.com/cicero343" target="_blank">GitHub</a></li>
            <li><a href="https://tryhackme.com/p/bdonovan343" target="_blank">TryHackMe</a></li>
        </ul>
    </div>
</body>
</html>
