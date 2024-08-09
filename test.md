---
title: test
permalink: /test/
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


<div id="chat"></div>

<script>
  // JavaScript code to handle real-time chat functionality
  var chat = document.getElementById('chat');

  function addMessage(message) {
    var p = document.createElement('p');
    p.textContent = message;
    chat.appendChild(p);
  }

  // WebSocket code to connect to the server and receive messages
  var socket = new WebSocket('ws://localhost:3000');

  socket.addEventListener('message', function(event) {
    addMessage(event.data);
  });

  // JavaScript code to send messages to the server
  var form = document.querySelector('form');
  var input = document.querySelector('input');

  form.addEventListener('submit', function(event) {
    event.preventDefault();
    var message = input.value;
    socket.send(message);
    input.value = '';
    addMessage('You: ' + message);
  });
</script>








<div class="drag-container">
  <div class="drag-item" draggable="true">Item 1</div>
  <div class="drag-item" draggable="true">Item 2</div>
  <div class="drag-item" draggable="true">Item 3</div>
</div>

<style>
  .drag-container {
    display: flex;
  }

  .drag-item {
    width: 100px;
    height: 100px;
    background-color: #f7b841;
    margin-right: 10px;
    cursor: grab;
  }

  .drag-item:active {
    cursor: grabbing;
  }
</style>

<script>
  // JavaScript code to handle drag-and-drop functionality
  var dragItems = document.querySelectorAll('.drag-item');

  dragItems.forEach(function(item) {
    item.addEventListener('dragstart', function(event) {
      event.dataTransfer.setData('text/plain', event.target.id);
    });
  });
</script>







 <button class="animateFromCenter">Click Me!</button>
    <button class="animateFromLeft">Click Me!</button>
    <button class="animateFromRight">Click Me!</button>
<style>
 *{
    user-select: none;
}
body{
    margin: 0;
    display:grid;
    place-items: center;
    grid-template-columns: 33% 33% 33%;
    height:100vh;
    background-color: rgb(27, 28, 30);
}
button{
    display: grid;
    
    padding:10px 20px;
    cursor:pointer;
    background-color: transparent;
    border:1px solid rgb(51, 51, 60);
    border-radius: 20px;
    color:white;
    overflow: hidden;
    font-family: monospace;
    font-size: 1.2rem;
    z-index: 1;
    font-weight: bold;
    position: relative;
}

button:hover{
    background-color: rgb(51, 51, 60);
}
button:after{
    content:'';
    place-self: center;
    width:0px;
    background-color: rgb(19, 18, 21);
    z-index: -1;
    height:0px;
    border-radius: 50%;
    position: absolute;
    transition: 0.3s;
}
button:active::after{
    width:200px;
    height:200px;
}



.animateFromRight::after{
    right:-200px;
    width:200px;
    height:200px;
}
.animateFromRight:active::after{
    right:0px;
}
.animateFromLeft::after{
    width:200px;
    height:200px;
    left:-200px;
}
.animateFromLeft:active::after{

    left:0px;
}
</style>








<div class="slider">
  <img src="image1.jpg">
  <img src="image2.jpg">
  <img src="image3.jpg">
</div>

<style>
  .slider {
    overflow: hidden;
    width: 500px;
    height: 300px;
  }

  .slider img {
    width: 100%;
    height: auto;
    opacity: 0;
    transition: opacity 0.5s ease-in-out;
  }

  .slider img.active {
    opacity: 1;
  }
</style>

<script>
  // JavaScript code to handle image slider navigation and animation
  var images = document.querySelectorAll('.slider img');
  var currentImage = 0;

  setInterval(function() {
    images[currentImage].classList.remove('active');
    currentImage = (currentImage + 1) % images.length;
    images[currentImage].classList.add('active');
  }, 2000);
</script>


