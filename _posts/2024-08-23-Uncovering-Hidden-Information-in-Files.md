---
title: "Uncovering Hidden Information in Files: Tools for File Analysis, Steganography and more"
date: 2024-08-23
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
        /* No link color is specified here, allowing default browser color */
        --link-hover-color: darkblue; /* Darker blue on hover in light mode */
    }

    /* Dark mode settings */
    [data-theme="dark"] {
        --bg-color: #000000;
        --txt-color: #ffffff;
        --link-color: #00ff00; /* Green links in dark mode */
        --link-hover-color: #00cc00; /* Slightly darker green on hover in dark mode */
    }

    /* Apply the variables to the body */
    body {
        background-color: var(--bg-color);
        color: var(--txt-color);
    }

    /* Link styling */
    a:link, a:visited {
        /* Default to browser's default link color */
        color: inherit; /* Inherit the text color */
    }

    a:hover {
        color: var(--link-hover-color); /* Hover color based on light mode setting */
    }

    /* Dark mode link styling */
    [data-theme="dark"] a:link, [data-theme="dark"] a:visited {
        color: var(--link-color); /* Green links in dark mode */
    }

    [data-theme="dark"] a:hover {
        color: var(--link-hover-color); /* Darker green on hover in dark mode */
    }

    a:active {
        /* Maintain inherited color when clicked */
        color: inherit;
    }

    /* Dark mode active link styling */
    [data-theme="dark"] a:active {
        color: var(--link-color); /* Maintain green when clicked in dark mode */
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

There are various tools that one can use to find hidden information in files (e.g. a text document hidden within an image file). These can be invaluable in Digital Forensics and Incident Response (DFIR) scenarios.

My experience (thus far) is that quite a few of these tools are not that difficult to use, so I'll be outlining some of them in this post.

I'm by no means an expert in these areas; so, perhaps I will update this post as time goes on!

<h2 id="content" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Content</h2>
<ul>
    <li><a href="#file-analysis">File Analysis</a></li>
    <li><a href="#binary-analysis">Binary Analysis & Reverse Engineering</a></li>
    <li><a href="#debugging">Debugging Tools</a></li>
    <li><a href="#system-tracing">System Tracing & Monitoring</a></li>
    <li><a href="#steganography">Steganography</a></li>
    <li><a href="#notable-mentions">Notable Mentions: File Carving & Digital Forensics</a></li>
    <!-- Add more glossary items as needed -->
</ul>

<br>

<h2 id="file-analysis" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">File Analysis</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">file</h3>

The file command is used to determine the type of a file. This is particularly useful when you need to identify files with ambiguous or missing extensions.

![image](https://github.com/user-attachments/assets/480df8d5-b27d-4d87-a3bb-ea4684ad2725)

<h3 style="text-decoration: underline;">strings</h3>

The strings command can be used to extract any printable strings in the binary file. This can be useful to see some text data, function names, or other strings embedded in the binary.

![image](https://github.com/user-attachments/assets/afc4e48f-2a2f-4b5d-9027-a7ce874119a2)

<h3 style="text-decoration: underline;">hexedit</h3>

hexedit is a hex editor that allows you to view and edit the raw binary data of files. It's useful for tasks like modifying file headers, performing manual patching, or inspecting binary content.

In the images below you can see that we've changed the hex code for this .png file and now the 'file' command thinks it's a PDF file!

![image](https://github.com/user-attachments/assets/261b0db5-a762-4da9-8565-7eaf811e2e2b)

![image](https://github.com/user-attachments/assets/4d60744a-4140-4b12-918f-8a136d3da94e)

![image](https://github.com/user-attachments/assets/1e78381b-eb99-4ae7-a063-99695615c841)

![image](https://github.com/user-attachments/assets/e89134eb-6c90-4057-b2a3-7c400904e7bc)

<br>

<h2 id="binary-analysis" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Binary Analysis & Reverse Engineering</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">binwalk</h3>

binwalk is a tool for analysing binary files to detect embedded files, firmware, and other data. It’s commonly used in reverse engineering to extract data from binary files.

![image](https://github.com/user-attachments/assets/c45f830e-11b9-4ade-850d-fc2a8cf36143)
![image](https://github.com/user-attachments/assets/ff52f6f7-c9a7-4a2c-bb86-b64fac13ef26)

![image](https://github.com/user-attachments/assets/509ae5f3-2e50-4f05-9fea-1485ca9bebdb)


<h3 style="text-decoration: underline;">readelf</h3>

The readelf command is a tool that displays information about ELF files. It can show you headers, sections, symbols, and more.

![image](https://github.com/user-attachments/assets/22819f69-dda2-46b8-9838-d9c53b197fef)

<h3 style="text-decoration: underline;">radare2</h3>

radare2 is a powerful open-source framework for reverse engineering and analysing binaries. It includes a wide range of tools for disassembling, debugging, and decompilation.

![1_325iRMMQV2gupfGta-J7bQ](https://github.com/user-attachments/assets/0c2687a2-1cd2-404e-91a8-e6775c99f21a)

<h3 style="text-decoration: underline;">Ghidra</h3>

Ghidra is a powerful reverse engineering tool developed by the NSA. It disassembles and decompiles binary code, allowing users to analyse programs for hidden functionality, malware, or vulnerabilities.

![215551674-d6f156e0-bb5e-4e7d-867b-4fd4354240e8](https://github.com/user-attachments/assets/9592514c-5d44-49f8-b4ae-c81a33666da2)

<br>

<h2 id="debugging" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Debugging Tools</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">GDB (GNU Debugger)</h3>

GDB is a debugger for programs written in languages like C, C++, and more compiled binaries. Allows for real-time inspection (interactive) and control over program execution in order to find bugs and hidden behaviour.

![list-1](https://github.com/user-attachments/assets/44ddcc32-286e-41bb-8b06-dba5e3d192c2)

<br>

<h2 id="system-tracing" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">System Tracing & Monitoring</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">lsof (List Open Files)</h3>

lsof lists information about files opened by processes. This can be useful for tracking which files a program is using or analysing potential malware that might be interacting with the file system.

![image](https://github.com/user-attachments/assets/70414805-bed7-4d3b-93aa-599be459153b)

<h3 style="text-decoration: underline;">ltrace</h3>

ltrace helps you track library function calls made by programs.

![image](https://github.com/user-attachments/assets/8c5ca7fc-9877-48a1-a72c-e18bfa4c0b43)

<h3 style="text-decoration: underline;">strace</h3>

strace helps you monitor system calls and signals received by programs.

![word-image-261](https://github.com/user-attachments/assets/4cbf1932-1fce-4e96-b902-41505ec2ffce)

<br> 


<h2 id="steganography" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Steganography</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">exiftool</h3>

exiftool is a powerful tool used to read, write, and manipulate metadata in a wide variety of file formats, including images, videos, audio files, and documents. It’s commonly used to view or edit EXIF data in images, which includes details like camera settings, timestamps, and GPS coordinates.

![image](https://github.com/user-attachments/assets/b94fe8c5-53e6-45a6-8e3d-7b7de2c337af)

<h3 style="text-decoration: underline;">steghide</h3>

steghide is a steganography tool that allows you to embed (hide) and extract data within image or audio files. The tool supports various file formats and can also encrypt the embedded data. It’s often used in security and forensics to conceal or detect hidden information within multimedia files.

![image](https://github.com/user-attachments/assets/6f9bdc3b-5068-4332-9158-edb199929f26)

<br> 

<h2 id="notable-mentions" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Notable Mentions: File Carving & Digital Forensics</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<h3 style="text-decoration: underline;">Foremost</h3>

foremost is a console program to recover files based on their headers, footers, and internal data structures. It can be used for extracting hidden files from disk images or memory dumps, where the file system might be corrupted or missing.

![index 19](https://github.com/user-attachments/assets/b1ee69fd-b8cd-49f2-8d76-1f01f81f0c04)

<h3 style="text-decoration: underline;">Autopsy</h3>

Autopsy is a comprehensive digital forensics platform used to analyse hard drives, smartphones, and other data sources. It features file carving, metadata extraction, timeline analysis, keyword searching, and more. Investigators use it to recover deleted files, analyse disk images, and uncover hidden or obscured data.

![overview](https://github.com/user-attachments/assets/040edcb2-0903-4198-887f-14ac9af1666c)

<h3 style="text-decoration: underline;">EnCase</h3>

EnCase is a digital forensics tool primarily used for forensic investigation, data recovery, and analysis of digital devices and storage media.

![1271757361_encase](https://github.com/user-attachments/assets/50919e3a-374f-4b60-acbc-21698d4a44d0)
