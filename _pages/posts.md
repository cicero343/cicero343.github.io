---
title: All Posts
permalink: /posts/
layout: default
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Posts</title>
    <style>
        /* Ensure dark mode settings are included */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
            --container-bg-color: white;
            --container-txt-color: #000000;
            --link-color-light: blue;
            --link-hover-color-light: darkblue;
            --link-color-dark: #00ff00;
            --link-hover-color-dark: #00cc00;
            --header-color-dark: #ffffff; /* White header color in dark mode */
        }

        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --container-bg-color: #333333;
            --container-txt-color: #00ff00;
        }

        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
            margin: 0;
            padding: 0;
        }

        .posts-container {
            margin: 1rem auto;
            padding: 1rem;
            background-color: var(--container-bg-color);
            color: var(--container-txt-color);
            border-radius: 10px;
            max-width: 90%;
        }

        .post {
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: var(--container-bg-color);
        }

        .post h2 {
            margin-top: 0;
        }

        .post .date {
            font-size: 0.9em;
            color: #666;
            margin-bottom: 10px;
        }

        a:link, a:visited {
            color: var(--link-color-light);
        }

        a:hover {
            color: var(--link-hover-color-light);
        }

        a:active {
            color: var(--link-color-light);
        }

        [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
            color: var(--link-color-dark);
        }

        [data-theme="dark"] a:hover {
            color: var(--link-hover-color-dark);
        }

        [data-theme="dark"] a:active {
            color: var(--link-color-dark);
        }

        [data-theme="dark"] .post {
            background-color: #333333;
        }

        .page-title {
            margin: 1rem 0; /* Adjust top and bottom margin */
            padding: 0; /* Remove padding */
            color: var(--txt-color); /* Normal color in light mode */
            text-align: left; /* Ensure left alignment */
        }

        [data-theme="dark"] .page-title {
            color: var(--header-color-dark); /* White header color in dark mode */
        }

        hr {
            margin: 0; /* Remove margin from <hr> for flush appearance */
        }
    </style>
</head>
<body>
    <!-- Page title -->
    <h1 class="page-title">All Posts</h1>
    <hr>
    <div class="posts-container">
        {% for post in site.posts %}
          <div class="post">
            <div class="date">{{ post.date | date: "%B %d, %Y" }}</div>
            <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
          </div>
        {% endfor %}
    </div>
</body>
</html>
