---
Title: A Diary of IT Projects
---
<img src="https://avatars.githubusercontent.com/u/175522457?v=4" width="125" height="125" style="border-radius: 20px;">

<div class="container">
	<div class="avatar">
		<a href="https://codepen.io/MarioDesigns/">
			<img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/751678/skytsunami.png" alt="Skytsunami" />
		</a>
	</div>
	<div class="content">
		<h1>Floating CSS animation</h1>
		<p>Follow me on:</p>
		<p>
			<span><a href="https://twitter.com/MDesignsuk" target="_blank"><i class="fa fa-twitter"></i></a></span>
			<span><a href="https://github.com/Mario-Duarte/" target="_blank"><i class="fa fa-github"></i></a></span>
			<span><a href="https://bitbucket.org/Mario_Duarte/" target="_blank"><i class="fa fa-bitbucket"></i></a></span>
			<span><a href="https://codepen.io/MarioDesigns/" target="_blank"><i class="fa fa-codepen"></i></a></span>
		</p>
		<p>BY: Mario Duarte</p>
	</div>
</div>

<a class="suppoprt-me" href="https://www.buymeacoffee.com/marioduarte" target="_blank"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a Coffee&nbsp&emoji=&slug=marioduarte&button_colour=FF5F5F&font_colour=ffffff&font_family=Cookie&outline_colour=000000&coffee_colour=FFDD00"></a>





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
