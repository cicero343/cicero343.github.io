---
Title: A Diary of IT Projects
---

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
  <style>
      /* Dark mode settings for icons */
      [data-theme="dark"] .icon {
          fill: #ffffff; /* Light color for icons in dark mode */
      }

      /* Light mode settings for icons */
      [data-theme="light"] .icon {
          fill: #000000; /* Dark color for icons in light mode */
      }
  </style>
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
            --link-color-light: blue; /* Blue links in light mode */
            --link-hover-color-light: darkblue; /* Darker blue on hover in light mode */
            --link-color-dark: #00ff00; /* Green links in dark mode */
            --link-hover-color-dark: #00cc00; /* Slightly darker green on hover in dark mode */
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            /* Link colors are handled by the variables above */
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
    <title>Social Media Icons</title>
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
            gap: 10px; /* Adds space between each link */
            align-items: center; /* Align items vertically */
        }
        .link-list a {
            display: flex; /* Make the anchor tags flex containers */
            align-items: center; /* Center content vertically */
            justify-content: center; /* Center content horizontally */
            width: 24px; /* Set width for icons */
            height: 24px; /* Set height for icons */
            text-decoration: none;
        }
        .link-list img {
            width: 100%; /* Scale icon to fit anchor tag */
            height: 100%; /* Scale icon to fit anchor tag */
        }
        .link-list a:hover {
            opacity: 0.8; /* Slightly change opacity on hover for better visual feedback */
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
                <li><a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank"><img src="https://www.svgrepo.com/show/391478/linkedin.svg" alt="LinkedIn" class="icon"></a></li>
                <li><a href="https://github.com/cicero343" target="_blank"><img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.svg" alt="GitHub" class="icon"></a></li>
            </ul>
        </div>
    </div>
</body>
</html>
