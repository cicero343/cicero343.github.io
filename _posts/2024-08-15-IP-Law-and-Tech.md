---
title: "IP Law and Tech (Interesting Cases / Cheat Sheet)"
date: 2024-08-15
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

“One of the constant themes in the history of British copyright law is that it has been influenced by foreign and international trends and developments”<a href="#ref1" id="back1" class="reference"> [1]</a> 

**Copyright**

There are many pre-stage tests one must do before asking whether copyright has been infringed. For example, one must first ask whether the subject matter in question is 'original' enough to be protected (the ‘skill, labour and judgement’ test).<a href="#ref2" id="back2" class="reference"> [2]</a> One must also ask if a 'substantial part' of the work has been copied to amount to infringement.<a href="#ref3" id="back3" class="reference"> [3]</a> For the sake of keeping this blog post as short and sweet as possible. We will be glossing over these details to focus on the cases and juicy bits. 

**CDPA 1988, s. 3(1)(b)**

Computer programs protected as literary works<a href="#ref4" id="back4" class="reference"> [4]</a>

Even computer-generated works could be protected<a href="#ref5" id="back5" class="reference"> [5]</a>

**CDPA 1988, s. 17 - Infringement by Literal Copying**

e.g. IBCOS Computers Ltd v Barclays Mercantile Highland Finance Ltd  (copying computer code).<a href="#ref6" id="back6" class="reference"> [6]</a>

Right-holder needs to prove defendant is not simply emulating the function of the program<a href="#ref7" id="back7" class="reference"> [7]</a>

Includes copies which are transient or are incidental to some other use of the work.<a href="#ref8" id="back8" class="reference"> [8]</a>

Person will infringe (absent a defence) where e.g. they store work (or other subject matter) on a USB.<a href="#ref9" id="back9" class="reference"> [9]</a>


<div id="references">
    <h2>References</h2>
    <p id="ref1">1. Bently, Sherman, Gangjee, & Johnson, Intellectual Property Law (5th edn, OUP, 2018), 44.  <a href="#back1" class="back-to-ref">[1]</a></p>
    <p id="ref2">2. Ladbroke v William Hill [1964] 1 All ER 465; see also Infopaq case (2009)<a href="#back2" class="back-to-ref">[2]</a></p>
    <p id="ref3">3. Copyright, Designs and Patents Act (CDPA) 1988, s 16(3) <a href="#back3" class="back-to-ref">[3]</a></p>
    <p id="ref4">4. see also Trips, Art. 10(1); Software Dir., Art. 1; IBCOS Computers Ltd v Barclays Mercantile Highland Finance Ltd , [1994] FSR 275; Sega Enterprises v Richards [1983] FSR 73 <a href="#back4" class="back-to-ref">[4]</a></p>
    <p id="ref5">5. CDPA 1988, ss. 9(3), 12(7), 178<a href="#back5" class="back-to-ref">[5]</a></p>
    <p id="ref6">6. [1994] FSR 275<a href="#back6" class="back-to-ref">[6]</a></p>
    <p id="ref7">7. Navitaire Inc v easyJet Airline Company [2006] RPC 3; see also Nova Productions Ltd v Mazooma Games Ltd . [2007] RPC 25<a href="#back6" class="back-to-ref">[7]</a></p>
    <p id="ref8">8. CDPA 1988, s. 17(6) But note CDPA 1988, s. 28A (transient copies allowed if temporary copy). <a href="#back8" class="back-to-ref">[8]</a></p>
    <p id="ref9">9. Technische Universität Darnstadt v. Eugen Ulmer KG, Case C-117/13, EU:C:2014:2196, [37], [52] (ECJ).<a href="#back9" class="back-to-ref">[9]</a></p>
</div>
