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
    <title>Terminal-like Text Box with Copy Function</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }

        .terminal-container {
            position: relative; /* For positioning the copy button */
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

        /* Copy button styling */
        .copy-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: #333; /* Dark background */
            color: #fff; /* White text */
            border: none;
            padding: 5px 10px;
            font-size: 12px;
            border-radius: 5px;
            cursor: pointer;
        }

        .copy-button:hover {
            background-color: #555; /* Lighter background on hover */
        }
    </style>
</head>
<body>

    <div class="terminal-container">
        <div class="terminal" id="code-block">gcc -fPIC -shared -o libmessage.so message.c</div>
        <button class="copy-button">Copy</button>
    </div>

    <script>
        // JavaScript for copying the code
        document.querySelector(".copy-button").addEventListener("click", function() {
            // Get the text from the terminal block
            const codeText = document.getElementById("code-block").innerText.trim();

            // Copy the text to clipboard
            navigator.clipboard.writeText(codeText).then(function() {
                // Change button text to "Copied!" after successful copy
                const button = document.querySelector(".copy-button");
                button.innerText = "Copied!";
                
                // Revert button text after 2 seconds
                setTimeout(function() {
                    button.innerText = "Copy";
                }, 2000);
            }, function(err) {
                console.error('Failed to copy text: ', err);
            });
        });
    </script>

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
    <title>Terminal-like Text Box with Copy Function</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }

        .terminal-container {
            position: relative; /* For positioning the copy button */
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

        /* Copy button styling */
        .copy-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: #333; /* Dark background */
            color: #fff; /* White text */
            border: none;
            padding: 5px 10px;
            font-size: 12px;
            border-radius: 5px;
            cursor: pointer;
        }

        .copy-button:hover {
            background-color: #555; /* Lighter background on hover */
        }
    </style>
</head>
<body>

    <div class="terminal-container">
        <div class="terminal" id="code-block">
            #include &lt;stdio.h&gt;<br>#include &lt;dlfcn.h&gt;<br><br>int main() {<br>
            void *handle;<br>void (*show_message)(const char *);<br><br>handle = dlopen("./libmessage.so", RTLD_LAZY);<br>
            if (!handle) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>dlerror(); 
            // Clear any existing error<br>show_message = (void (*)(const char *))dlsym(handle, "show_message");<br>
            if (dlerror() != NULL) {<br>    fprintf(stderr, "%s\n", dlerror());<br>    return 1;<br>}<br><br>
            show_message("Hello, World!");<br><br>dlclose(handle);<br>return 0;<br>}
        </div>
        <button class="copy-button">Copy</button>
    </div>

    <script>
        // Function to decode HTML entities
        function decodeHTMLEntities(text) {
            const tempElement = document.createElement('textarea');
            tempElement.innerHTML = text;
            return tempElement.value;
        }

        // JavaScript for copying the code
        document.querySelector(".copy-button").addEventListener("click", function() {
            // Get the raw HTML content from the terminal block
            const codeHTML = document.getElementById("code-block").innerHTML;

            // Decode the HTML entities to get the correct symbols like < and >
            const codeText = decodeHTMLEntities(codeHTML.replace(/<br>/g, '\n')).trim();

            // Copy the decoded text to clipboard
            navigator.clipboard.writeText(codeText).then(function() {
                // Change button text to "Copied!" after successful copy
                const button = document.querySelector(".copy-button");
                button.innerText = "Copied!";
                
                // Revert button text after 2 seconds
                setTimeout(function() {
                    button.innerText = "Copy";
                }, 2000);
            }, function(err) {
                console.error('Failed to copy text: ', err);
            });
        });
    </script>

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
