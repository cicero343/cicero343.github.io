---
title: About me
permalink: /about/
---

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
  <link rel="shortcut icon" href="{{ '/assets/favicon.ico' | relative_url }}" type="image/x-icon">
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
        --container-bg-color: white; /* Default content container background in light mode */
        --container-txt-color: #000000; /* Default content container text color in light mode */
        --link-color-light: blue; /* Blue links in light mode */
        --link-hover-color-light: darkblue; /* Darker blue on hover in light mode */
        --link-color-dark: #00ff00; /* Green links in dark mode */
        --link-hover-color-dark: #00cc00; /* Slightly darker green on hover in dark mode */
    }

    /* Dark mode settings */
    [data-theme="dark"] {
        --bg-color: #000000;
        --txt-color: #ffffff;
        --container-bg-color: #333333; /* Grey background for the content container in dark mode */
        --container-txt-color: #00ff00; /* Green text color in the content container in dark mode */
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

<div class="content-container">
  <p>Hello and welcome to my site, I’m so happy you’re here! 🥳</p>
  <p>I'm just a law graduate with a passion for tech. I also enjoy a bit of music production.</p>
  <p>Here's a cool nyan cat GIF I permanently borrowed. Your day has now been blessed!</p>
</div>

<br>

![nyan-cat](https://github.com/user-attachments/assets/a8b39c6a-10cd-4444-9f93-423f0972b035)



<!-- <div class="slider">
  <img src="/assets/favicon-16x16.png">
  <img src="/assets/favicon-32x32.png">
  <img src="image3.jpg">
</div>

<style>
  .slider {
    overflow: hidden;
    width: 500px;
    height: 300px;
  }

  .slider img {
    width: 100%;
    height: auto;
    opacity: 0;
    transition: opacity 0.5s ease-in-out;
  }

  .slider img.active {
    opacity: 1;
  }
</style>

<script>
  // JavaScript code to handle image slider navigation and animation
  var images = document.querySelectorAll('.slider img');
  var currentImage = 0;

  setInterval(function() {
    images[currentImage].classList.remove('active');
    currentImage = (currentImage + 1) % images.length;
    images[currentImage].classList.add('active');
  }, 2000);
</script> -->

