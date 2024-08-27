---
layout: default
---

<style>
  body {
    background-color: #f0f0f0; /* Fallback background color */
    background-image: linear-gradient(to bottom, #f0f0f0, #f0f0f0), linear-gradient(to bottom, #f0f0f0, #f0f0f0);
    background-position: left center, right center;
    background-repeat: no-repeat;
    background-size: 100vw 100vh;
    padding: 2rem 10%;
  }

  @media only screen and (max-width: 768px) {
    body {
      padding: 2rem 5%;
      background-size: 100vw 100vh;
    }
  }

  @media only screen and (max-width: 480px) {
    body {
      padding: 1rem 2%;
      background-size: 100vw 100vh;
    }
  }

  /* Ensure content area remains white */
  .main-content {
    background-color: white;
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  }
</style>

<div class="main-content">
  ## Your Markdown Content Here

  This is a test page with a custom background applied to the borders. The main content area remains white.

  More content here...
</div>
