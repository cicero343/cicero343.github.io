---
title: "IP Law and Tech (Interesting Cases / Cheat Sheet)"
date: 2024-08-15
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

“One of the constant themes in the history of British copyright law is that it has been influenced by foreign and international trends and developments”<a href="#ref1" id="back1" class="reference"> [1]</a> 

**Copyright**

There are many pre-stage tests one must do before asking whether copyright has been infringed. For example, one must first ask whether the subject matter in question is original enough to be protected (the ‘skill, labour and judgement’ test).<a href="#ref2" id="back2" class="reference"> [2]</a> One must also ask if a substantial part of the work has been copied to amount to infringement.<a href="#ref3" id="back3" class="reference"> [3]</a> For the sake of keeping this blog post as short and sweet as possible. We will be glossing over these details to focus on the cases and juicy bits. 




<div id="references">
    <h2>References</h2>
    <p id="ref1">1. Bently, Sherman, Gangjee, & Johnson, Intellectual Property Law (5th edn, OUP, 2018), 44.  <a href="#back4" class="back-to-ref">[1]</a></p>
    <p id="ref2">2. Ladbroke v William Hill [1964] 1 All ER 465; see also Infopaq case (2009)<a href="#back5" class="back-to-ref">[2]</a></p>
    <p id="ref3">3. Copyright, Designs and Patents Act (CDPA) 1988, s 16(3) <a href="#back5" class="back-to-ref">[3]</a></p>
</div>
