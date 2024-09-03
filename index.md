---
Title: A Diary of IT Projects
---

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
  <style>
      /* Default styles for icons */
      .icon {
          filter: invert(0); /* Default to no inversion */
          width: 24px;
          height: 24px;
          margin-left: 15px; /* Add space between the toggle button and icons */
      }

      /* Dark mode settings */
      [data-theme="dark"] .icon {
          filter: invert(1); /* Invert colors for dark mode */
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

        /* Layout adjustments */
        .header-container {
            display: flex;
            justify-content: flex-start; /* Align items at the start */
            align-items: center; /* Center the items vertically */
            margin-bottom: 10px; /* Add space between header and content below */
        }

        .theme-toggle {
            margin-right: auto; /* Push the icons to the right side */
        }

        .tryhackme-badge {
            margin-top: 15px; /* Add some space above the TryHackMe badge */
        }
    </style>
</head>
<body>
    <div class="header-container">
        <button id="theme-toggle" class="theme-toggle">Toggle Dark Mode</button>
        <a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank"><img src="https://www.svgrepo.com/show/391478/linkedin.svg" alt="LinkedIn" class="icon"></a>
        <a href="https://github.com/cicero343" target="_blank"><img src="https://upload.wikimedia.org/wikipedia/commons/9/91/Octicons-mark-github.svg" alt="GitHub" class="icon"></a>
    </div>
    
    <div class="tryhackme-badge">
        <script src="https://tryhackme.com/badge/2125035"></script>
    </div>

<div style="margin-bottom: 5px;">
    <a href="https://app.hackthebox.com/users/2067546" target="_blank">
        <img src="https://www.hackthebox.eu/badge/image/2067546" alt="Hack The Box Profile" width="150" height="34">
    </a>
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
