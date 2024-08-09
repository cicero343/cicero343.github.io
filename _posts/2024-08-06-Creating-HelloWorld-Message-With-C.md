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
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">sudo nano message.c</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
</body>
</html>
    
<br>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <pre class="terminal" id="text-to-copy">#include &lt;stdio.h&gt;

void show_message(const char *message) {
    printf("%s\n", message);
}</pre>
        <button class="copy-button" onclick="copyText()">Copy Text</button>
    </div>

    <script>
        function copyText() {
            var textBox = document.getElementById('text-to-copy');
            
            // Create a temporary textarea to hold the text
            var tempTextArea = document.createElement('textarea');
            tempTextArea.value = textBox.textContent; // Use textContent to get the actual text
            document.body.appendChild(tempTextArea);
            tempTextArea.select();
            
            // Copy the text to clipboard
            navigator.clipboard.writeText(tempTextArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });

            // Clean up
            document.body.removeChild(tempTextArea);
        }
    </script>
</body>
</html>

<br>

**Step 2: Compile the Shared Library**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">gcc -fPIC -shared -o libmessage.so message.c</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <div class="copy-container">
        <div class="terminal" data-copy-text="ls -la">ls -la</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
</body>
</html>

**Step 3: Create a C file called 'callmessage.c'**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">sudo nano callmessage.c</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <div class="copy-container">
        <div class="terminal" data-copy-text="ls -la">ls -la</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
</body>
</html>

<br>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">#include <stdio.h>
#include <dlfcn.h>

int main() {
void *handle;
void (*show_message)(const char *);

handle = dlopen("./libmessage.so", RTLD_LAZY);
if (!handle) {
    fprintf(stderr, "%s\n", dlerror());
    return 1;
}

dlerror(); // Clear any existing error
show_message = (void (*)(const char *))dlsym(handle, "show_message");
if (dlerror() != NULL) {
    fprintf(stderr, "%s\n", dlerror());
    return 1;
}

show_message("Hello, World!");

dlclose(handle);
return 0;
}</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <div class="copy-container">
        <div class="terminal" data-copy-text="ls -la">ls -la</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
</body>
</html>


**Step 4: Compile the 'callmessage' Program**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">gcc -o callmessage callmessage.c -ldl</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <div class="copy-container">
        <div class="terminal" data-copy-text="ls -la">ls -la</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
</body>
</html>

**Step 5: Run the Executable**

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .copy-container {
            margin: 20px;
        }
        .terminal {
            background-color: #000; /* Black background for terminal look */
            color: #0f0; /* Green text color */
            padding: 10px;
            border-radius: 5px;
            font-family: monospace; /* Terminal-like font */
            white-space: pre; /* Preserve whitespace without extra spaces */
            overflow: auto; /* Scroll if the content is too large */
            display: inline-block; /* Make the terminal block inline to avoid extra margins */
        }
        .copy-button {
            margin-top: 10px;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .copy-button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="copy-container">
        <div class="terminal" data-copy-text="sudo nano message.c">./callmessage</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <div class="copy-container">
        <div class="terminal" data-copy-text="ls -la">ls -la</div>
        <button class="copy-button" onclick="copyText(this)">Copy Text</button>
    </div>

    <script>
        function copyText(button) {
            // Find the closest .terminal element to the clicked button
            var textBox = button.previousElementSibling;
            var text = textBox.getAttribute('data-copy-text');

            // Create a temporary textarea to copy the text
            var textArea = document.createElement('textarea');
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            navigator.clipboard.writeText(textArea.value)
                .then(() => {
                    alert('Text copied to clipboard!');
                })
                .catch(err => {
                    console.error('Error copying text: ', err);
                });
            document.body.removeChild(textArea);
        }
    </script>
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
