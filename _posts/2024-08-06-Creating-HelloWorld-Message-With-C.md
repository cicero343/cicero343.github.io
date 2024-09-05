---
title: "Intro to C language: Creating a 'Hello World' Message (in WSL)"
date: 2024-08-07
layout: default
---

<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">Intro to C language: Creating a &#39;Hello World&#39; Message (in WSL)</h1>
  <p class="post-meta">
    <time class="dt-published" datetime="2024-08-07T00:00:00+00:00" itemprop="datePublished">Aug 7, 2024</time>
  </p>
</header>

<div class="post-content e-content" itemprop="articleBody">

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Intro to C Language</title>
    
    <!-- Add Font Awesome for the up arrow icon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
    <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
    <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
    <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />

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

        <style>
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre-wrap; /* Preserve whitespace and line breaks */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
            width: 100%; /* Make the terminal box full-width */
            box-sizing: border-box; /* Include padding in width calculation */
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

Windows .dll (dynamic link library) files and UNIX-like .so files (or shared object files) were quite hard for me to wrap my head around as I'm not from a Comp Sci or Programmer background.

<br>
<br>

Essentially, .dll and .so files are 'shared libraries' which contain reusable code that can be dynamically loaded and used by other programs during runtime. You've probably seen them on Windows in some of these areas:

<br>
<br>

<img src="/assets/images/dll examples.png" alt="dll examples" style="max-width: 100%; height: auto;">

<br>
<br>
<br>

I wanted to create a basic example to help me understand how they work, so here's a quick guide on <strong>Creating a 'Hello World' Message with C in Windows Subsystem for Linux (WSL)</strong>. My WSL was not playing nicely with X11 libraries, so this is going to be very basic.

<br>
<br>
<br>

<strong>Step 1: Create a C file called 'message.c'</strong>

<br>
<br>

<div class="terminal">sudo nano message.c</div>
    
<br>
<br>

<div class="terminal">#include &lt;stdio.h&gt;<br><br>void show_message(const char *message) {<br>printf("%s\n", message);<br>}</div>

<br>
<br>

<strong>Step 2: Compile the Shared Library</strong>

<br>
<br>

<div class="terminal">gcc -fPIC -shared -o libmessage.so message.c</div>

<br>
<br>

<strong>Step 3: Create a C file called 'callmessage.c'</strong>

<br>
<br>

<div class="terminal">sudo nano callmessage.c</div>

<br>
<br>

<div class="terminal">#include &lt;stdio.h&gt;<br>#include &lt;dlfcn.h&gt;<br><br>int main() {<br>void *handle;<br>void (*show_message)(const char *);<br><br>handle = dlopen("./libmessage.so", RTLD_LAZY);<br>if (!handle) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>dlerror(); // Clear any existing error<br>show_message = (void (*)(const char *))dlsym(handle, "show_message");<br>if (dlerror() != NULL) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>show_message("Hello, World!");<br><br>dlclose(handle);<br>return 0;<br>}</div>

<br>
<br>

<strong>Step 4: Compile the 'callmessage' Program</strong>

<br>
<br>

<div class="terminal">gcc -o callmessage callmessage.c -ldl</div>

<br>
<br>

<strong>Step 5: Run the Executable</strong>

<br>
<br>

<div class="terminal">./callmessage</div>
    
<br>
<br>

When you run ./callmessage, it will:

<br>
<br>

<ul>
<li>Load libmessage.so.</li>
<li>Look up the show_message function in the shared library.</li>
<li>Call the show_message function with the argument "Hello, World!".</li>
<li>Print "Hello, World!" to the terminal</li>
</ul>

<br>
  
<img src="/assets/images/helloworld compiled.png" alt="compiled program" style="max-width: 100%; height: auto;">

<br>
<br>

You'll see in the image above that both the .so file and the executable 'callmessage' file are identified as being ELF files (Executable and Linkable Format).

<br>
<br>

ELF format is used for both types of files in Unix-like systems, but the 'callmessage' file is a standalone program that can be run by the OS.
