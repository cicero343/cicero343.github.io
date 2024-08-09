---
title: About me
permalink: /test/
---

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
</head>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Text Example</title>
    <style>
        .copy-container {
            margin: 20px;
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
        <p id="text-to-copy">
            This is the text you want to copy. You can put any length of text here.
        </p>
        <button class="copy-button" onclick="copyText()">Copy Text</button>
    </div>

    <script>
        function copyText() {
            var text = document.getElementById('text-to-copy').innerText;
            navigator.clipboard.writeText(text).then(function() {
                alert('Text copied to clipboard!');
            }).catch(function(err) {
                console.error('Error copying text: ', err);
            });
        }
    </script>
</body>
</html>
