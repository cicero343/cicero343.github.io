---
title: A Diary of IT Projects
layout: home
---

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
</head>

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
        color: var(--link-color-light); /* Use variable for link color */
    }
    .link-list a:hover {
        text-decoration: underline;
        color: var(--link-hover-color-light); /* Use variable for hover color */
    }
</style>
