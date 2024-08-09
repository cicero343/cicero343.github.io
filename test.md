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
    <title>Side by Side Images</title>
    <style>
        .image-container {
            display: flex; /* Use flexbox to place items side by side */
            gap: 10px; /* Optional: Adds space between the items */
        }
        .profile-image {
            border-radius: 20px; /* Apply border radius to profile image */
        }
    </style>
</head>
<body>
    <div class="image-container">
        <img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="100" height="100" alt="Profile Image" class="profile-image">
        <div class="tryhackme-badge">
            <script src="https://tryhackme.com/badge/2125035"></script>
        </div>
    </div>
</body>
</html>
