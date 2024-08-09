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

Hello and welcome to my site, I'm so happy you're here! 🥳

I'm just a law graduate with a passion for tech. I also enjoy a bit of music production.

Here's a cool nyan cat GIF I permanently borrowed. Your day has now been blessed!

![nyan-cat](https://github.com/user-attachments/assets/a8b39c6a-10cd-4444-9f93-423f0972b035)




Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer fermentum ex sit amet tincidunt consectetur. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos.<a href="#ref4" id="back4" class="reference">[4]</a> Sed cursus nunc sagittis orci ornare porta. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Vivamus at pellentesque arcu, ac pulvinar libero.<a href="#ref5" id="back5" class="reference">[5]</a>.


<div id="references">
    <h2>References</h2>
    <p id="ref4">4. See Suspendisse nisl augue, hendrerit eu urna eu, fermentum accumsan mi. Donec orci ipsum, luctus et quam a, feugiat vulputate magna. Sed non efficitur risus. <a href="#back4" class="back-to-ref">[4]</a></p>
    <p id="ref5">5. See, e.g., Curabitur maximus aliquam vestibulum. Sed orci enim, tincidunt nec libero a, hendrerit imperdiet diam (1999). <a href="#back5" class="back-to-ref">[5]</a></p>
</div>




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

