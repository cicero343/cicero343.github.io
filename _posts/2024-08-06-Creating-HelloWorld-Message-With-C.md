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
    <div class="terminal">#include &lt;stdio.h&gt;<br>#include &lt;dlfcn.h&gt;<br><br>int main() {<br>
        &nbsp;&nbsp;&nbsp;&nbsp;void *handle;<br>
        &nbsp;&nbsp;&nbsp;&nbsp;void (*show_message)(const char *);<br><br>

        &nbsp;&nbsp;&nbsp;&nbsp;handle = dlopen("./libmessage.so", RTLD_LAZY);<br>
        &nbsp;&nbsp;&nbsp;&nbsp;if (!handle) {<br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fprintf(stderr, "%s\n", dlerror());<br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return 1;<br>
        &nbsp;&nbsp;&nbsp;&nbsp;}<br><br>

        &nbsp;&nbsp;&nbsp;&nbsp;dlerror(); // Clear any existing error<br>
        &nbsp;&nbsp;&nbsp;&nbsp;show_message = (void (*)(const char *))dlsym(handle, "show_message");<br>
        &nbsp;&nbsp;&nbsp;&nbsp;if (dlerror() != NULL) {<br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fprintf(stderr, "%s\n", dlerror());<br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return 1;<br>
        &nbsp;&nbsp;&nbsp;&nbsp;}<br><br>

        &nbsp;&nbsp;&nbsp;&nbsp;show_message("Hello, World!");<br><br>

        &nbsp;&nbsp;&nbsp;&nbsp;dlclose(handle);<br>
        &nbsp;&nbsp;&nbsp;&nbsp;return 0;<br>
        }
    </div>
</body>
</html>


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
