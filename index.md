---
Title: A Diary of IT Projects
layout: default
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
          transition: transform 0.2s, filter 0.3s ease, brightness 0.3s ease;
          margin-left: 10px; /* Reduced space between the icons */
      }

      /* Dark mode settings */
      [data-theme="dark"] .icon {
          filter: invert(1) brightness(1.5); /* Invert colors for dark mode */
      }

      /* Layout adjustments */
      .header-container {
          display: flex;
          align-items: center; /* Center items vertically */
          margin-bottom: 10px; /* Add space between header and content below */
      }

      .header-container a {
          margin-right: 5px; /* Reduced space between the social icons */
      }

      .badge-container {
          display: flex;
          flex-direction: column; /* Stack badges vertically by default */
          margin-top: 15px;
      }

      .tryhackme-badge {
          margin-bottom: 5px; /* Space below TryHackMe badge */
      }

      .hackthebox-badge {
          margin-left: 15px; /* Space between HackTheBox badge and TryHackMe badge */
      }

      /* Responsive layout for larger screens */
      @media (min-width: 768px) {
          .header-container {
              justify-content: flex-start; /* Align items at the start */
          }

          .badge-container {
              flex-direction: column; /* Stack badges vertically on larger screens */
              align-items: flex-start;
          }
      }

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

<html lang="en">
<body>
    <div class="header-container">
        <a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank">
            <img src="https://www.svgrepo.com/show/391478/linkedin.svg" alt="LinkedIn" class="icon">
        </a>
        <a href="https://github.com/cicero343" target="_blank">
            <img src="https://upload.wikimedia.org/wikipedia/commons/9/91/Octicons-mark-github.svg" alt="GitHub" class="icon">
        </a>
        <div class="hackthebox-badge">
            <a href="https://app.hackthebox.com/users/2067546" target="_blank">
                <img src="https://www.hackthebox.eu/badge/image/2067546" alt="Hack The Box Profile" width="150" height="34">
            </a>
        </div>
    </div>
    
    <div class="badge-container">
        <div class="tryhackme-badge">
            <script src="https://tryhackme.com/badge/2125035"></script>
        </div>
    </div>

<h2 class="post-list-heading">Recent Posts</h2>
<ul class="post-list">
  {% for post in site.posts limit:5 %}
    <li style="margin-bottom: 10px;"> <!-- Reduced bottom margin between posts -->
      <span class="post-meta" style="font-size: 0.85em; color: #666;">{{ post.date | date: "%b %d, %Y" }}</span>
      <h3 style="font-size: 1.1em; margin: 3px 0;"> <!-- Reduced top and bottom margins -->
        <a class="post-link" href="{{ post.url }}" style="font-size: 1.1em;">
          {{ post.title }}
        </a>
      </h3>
    </li>
  {% endfor %}
</ul>

    <p class="rss-subscribe">subscribe <a href="/feed.xml">via RSS</a></p>

</body>
</html>
