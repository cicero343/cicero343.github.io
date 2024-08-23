---
title: "Uncovering Hidden Information in Files: Tools for File Analysis and Steganography"
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

I'm by no means an expert in steganography, reverse engineering or file analysis. With that in mind, perhaps I will update this post as time goes on.

There are, however, various tools that one can use to find hidden information in files (e.g. a text document hidden within an image file).

My experience thus far is that quite a few of these tools are not that difficult to use, so I'll be outlining some of them in this post.

<h2>File Analysis, Reverse Engineering and Debugging</h2>

These tools can help you inspect files, binaries, or executables for hidden or unexpected information.

<h4>file</h4>

The file command is used to determine the type of a file. It analyses the file's contents and provides a description, such as whether it's a text file, an image, a compiled binary, or something else. This is particularly useful when you need to identify files with ambiguous or missing extensions.

![image](https://github.com/user-attachments/assets/a60d2b1e-b275-49f5-9765-e0a927624842)

<h4>strings</h4>

The strings command can be used to extract any printable strings in the binary file. This can be useful to see some text data, function names, or other strings embedded in the binary.

![image](https://github.com/user-attachments/assets/19907020-c129-4206-a903-7241da04d4b7)

<h4>binwalk</h4>

binwalk is a tool for analysing binary files to detect embedded files, firmware, and other data. It’s commonly used in reverse engineering to extract data from binary files.

![image](https://github.com/user-attachments/assets/5d734045-c42f-41b7-874a-5e9177d0da4b)
![image](https://github.com/user-attachments/assets/74eef571-0019-4b3a-815e-e65b459e22b9)
![image](https://github.com/user-attachments/assets/237e3a08-d9ad-4066-9cbd-b4efdd0a0763)

<h4>hexedit</h4>

hexedit is a hex editor that allows you to view and edit the raw binary data of files. It represents the data in both hexadecimal and ASCII formats, making it possible to manipulate the file at a low level. This tool is useful for tasks like modifying file headers, performing manual patching, or inspecting binary content.

In the images below you can see that we've changed the hex code for this .png file and now the 'file' command thinks it's a PDF file!

![image](https://github.com/user-attachments/assets/1ada6594-4bdd-4cb3-9366-30a43550d87b)
![image](https://github.com/user-attachments/assets/1e78381b-eb99-4ae7-a063-99695615c841)
![image](https://github.com/user-attachments/assets/ee2cbb68-8fea-4ee2-9b4d-fbddfbc03d09)

<h4>readelf</h4>

The readelf command is a tool that displays information about ELF files. It can show you headers, sections, symbols, and more.

![image](https://github.com/user-attachments/assets/d2b25b6a-4907-40f3-9a55-58c102350796)

<h4>ltrace</h4>

ltrace helps you track library function calls made to dynamically linked (shared) libraries.

![image](https://github.com/user-attachments/assets/6f2bc672-b743-4aab-a98b-55aaa988182c)

<h4>strace</h4>

strace helps you monitor system calls made by a program with the kernel. This can help you understand how a program interacts with the operating system.

![word-image-261](https://github.com/user-attachments/assets/4cbf1932-1fce-4e96-b902-41505ec2ffce)

<h4>radare2</h4>

radare2 is a powerful open-source framework for reverse engineering and analysing binaries. It includes a wide range of tools for disassembling, debugging, and analysing binary files.

<br> 

<h2>Steganography</h2>

<h4>exiftool</h4>

exiftool is a powerful tool used to read, write, and manipulate metadata in a wide variety of file formats, including images, videos, audio files, and documents. It’s commonly used to view or edit EXIF data in images, which includes details like camera settings, timestamps, and GPS coordinates.

![image](https://github.com/user-attachments/assets/9f9bab9b-f073-4db6-9c4b-190ef2f0b65c)

<h4>steghide</h4>

steghide is a steganography tool that allows you to embed (hide) and extract data within image or audio files. The tool supports various file formats and can also encrypt the embedded data. It’s often used in security and forensics to conceal or detect hidden information within multimedia files.

![image](https://github.com/user-attachments/assets/6929e938-4251-4b8f-8963-799f3e4e17a4)
