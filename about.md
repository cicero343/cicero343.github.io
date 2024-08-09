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




As stated at the top of this Article, the Latin maxim *nemo dat quod non habet*—one cannot give what they do not have (or, you have to have it to give it)<a href="#ref4" id="back4" class="reference">[4]</a>—holds a special place in our law. The *nemo dat* principle is so strong that it has broad applications associated with the transfer of most assets, not just real property<a href="#ref5" id="back5" class="reference">[5]</a>.

<div id="references">
    <h2>References</h2>
    <p id="ref4">4. See BLACK’S LAW DICTIONARY 1933 (10th ed. 2014) (“No one gives what he does not have . . . .”); Kevin E. Davis, The Effects of Forfeiture on Third Parties, 48 MCGILL L.J. 183, 196–97 (2003) (articulating the “common law rule of *nemo dat quod non habet* (‘he who hath not cannot give’)”). <a href="#back4" class="back-to-ref">[Return to reference]</a></p>
    <p id="ref5">5. See, e.g., Stephen T. Black, Psst! Wanna Buy a Bridge? IP Transfers of Non-Existent Property, 31 GA. ST. U. L. REV. 523, 529–30 (2015) (discussing the broader applications of *nemo dat*-like norms); Adam J. Levitin, Finding Nemo: Rediscovering the Virtues of Negotiability in the Wake of Enron, 2007 COLUM. BUS. L. REV. 83, 90 (2007) (defining “the commercial law principle of *nemo dat quod non habet*—you can transfer only what you have”) (emphasis added); Carl S. Bjerre, Secured Transactions Inside Out: Negative Pledge Covenants, Property and Perfection, 84 CORNELL L. REV. 305, 333 (1999) (“[I]f the owner grants a security interest to one lender, the *nemo dat* principle standing alone would dictate that the owner..."). <a href="#back5" class="back-to-ref">[Return to reference]</a></p>
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

