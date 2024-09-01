---
title: "Intro to C language: Creating a 'Hello World' Message (in WSL)"
date: 2024-08-07
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
    
<!-- Add Font Awesome for the up arrow icon -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">

<style>
    /* Ensure the header has enough space to avoid overlap with fixed elements */
    .header-container {
        margin-top: 60px; /* Adjust this value as needed */
    }

    /* Back to Top Button Styling */
    .back-to-top {
        position: fixed;
        bottom: 20px;
        right: 20px;
        background-color: var(--button-bg-light); /* Light mode background */
        color: var(--button-text-light); /* Light mode icon color */
        border: none;
        border-radius: 50%; /* Circular button */
        width: 50px;
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 24px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        transition: background-color 0.3s ease, box-shadow 0.3s ease;
        cursor: pointer;
        display: none; /* Initially hidden */
        z-index: 1000; /* Ensure it appears above other content */
    }

    .back-to-top:hover {
        background-color: var(--button-bg-hover-light);
        box-shadow: 0 6px 8px rgba(0, 0, 0, 0.5);
    }

    /* Dark mode overrides for the Back to Top button */
    [data-theme="dark"] .back-to-top {
        background-color: var(--button-bg-dark);
        color: var(--button-text-dark);
    }

    [data-theme="dark"] .back-to-top:hover {
        background-color: var(--button-bg-hover-dark);
    }

    /* Ensure the theme toggle button is positioned properly */
    #theme-toggle {
        position: absolute; /* Allows positioning within its container */
        top: 20px; /* Adjust the top value to move it down */
        left: 20px; /* Adjust the left value to move it right */
        background-color: var(--button-bg-light);
        color: var(--button-text-light);
        border: none;
        border-radius: 5px;
        padding: 10px 20px;
        cursor: pointer;
        z-index: 1000; /* Ensure it appears above other content */
    }

    #theme-toggle:hover {
        background-color: var(--button-bg-hover-light);
    }

    /* Dark mode overrides for the theme toggle button */
    [data-theme="dark"] #theme-toggle {
        background-color: var(--button-bg-dark);
        color: var(--button-text-dark);
    }

    [data-theme="dark"] #theme-toggle:hover {
        background-color: var(--button-bg-hover-dark);
    }
</style>

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

Windows .dll (dynamic link library) files and UNIX-like .so files (or shared object files) were quite hard for me to wrap my head around as I'm not from a Comp Sci or Programmer background.

Essentially, .dll and .so files are 'shared libraries' which contain reusable code that can be dynamically loaded and used by other programs during runtime. You've probably seen them on Windows in some of these areas:

![Github post 1](https://github.com/user-attachments/assets/537e933a-dd85-4134-97b0-f7eff6300a0c)

<br>

I wanted to create a basic example to help me understand how they work, so here's a quick guide on **Creating a 'Hello World' Message with C in Windows Subsystem for Linux (WSL)**. My WSL was not playing nicely with X11 libraries, so this is going to be very basic.

<br>

**Step 1: Create a C file called 'message.c'**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">sudo nano message.c</div>
</body>
</html>
    
<br>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">#include &lt;stdio.h&gt;<br><br>void show_message(const char *message) {<br>printf("%s\n", message);<br>}</div>
</body>
</html>

<br>

**Step 2: Compile the Shared Library**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">gcc -fPIC -shared -o libmessage.so message.c</div>
</body>
</html>

<br>

**Step 3: Create a C file called 'callmessage.c'**


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">sudo nano callmessage.c</div>
</body>
</html>

<br>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">#include &lt;stdio.h&gt;<br>#include &lt;dlfcn.h&gt;<br><br>int main() {<br>void *handle;<br>void (*show_message)(const char *);<br><br>handle = dlopen("./libmessage.so", RTLD_LAZY);<br>if (!handle) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>dlerror(); // Clear any existing error<br>show_message = (void (*)(const char *))dlsym(handle, "show_message");<br>if (dlerror() != NULL) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>show_message("Hello, World!");<br><br>dlclose(handle);<br>return 0;<br>}</div>
</body>
</html>

<br>

**Step 4: Compile the 'callmessage' Program**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">gcc -o callmessage callmessage.c -ldl</div>
</body>
</html>

<br>

**Step 5: Run the Executable**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Terminal-like Text Box</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
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
    <div class="terminal">./callmessage</div>
</body>
</html>
    
<br>

When you run ./callmessage, it will:

- Load libmessage.so.
<br>
- Look up the show_message function in the shared library.
<br>
- Call the show_message function with the argument "Hello, World!".
<br>
- Print "Hello, World!" to the terminal

<br>
  
![image](https://github.com/user-attachments/assets/cd927d40-a891-4d82-88a6-a0b72605d059)

You'll see in the image above that both the .so file and the executable 'callmessage' file are identified as being ELF files (Executable and Linkable Format).

<br>

ELF format is used for both types of files in Unix-like systems, but the 'callmessage' file is a standalone program that can be run by the OS.
