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

  Below is a list of upcoming UK bank holidays fetched dynamically from the GOV.UK API:

  <div id="bank-holidays-container">
    <!-- Bank holidays will be loaded here -->
  </div>
</div>

<script>
  // Fetch the JSON data from the API
  fetch('https://www.gov.uk/bank-holidays.json')
    .then(response => response.json())
    .then(data => {
      const container = document.getElementById('bank-holidays-container');

      // Get the England and Wales bank holidays (modify as needed for Scotland or Northern Ireland)
      const holidays = data['england-and-wales'].events;

      // Create an unordered list to display the holidays
      const ul = document.createElement('ul');

      holidays.forEach(holiday => {
        const li = document.createElement('li');
        li.textContent = `${holiday.title} - ${new Date(holiday.date).toDateString()}`;
        ul.appendChild(li);
      });

      // Append the list to the container
      container.appendChild(ul);
    })
    .catch(error => {
      console.error('Error fetching the bank holidays:', error);
    });
</script>
