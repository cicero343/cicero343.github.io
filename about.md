---
title: About me
permalink: /about/
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
        --bg-image-light: url('https://png.pngtree.com/background/20220726/original/pngtree-digital-stream-or-binary-code-data-on-matrix-background-picture-image_1821715.jpg'); /* Light mode background image */
        --bg-filter-light: brightness(1.2) contrast(1.2); /* Adjust brightness and contrast for better visibility in light mode */
        --txt-color-light: #000000; /* Text color in light mode */
    }

    /* Dark mode settings */
    [data-theme="dark"] {
        --bg-image-dark: url('https://png.pngtree.com/background/20220726/original/pngtree-digital-stream-or-binary-code-data-on-matrix-background-picture-image_1821715.jpg'); /* Dark mode background image */
        --bg-filter-dark: none; /* No filter for dark mode, use original image */
        --txt-color-dark: #ffffff; /* Text color in dark mode */
    }

    /* Apply the variables to the body */
    body {
        background-image: var(--bg-image-light); /* Default background image */
        background-size: cover; /* Ensure the image covers the entire background */
        background-repeat: no-repeat; /* Prevent image repetition */
        background-position: center; /* Center the image */
        color: var(--txt-color-light); /* Default text color */
        filter: var(--bg-filter-light); /* Apply light mode filter */
    }

    /* Dark mode overrides */
    [data-theme="dark"] body {
        background-image: var(--bg-image-dark); /* Dark mode background image */
        filter: var(--bg-filter-dark); /* Apply dark mode filter */
        color: var(--txt-color-dark); /* Dark mode text color */
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

Hello and welcome to my site, I'm so happy you're here! 🥳

I'm just a law graduate with a passion for tech. I also enjoy a bit of music production.

Here's a cool nyan cat GIF I permanently borrowed. Your day has now been blessed!

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

