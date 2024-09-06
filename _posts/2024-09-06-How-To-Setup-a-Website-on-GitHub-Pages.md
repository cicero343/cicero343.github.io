---
title: "How To Setup a Website on GitHub Pages"
date: 2024-09-06
layout: default
---

<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">How To Setup a Website on GitHub Pages</h1>
  <p class="post-meta">
    <time class="dt-published" datetime="2024-09-06T00:00:00+00:00" itemprop="datePublished">Sep 06, 2024</time>
  </p>
</header>

<div class="post-content e-content" itemprop="articleBody">

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
  
    <!-- Add Font Awesome for the up arrow icon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">

    <style>
        /* Default light mode settings */
        :root {
            --bg-color: #ffffff;
            --txt-color: #000000;
            --link-color-light: blue; /* Blue links in light mode */
            --link-hover-color-light: darkblue; /* Darker blue on hover in light mode */
            --button-bg-light: #000000; /* Black background for button in light mode */
            --button-text-light: #ffffff; /* White text color for button in light mode */
            --button-bg-hover-light: #333333; /* Darker background for button on hover in light mode */
        }

        /* Dark mode settings */
        [data-theme="dark"] {
            --bg-color: #000000;
            --txt-color: #ffffff;
            --link-color-dark: #00ff00; /* Green links in dark mode */
            --link-hover-color-dark: #00cc00; /* Slightly darker green on hover in dark mode */
            --button-bg-dark: #000000; /* Black background for button in dark mode */
            --button-text-dark: #00ff00; /* Green text color for button in dark mode */
            --button-bg-hover-dark: #333333; /* Darker background for button on hover in dark mode */
        }

        /* Apply the variables to the body */
        body {
            background-color: var(--bg-color);
            color: var(--txt-color);
        }

        /* Link styling */
        a:link, a:visited {
            color: var(--link-color-light); /* Use default blue color for light mode */
        }

        /* Dark mode overrides */
        [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
            color: var(--link-color-dark); /* Use green color for dark mode */
        }

        a:hover {
            color: var(--link-hover-color-light); /* Hover color in light mode */
        }

        /* Dark mode hover overrides */
        [data-theme="dark"] a:hover {
            color: var(--link-hover-color-dark); /* Hover color in dark mode */
        }

        a:active {
            color: inherit; /* Maintain inherited color when clicked */
        }

        /* Dark mode active overrides */
        [data-theme="dark"] a:active {
            color: var(--link-color-dark); /* Maintain green when clicked in dark mode */
        }

        /* Circular Back to Top Button */
        .back-to-top {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: var(--button-bg-light); /* Light mode background */
            color: var(--button-text-light); /* Light mode icon color */
            border: none;
            border-radius: 50%; /* Makes the button circular */
            width: 50px; /* Diameter of the circle */
            height: 50px; /* Diameter of the circle */
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px; /* Icon size */
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3); /* Shadow effect */
            transition: background-color 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
            display: none; /* Initially hidden */
        }

        .back-to-top:hover {
            background-color: var(--button-bg-hover-light); /* Darker background on hover */
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.5);
        }

        /* Dark mode overrides for the Back to Top button */
        [data-theme="dark"] .back-to-top {
            background-color: var(--button-bg-dark); /* Dark mode background */
            color: var(--button-text-dark); /* Dark mode icon color */
        }

        [data-theme="dark"] .back-to-top:hover {
            background-color: var(--button-bg-hover-dark); /* Darker background on hover in dark mode */
        }
    </style>
</head>

<body>

    <!-- Back to Top Button -->
    <button onclick="topFunction()" class="back-to-top" title="Go to top">
        <i class="fas fa-chevron-up"></i> <!-- Font Awesome Up Arrow Icon -->
    </button>

    <script>
        // Get the button
        let myBtn = document.querySelector('.back-to-top');

        // Show the button when the user scrolls down 20px
        window.onscroll = function() {scrollFunction()};

        function scrollFunction() {
            if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
                myBtn.style.display = "flex"; /* Show the button */
            } else {
                myBtn.style.display = "none"; /* Hide the button */
            }
        }

        // Scroll to the top when the button is clicked
        function topFunction() {
            document.body.scrollTop = 0;
            document.documentElement.scrollTop = 0;
        }
    </script>

</body>
</html>

As a 90s kid who grew up with MySpace and Piczo, being able to customise a website with HTML and CSS was somewhat natural to me. Learning how to do the same with this Jekyll site on GitHub was a bit more of a challenge, and I've certainly learned some things along the way.

<br>
<br>

If you're looking to create a static website for your portfolio or blogging, then look no further than GitHub pages. It's a fun experience!

<br>
<br>

You can enable HTTPS to secure your site, you can choose your own github-based domain for free (e.g. username.github.io), and if you own a custom domain name you can set up DNS to redirect any requests to your domain to your GitHub site.

<br>
<br>

There's lots of thorough guides on how to set up GitHub Pages with Jekyll, and they explain the process better than I could. 

<br>
<br>

I've included some of these resources below, so skip to the end if you're at a further stage. For the purposes of this post, I just want to share some other gems (pun intended) <a href="#ref1" id="back1" class="reference"> [1]</a>  of knowledge that you might not necessarily find on these technical 'step-by-step' guides.

<br>
<br>

<h2 id="Static Sites vs. Dynamic Sites" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Static Sites vs. Dynamic Sites</h2>

<br>

With GitHub Pages, you'll be creating a <strong>static</strong> website.

<br>
<br>

Static website = Everyone will 'see the exact same thing on each page'

<br>
<br>

Dynamic website = 'pulls content on the fly', content 'changes with the user'. <a href="#ref2" id="back2" class="reference"> [2]</a> 

<br>
<br>

e.g. a site that holds your CV (resume) vs. Amazon or a CMS system with a back-end database.

<br>
<br>

<h2 id="Limitations of GitHub Pages" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Limitations of GitHub Pages</h2>

<br>

<ul>
<li>You can't use it for commercial purposes.</li>
<br>
<li>Your entire GitHub Pages site repo can't be bigger than 1GB (this is quite generous, as you'd need an awful lot of images and text files to even come close to 1GB).</li><a href="#ref3" id="back3" class="reference"> [3]</a> 
</ul>

<br>

<h2 id="If you're a complete beginner, don't fret!" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">If you're a complete beginner, don't fret!</h2>

<br>

GitHub actually has a beginner guide that will walk you through the process of setting up your GitHub Pages site, and you can have your site up and running in less than an hour. It's actually what I did, and I don't think you should feel any shame in using it.

<br>
<br>

<a href="https://github.com/skills/github-pages">GitHub Pages Skills</a>

<br>
<br>

<h2 id="What is Jekyll?" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">What is Jekyll?</h2>

<br>

Jekyll is a static site generator with built-in support for GitHub Pages.

<br>
<br>

It simplifies website creation by automating tasks and applying pre-set styles, so you can focus on your content and not have to worry about HTML (perfect for beginners).

<br>
<br>
<a href="https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll">GitHub Pages and Jekyll</a>

<br>
<br>

<h2 id="Do I need to install Jekyll locally?" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">"Do I need to install Jekyll locally?"</h2>

<br>

In short, no. If you create your site using the <a href="https://github.com/skills/github-pages">GitHub Pages Skills</a> link, your site will be created using Jekyll (on GitHub), and you don't really need to learn how to use Jekyll.

<br>
<br>

Having said that, I would definitely recommend installing Jekyll locally with WSL2 (see below).

<br>
<br>

This is because it will allow you to auto-regenerate your site on your localhost when you make changes in real-time. Otherwise, you'll be waiting for your files to slowly upload live to your GitHub repo (containing your site) in order to see the changes you've made.

<br>
<br>

A local install of Jekyll means better version control by essentially having a 'dev' and 'prod' branch (local vs. on GitHub). Should you also wish to set up the Git CLI to commit to prod from the terminal, you can then do that seamlessly within WSL2.

<br>
<br>

In the image below, you can see that I have Jekyll installed locally via WSL2, this allows me to serve my website on my localhost (127.0.0.1:4000) and I can have the 'repo' of my site saved locally for easy access.

<br>
<br>

<img src="/assets/images/JekyllWSL2.png" alt="Jekyll on WSL2" style="max-width: 100%; height: auto;">

<br>
<br>

<h2 id="Windows Subsystem for Linux 2 (WSL2)" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Windows Subsystem for Linux 2 (WSL2)</h2>

<br>

Windows Subsystem for Linux (WSL) lets you install Linux and use Linux applications, utilities, and Bash command-line tools directly on Windows. It's also faster than a virtual machine or dual boot. 

<br>
<br>

For installing it, you should use this Microsoft Guide - <a href="https://learn.microsoft.com/en-us/windows/wsl/install">Microsoft Learn WSL</a>

<br>
<br>

<h2 id="Why do we need WSL2 to install Jekyll?" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">"So, why do we need WSL2 to install Jekyll?"</h2>

<br>

Jekyll is written using the Ruby programming language, and so we'll need to install both in order to use Jekyll locally. You won't actually need to learn how to use Ruby though, so don't worry.

<br>
<br>

My decision to use WSL2 for Jekyll was based off what I read online, as there are numerous discussions about how Ruby does not play nicely with Windows.

<br>
<br>

I also considered installing Jekyll and Ruby via a Docker container, as this sounded like a fun project. However, it's arguably overkill just for creating a static site.

<br>
<br>

For installing Jekyll, you should refer to this guide - <a href="https://jekyllrb.com/docs/installation/windows/">Jekyll Docs</a> (refer to "Installation via Bash on Windows 10" section)

<br>
<br>

<h2 id="Ok, so, how do we install Ruby?" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">"Ok, so, how do we install Ruby?"</h2>

<br>

Check out some of the useful links below for some of the guides I used. It seemed to me that people were using slightly different methods. 

<br>
<br>

For me, the easiest way of installing Ruby and Jekyll locally on WSL2 was actually to use the brew package manager for unix devices - <a href="https://brew.sh/">Homebrew Package Manager</a>

<br>
<br>

Bear in mind that it's normally recommended to add Ruby and Brew to your path environment variable after installation. This will allow you to execute commands from any directory, and prevents any possible issues with other dependencies.

<br>
<br>
<br>

<h2 id="USEFUL RESOURCES" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">USEFUL RESOURCES:</h2>

<br>
I recommend exploring these after you have set your site up.

<br>
<br>
<a href="https://ralphwillgoss.github.io/blog/2023/05/17/installalling-jekyll-windows-10-wsl2">https://ralphwillgoss.github.io/blog/2023/05/17/installalling-jekyll-windows-10-wsl2</a>

<br>
<br>

<a href="https://aregsar.com/blog/2019/how-to-customize-your-github-pages-blog-layout-in-five-minutes/">https://aregsar.com/blog/2019/how-to-customize-your-github-pages-blog-layout-in-five-minutes/</a>

<br>
<br>

<a href="https://davemateer.com/2020/10/20/running-jekyll-on-wsl2">https://davemateer.com/2020/10/20/running-jekyll-on-wsl2</a>

<br>
<br>

<a href="https://seankilleen.com/2020/07/building-my-jekyll-blog-with-ubuntu-on-wsl2/">https://seankilleen.com/2020/07/building-my-jekyll-blog-with-ubuntu-on-wsl2/</a>

<br>
<br>
<a href="https://simondosda.github.io/posts/2021-09-13-blog-github-pages-1-introduction.html">https://simondosda.github.io/posts/2021-09-13-blog-github-pages-1-introduction.html</a>

<br>
<br>

<h2 id="Additional Resources" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Additional Resources:</h2>

<br>

<strong><u>Choosing a different theme for your Jekyll site:</u></strong>

<br>
<br>

Lots of paid and free jekyll themes, here's a curated list of all the free ones - <a href="https://jekyllthemes.io/free">Jekyll Themes.io</a>

<br>
<br>

<strong><u>For adding comment sections:</u></strong>

<br>
<br>

<ul>
<li><a href="https://giscus.app/">giscus</a> (this is what I'm using, and I would recommend it over utterances for this <a href="#ref4" id="back4" class="reference"> [4]</a> reason)</li>
<br>
<li><a href="https://utteranc.es/ ">uterrances</a></li>
</ul>

<br>

<strong><u>Miscellaneous:</u></strong>

<br>
<br>

<a href="https://youtu.be/UKB9ylw0G4U?si=niGxrjxjZ3DEQoVf">Install Jekyll on Apple Silicon (Jamstack)</a>

<br>
<br>

It appears there may be publically available Docker images for Jekyll (I've not used this, so I can't vouch for it) - <a href="https://hub.docker.com/r/jekyll/jekyll/">Jekyll Docker Image</a>

<br>
<br>
<br>

<h2 id="Final thoughts" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Final thoughts / Things I wish I knew earlier:</h2>

<br>

I was initially quite confused as to which one of my site's files contained the code that said "your posts will be displayed on the index/main page". I could see the page code for it when I looked at the index page source, but there was no traces of it in the actual files of my site.

<br>
<br>

<ul>
<li> This is because if you don't specify a layout in your pages, Jekyll will use its own hidden "default" layout corresponding to your theme. If you want to override this layout, you should e.g. create a new layout called 'default.html' and store it inside a directory called '/_layouts' in your repo. You can then apply this layout by specifying 'layout: default' in each individual page. You can also have many layouts for certain pages of your site.</li>
</ul>
    
<br>

GitHub Pages supports Javascript, CSS and HTML. If you see some cool styling on a website you can always 'view page source' or 'inspect' -> 'style editor' to reverse engineer and borrow ideas for your site. There's also lots of cool resources online that give example styles etc. for you to use for free; just Google something like 'Top 10 CSS/HTML/Javascript for your static website'.

<br>
<br>
<br>

<div id="references">
    <h2>References</h2>
    <p id="ref1">A Gemfile in Jekyll describes the Ruby dependencies the website needs to run.<a href="#back1" class="back-to-ref"> [1]</a></p>
    <p id="ref2">
    <a href="https://www.wix.com/blog/static-vs-dynamic-website">https://www.wix.com/blog/static-vs-dynamic-website</a><a href="#back2" class="back-to-ref"> [2]</a></p>
    <p id="ref3">
    <a href="https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages">https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages</a><a href="#back3" class="back-to-ref"> [3]</a></p>
    <p id="ref4">
    <a href="https://shipit.dev/posts/from-utterances-to-giscus.html">https://shipit.dev/posts/from-utterances-to-giscus.html</a><a href="#back4" class="back-to-ref"> [4]</a></p>
</div>

<br>
<br>

<script src="https://giscus.app/client.js"
        data-repo="cicero343/cicero343.github.io"
        data-repo-id="R_kgDOMgKHgA"
        data-category="Announcements"
        data-category-id="DIC_kwDOMgKHgM4CiNr5"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="dark"
        data-lang="en"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
