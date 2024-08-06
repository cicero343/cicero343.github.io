---
Title: A Diary of IT Projects
---
<img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="125" height="125" style="border-radius: 20px;">

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clickable Links</title>
    <style>
        .link-list {
            list-style: none;
            padding: 0;
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
    <ul class="link-list">
        <li><a href="https://www.linkedin.com/in/yourprofile" target="_blank">LinkedIn</a></li>
        <li><a href="https://github.com/yourusername" target="_blank">GitHub</a></li>
        <li><a href="https://twitter.com/yourusername" target="_blank">Twitter</a></li>
    </ul>
</body>
</html>


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
