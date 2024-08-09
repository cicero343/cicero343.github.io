---
Title: A Diary of IT Projects
---

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

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Side by Side Images with Horizontal Links</title>
    <style>
        .container {
            display: flex; /* Use flexbox to place items side by side */
            gap: 10px; /* Adds space between the items */
            align-items: flex-start; /* Align items at the top */
        }
        .profile-image {
            border-radius: 20px; /* Apply border radius to profile image */
        }
        .badge-links {
            display: flex;
            flex-direction: column; /* Arrange badge and links vertically */
            gap: 10px; /* Adds space between the badge and the links */
        }
        .link-list {
            list-style: none;
            padding: 0;
            margin: 0;
            display: flex; /* Arrange links horizontally */
            gap: 20px; /* Adds space between each link */
        }
        .link-list a {
            text-decoration: none;
            color: #007bff;
        }
        .link-list a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="100" height="100" alt="Profile Image" class="profile-image">
        <div class="badge-links">
            <div class="tryhackme-badge">
                <script src="https://tryhackme.com/badge/2125035"></script>
            </div>
            <ul class="link-list">
                <li><a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank">LinkedIn</a></li>
                <li><a href="https://github.com/cicero343" target="_blank">GitHub</a></li>
                <li><a href="https://tryhackme.com/p/cicero343" target="_blank">TryHackMe</a></li>
            </ul>
        </div>
    </div>
</body>
</html>
