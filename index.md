---
title: A Diary of IT Projects
layout: home
---

<style>
  /* Dark mode link colors specific to this page */
  [data-theme="dark"] .link-list a {
    color: var(--link-color-dark);
  }
  
  [data-theme="dark"] .link-list a:hover {
    color: var(--link-hover-color-dark);
  }
  
  /* Ensuring that the layout stays consistent */
  .container {
    display: flex; /* Use flexbox to place items side by side */
    gap: 10px; /* Adds space between the items */
    align-items: flex-start; /* Align items at the top */
  }
  
  .profile-image {
    border-radius: 20px; /* Apply border radius to profile image */
  }
  
  .badge-links {
    display: flex;
    flex-direction: column; /* Arrange badge and links vertically */
    gap: 10px; /* Adds space between the badge and the links */
  }
  
  .link-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex; /* Arrange links horizontally */
    gap: 20px; /* Adds space between each link */
  }
  
  .link-list a {
    text-decoration: none;
    color: var(--link-color-light); /* Use variable for link color */
  }
  
  .link-list a:hover {
    text-decoration: underline;
    color: var(--link-hover-color-light); /* Use variable for hover color */
  }
</style>

<div class="container">
  <img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="100" height="100" alt="Profile Image" class="profile-image">
  <div class="badge-links">
    <div class="tryhackme-badge">
      <script src="https://tryhackme.com/badge/2125035"></script>
    </div>
    <ul class="link-list">
      <li><a href="https://www.linkedin.com/in/benedict-c-donovan/" target="_blank">LinkedIn</a></li>
      <li><a href="https://github.com/cicero343" target="_blank">GitHub</a></li>
      <li><a href="https://tryhackme.com/p/cicero343" target="_blank">TryHackMe</a></li>
    </ul>
  </div>
</div>
