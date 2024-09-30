---
title: About me
permalink: /about/
layout: default
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
    <title>About Me</title>
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
            --header-color-dark: #ffffff; /* White header color in dark mode */
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
            margin: 0;
            padding: 0;
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

        /* Page title styling */
        .page-title {
            margin: 0;
            padding: 0;
            color: var(--txt-color); /* Normal color in light mode */
            text-align: left; /* Ensure title is flush to the left */
        }

        [data-theme="dark"] .page-title {
            color: var(--header-color-dark); /* White header color in dark mode */
        }

        /* Header container styling */
        .header-container {
            display: flex;
            align-items: center; /* Center items vertically */
            gap: 15px; /* Space between the title and the profile image */
            margin-bottom: 20px; /* Space below the header container */
            padding: 0; /* Remove padding */
        }

        .profile-image {
            border-radius: 10px; /* Rounded edges for the image */
            width: 80px; /* Set size of the profile image */
            height: 80px; /* Set size of the profile image */
            object-fit: cover; /* Ensure the image fits within the dimensions */
        }

        /* Content container styling */
        .content-container {
            background-color: var(--container-bg-color);
            color: var(--container-txt-color);
            padding: 1rem;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            max-width: 90%; /* Ensures the content doesn't touch the edges */
            margin: 0 auto;
        }

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

        /* iFrame styling */
        .game-iframe {
            display: block; /* Ensures it takes the full width */
            margin: 20px auto; /* Centers the iFrame */
            border: none; /* Removes the default border */
        }
    </style>
</head>
<body>
    <div class="header-container">
        <h1 class="page-title">About Me</h1>
        <img src="https://avatars.githubusercontent.com/u/175522457?v=4" alt="Profile Image" class="profile-image">
    </div>

    <div class="content-container">
        <p>Hello and welcome to my site, I’m so happy you’re here! 🥳</p>
        <p>I'm just a law graduate with a passion for tech. I also enjoy a bit of music production.</p>
        <p>Here's a cool nyan cat GIF I permanently borrowed. Your day has now been blessed!</p>
    </div>

    <br>

    <img src="https://github.com/user-attachments/assets/a8b39c6a-10cd-4444-9f93-423f0972b035" alt="nyan-cat">

    <br>
    
    <iframe
        class="game-iframe"
        src="https://cicero343.github.io/mygame/index.html"
        width="640"
        height="360"
        scrolling="no">
    </iframe>

</body>
</html>



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
