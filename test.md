---
title: test
permalink: /test/
---

<style>
  /* Apply background only to the body, but not to header or footer */
  body {
    background-color: #f0f0f0;
    padding: 0; /* Remove padding applied earlier */
  }

  /* Wrap content in a container to apply custom styles */
  .content-container {
    background-color: white;
    margin: 0 auto;
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    max-width: 90%; /* Ensures the content doesn't touch the edges */
  }

  /* Adjust the container width for different screen sizes */
  @media only screen and (max-width: 768px) {
    .content-container {
      max-width: 95%;
    }
  }

  @media only screen and (max-width: 480px) {
    .content-container {
      max-width: 98%;
    }
  }
</style>

<div class="content-container">
  ## Your Markdown Content Here

  This page now has a custom background applied to the borders, but the main content area remains white and centered within a container.

  Additional content...
</div>
