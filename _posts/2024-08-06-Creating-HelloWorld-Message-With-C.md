---
title: "Intro to C language: Creating a 'Hello World' Message (in WSL)"
date: 2024-08-07
---

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


Windows .dll (dynamic link library) files and UNIX-like .so files (or shared object files) were quite hard for me to wrap my head around as I'm not from a Comp Sci or Programmer background.

Essentially, .dll and .so files are 'shared libraries' which contain reusable code that can be dynamically loaded and used by other programs during runtime. You've probably seen them on Windows in some of these areas:

![Github post 1](https://github.com/user-attachments/assets/537e933a-dd85-4134-97b0-f7eff6300a0c)

<br>

I wanted to create a basic example to help me understand how they work, so here's a quick guide on **Creating a 'Hello World' Message with C in Windows Subsystem for Linux (WSL)**. My WSL was not playing nicely with X11 libraries, so this is going to be very basic.

<br>

**Step 1: Create a C file called 'message.c'**

    sudo nano message.c
    
<br>

    #include <stdio.h>

    void show_message(const char *message) {
    printf("%s\n", message);
    }

**Step 2: Compile the Shared Library**

    gcc -fPIC -shared -o libmessage.so message.c


**Step 3: Create a C file called 'callmessage.c'**

    sudo nano callmessage.c
    
<br>

    #include <stdio.h>
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
    }

**Step 4: Compile the 'callmessage' Program**

    gcc -o callmessage callmessage.c -ldl

**Step 5: Run the Executable**

    ./callmessage
    
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
