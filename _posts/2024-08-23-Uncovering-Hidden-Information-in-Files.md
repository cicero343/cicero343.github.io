---
title: "Uncovering Hidden Information in Files: Tools for File Analysis, Steganography and more"
date: 2024-08-23
layout: default
---

<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">Uncovering Hidden Information in Files: Tools for File Analysis, Steganography and more</h1>
  <p class="post-meta">
    <time class="dt-published" datetime="2024-08-23T00:00:00+00:00" itemprop="datePublished">Aug 23, 2024</time>
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

There are various tools that one can use to find hidden information in files (e.g. a text document hidden within an image file). These can be invaluable in Digital Forensics and Incident Response (DFIR) scenarios.

<br>
<br>

My experience (thus far) is that quite a few of these tools are not that difficult to use, so I'll be outlining some of them in this post.

<br>
<br>

I'm by no means an expert in these areas; so, perhaps I will update this post as time goes on!
<br>
<br>

<h2 id="content" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Content</h2>
<ul>
    <li><a href="#file-analysis">File Analysis</a></li>
    <li><a href="#binary-analysis">Binary Analysis & Reverse Engineering</a></li>
    <li><a href="#debugging">Debugging Tools</a></li>
    <li><a href="#system-tracing">System Tracing & Monitoring</a></li>
    <li><a href="#steganography">Steganography</a></li>
    <li><a href="#notable-mentions">Notable Mentions: File Carving & Digital Forensics</a></li>
    <!-- Add more content items as needed -->
</ul>

<br>

<h2 id="file-analysis" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">File Analysis</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">file</h3>

The file command is used to determine the type of a file. This is particularly useful when you need to identify files with ambiguous or missing extensions.

<br>
<br>

<img src="/assets/images/file.png" alt="file command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">strings</h3>

The strings command can be used to extract any printable strings in the binary file. This can be useful to see some text data, function names, or other strings embedded in the binary.

<br>
<br>

<img src="/assets/images/strings.png" alt="strings command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">hexedit</h3>

hexedit is a hex editor that allows you to view and edit the raw binary data of files. It's useful for tasks like modifying file headers, performing manual patching, or inspecting binary content.

<br>
<br>

In the images below you can see that we've changed the hex code for this .png file and now the 'file' command thinks it's a PDF file!

<br>
<br>

<img src="/assets/images/hexedit 1.png" alt="hexedit command output" style="max-width: 100%; height: auto;">

<br>
<br>

<img src="/assets/images/hexedit 2.png" alt="hexedit command output" style="max-width: 100%; height: auto;">

<br>
<br>

<img src="/assets/images/hexedit 3.png" alt="hexedit command output" style="max-width: 100%; height: auto;">

<br>
<br>

<img src="/assets/images/hexedit 4.png" alt="hexedit command output" style="max-width: 100%; height: auto;">

<br>
<br>
<br>

<h2 id="binary-analysis" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Binary Analysis & Reverse Engineering</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">binwalk</h3>

binwalk is a tool for analysing binary files to detect embedded files, firmware, and other data. It’s commonly used in reverse engineering to extract data from binary files.

<br>
<br>

<img src="/assets/images/binwalk 1.png" alt="binwalk command output" style="max-width: 100%; height: auto;">
<img src="/assets/images/binwalk 2.png" alt="binwalk command output" style="max-width: 100%; height: auto;">

<br>
<br>

<img src="/assets/images/binwalk 3.png" alt="binwalk command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">readelf</h3>

The readelf command is a tool that displays information about ELF files. It can show you headers, sections, symbols, and more.

<br>
<br>

<img src="/assets/images/readelf.png" alt="readelf command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">radare2</h3>

radare2 is a powerful open-source framework for reverse engineering and analysing binaries. It includes a wide range of tools for disassembling, debugging, and decompilation.

<br>
<br>

<img src="/assets/images/radare2.png" alt="radare2 command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">Ghidra</h3>

Ghidra is a powerful reverse engineering tool developed by the NSA. It disassembles and decompiles binary code, allowing users to analyse programs for hidden functionality, malware, or vulnerabilities.

<br>
<br>

<img src="/assets/images/ghidra.png" alt="ghidra command output" style="max-width: 100%; height: auto;">

<br>
<br>
<br>

<h2 id="debugging" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Debugging Tools</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">GDB (GNU Debugger)</h3>

GDB is a debugger for programs written in languages like C, C++, and more compiled binaries. Allows for real-time inspection (interactive) and control over program execution in order to find bugs and hidden behaviour.

<br>
<br>

<img src="/assets/images/gdb.png" alt="gdb command output" style="max-width: 100%; height: auto;">

<br>
<br>
<br>

<h2 id="system-tracing" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">System Tracing & Monitoring</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">lsof (List Open Files)</h3>

lsof lists information about files opened by processes. This can be useful for tracking which files a program is using or analysing potential malware that might be interacting with the file system.

<br>
<br>

<img src="/assets/images/lsof.png" alt="lsof command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">ltrace</h3>

ltrace helps you track library function calls made by programs.

<br>
<br>

<img src="/assets/images/ltrace.png" alt="ltrace command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">strace</h3>

strace helps you monitor system calls and signals received by programs.

<br>
<br>

<img src="/assets/images/strace.png" alt="strace command output" style="max-width: 100%; height: auto;">

<br> 
<br>
<br>

<h2 id="steganography" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Steganography</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">exiftool</h3>

exiftool is a powerful tool used to read, write, and manipulate metadata in a wide variety of file formats, including images, videos, audio files, and documents. It’s commonly used to view or edit EXIF data in images, which includes details like camera settings, timestamps, and GPS coordinates.

<br>
<br>

<img src="/assets/images/exiftool.png" alt="exiftool command output" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">steghide</h3>

steghide is a steganography tool that allows you to embed (hide) and extract data within image or audio files. The tool supports various file formats and can also encrypt the embedded data. It’s often used in security and forensics to conceal or detect hidden information within multimedia files.

<br>
<br>

<img src="/assets/images/steghide.png" alt="steghide command output" style="max-width: 100%; height: auto;">

<br> 
<br>
<br>

<h2 id="notable-mentions" style="text-decoration: none; font-weight: bold; color: #00ff00; background-color: #000000; padding: 5px; border-radius: 5px;">Notable Mentions: File Carving & Digital Forensics</h2>
<a href="#content" class="back-to-content">Back to Content</a>

<br>
<br>

<h3 style="text-decoration: underline;">Foremost</h3>

foremost is a console program to recover files based on their headers, footers, and internal data structures. It can be used for extracting hidden files from disk images or memory dumps, where the file system might be corrupted or missing.

<br>
<br>

<img src="/assets/images/foremost.jpg" alt="foremost" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">Autopsy</h3>

Autopsy is a comprehensive digital forensics platform used to analyse hard drives, smartphones, and other data sources. It features file carving, metadata extraction, timeline analysis, keyword searching, and more. Investigators use it to recover deleted files, analyse disk images, and uncover hidden or obscured data.

<br>
<br>

<img src="/assets/images/autopsy.png" alt="autopsy" style="max-width: 100%; height: auto;">

<br>
<br>

<h3 style="text-decoration: underline;">EnCase</h3>

EnCase is a digital forensics tool primarily used for forensic investigation, data recovery, and analysis of digital devices and storage media.

<br>
<br>

<img src="/assets/images/encase.jpg" alt="encase" style="max-width: 100%; height: auto;">

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
