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

**CDPA 1988, s. 17 - Infringement by Copying**

e.g. IBCOS Computers Ltd v Barclays Mercantile Highland Finance Ltd  (copying computer code).<a href="#ref6" id="back6" class="reference"> [6]</a>

Right-holder needs to prove defendant is not simply emulating the function of the program<a href="#ref7" id="back7" class="reference"> [7]</a>

Includes copies which are transient or are incidental to some other use of the work.<a href="#ref8" id="back8" class="reference"> [8]</a>

Person will infringe (absent a defence) where e.g. they store work (or other subject matter) on a USB.<a href="#ref9" id="back9" class="reference"> [9]</a>

**CDPA 1988, s. 20 - Infringement by Communication to the Public**

Infringing person(s) need to make infringing subject matter 'available to the public'.<a href="#ref10" id="back10" class="reference"> [10]</a>

Includes uploading material onto publicly accessible web.<a href="#ref11" id="back11" class="reference"> [11]</a>

Includes installing peer-to-peer software that allows third parties to access works from the installer’s computer.<a href="#ref12" id="back12" class="reference"> [12]</a>

Does not apply if work is already publicly available?<a href="#ref13" id="back13" class="reference"> [13]</a>

e.g. Ziggo case<a href="#ref14" id="back14" class="reference"> [14]</a>

Concerned notorious torrent site ‘The Pirate Bay’  

various acts of indexing and classifying of the torrent files made them readily accessible to users. 

Pirate Bay’s intervention amounted to infringement by communication.<a href="#ref15" id="back15" class="reference"> [15]</a>

**CDPA 1988, s. 28A - Making of temporary copies**

No copyright liability for making temporary copies if:

Copies are transient/incidental e.g. caching websites<a href="#ref16" id="back16" class="reference"> [16]</a>

Copies are ‘essential part of a technological process’, ‘no independent economic significance’<a href="#ref17" id="back17" class="reference"> [17]</a>

Doesn't include unauthorised streams<a href="#ref18" id="back18" class="reference"> [18]</a>

**CDPA 1988, s. 50A, 50B, 50BA, 50C - Exceptions/Defences**

Making a back-up copy<a href="#ref19" id="back19" class="reference"> [19]</a>

But not necessary to back-up a computer game.<a href="#ref20" id="back20" class="reference"> [20]</a>

Decompilation<a href="#ref21" id="back21" class="reference"> [21]</a>

In order to help producers in making systems which are compatible/interoperable<a href="#ref22" id="back22" class="reference"> [22]</a>

Not allowed to decompile for research or study<a href="#ref23" id="back23" class="reference"> [23]</a>

Not allowed if information already readily available<a href="#ref24" id="back24" class="reference"> [24]</a>

Not allowed if decompilation not confined to acts necessary to achieve the permitted objective<a href="#ref25" id="back25" class="reference"> [25]</a>

Not allowed if attempting to create a program that is substantially similar in its expression to the program decompiled, or to do any act restricted by copyright.<a href="#ref26" id="back26" class="reference"> [26]</a>

Observing, studying and testing of computer programs<a href="#ref27" id="back27" class="reference"> [27]</a>

Not if breach of license terms?<a href="#ref28" id="back28" class="reference"> [28]</a>
  
Other acts permitted to lawful users 

Copying/adapting necessary for lawful use<a href="#ref29" id="back29" class="reference"> [29]</a> e.g. necessary to correct program error.<a href="#ref30" id="back30" class="reference"> [30]</a>

**CDPA 1988, s. 56 - Transfers of copies of works in electronic form.**

Transfer is allowed (even if perpetual license instead of a sale), provided the seller destroys their own copy.<a href="#ref31" id="back31" class="reference"> [31]</a>

**CDPA 1988, s. 97A - Injunctions against service providers**

EMI Records Ltd v. British Sky Broadcasting Ltd<a href="#ref32" id="back32" class="reference"> [32]</a>

Website indexing BitTorrent files 
Operators ‘authorising’ infringements of the users 

Newzbin<a href="#ref33" id="back33" class="reference"> [33]</a>
Provider was indexing site (active involvement)<a href="#ref34" id="back34" class="reference"> [34]</a>
Newzbin enabled users to download infringing files uploaded by third parties.<a href="#ref35" id="back35" class="reference"> [35]</a>

Twentieth Century Fox v. Sky UK<a href="#ref36" id="back36" class="reference"> [36]</a>
Website which allowed peer-to-peer users to watch unauthorised streams of films. 

<br>

The idea that ISPs will only be found liable where they have active involvement is reflected in the Electronic Commerce (EC Directive) Regulations 2002<a href="#ref37" id="back37" class="reference"> [37]</a>
regs 17, 18, and 19 allow providers 3 actions where they will have immunity from copyright<a href="#ref38" id="back38" class="reference"> [38]</a>
‘mere conduits’, ‘caching’, and ‘hosting’
They also compel providers to act expeditiously to remove infringing content once they obtain knowledge of its existence<a href="#ref39" id="back39" class="reference"> [39]</a>

But immunity is forfeited if ISP plays an ‘active role' allowing it to be aware of the infringing material.<a href="#ref40" id="back40" class="reference"> [40]</a>

It is suggested that this immunity 'shields' cloud providers, such as Microsoft’s OneDrive, DropBox, and iCloud<a href="#ref41" id="back41" class="reference"> [41]</a>


<div id="references">
    <h2>References</h2>
    <p id="ref1">1. Bently, Sherman, Gangjee, & Johnson, Intellectual Property Law (5th edn, OUP, 2018), 44. <a href="#back1" class="back-to-ref">[1]</a></p>
    <p id="ref2">2. Ladbroke v William Hill [1964] 1 All ER 465; see also Infopaq case (2009)<a href="#back2" class="back-to-ref">[2]</a></p>
    <p id="ref3">3. Copyright, Designs and Patents Act (CDPA) 1988, s 16(3) <a href="#back3" class="back-to-ref">[3]</a></p>
    <p id="ref4">4. see also Trips, Art. 10(1); Software Dir., Art. 1; IBCOS Computers Ltd v Barclays Mercantile Highland Finance Ltd , [1994] FSR 275; Sega Enterprises v Richards [1983] FSR 73 <a href="#back4" class="back-to-ref">[4]</a></p>
    <p id="ref5">5. CDPA 1988, ss. 9(3), 12(7), 178<a href="#back5" class="back-to-ref">[5]</a></p>
    <p id="ref6">6. [1994] FSR 275<a href="#back6" class="back-to-ref">[6]</a></p>
    <p id="ref7">7. Navitaire Inc v easyJet Airline Company [2006] RPC 3; see also Nova Productions Ltd v Mazooma Games Ltd . [2007] RPC 25<a href="#back6" class="back-to-ref">[7]</a></p>
    <p id="ref8">8. CDPA 1988, s. 17(6) But note CDPA 1988, s. 28A (transient copies allowed if temporary copy). <a href="#back8" class="back-to-ref">[8]</a></p>
    <p id="ref9">9. Technische Universität Darnstadt v. Eugen Ulmer KG, Case C-117/13, EU:C:2014:2196, [37], [52] (ECJ).<a href="#back9" class="back-to-ref">[9]</a></p>
    <p id="ref10">10. CDPA 1988, s. 20(2)<a href="#back10" class="back-to-ref">[10]</a></p>
    <p id="ref11">11. Public Relations Consultants Association v. NLA, Case C-360/13, EU:C:2014:1195, [57].<a href="#back11" class="back-to-ref">[11]</a></p>
    <p id="ref12">12. Dramatico Entertainment v. British Sky Broadcasting [2012] EWHC 268 (Ch), [2012] RPC (27) 665, [69] (Arnold J).<a href="#back12" class="back-to-ref">[12]</a></p>
    <p id="ref13">13. GS Media BV v. Sanoma Media Netherlands BV et al., Case C-160/15, EU:C:2016:221 [AG54] (AG Wathelet), [48]; (hyperlinks leading to protected works that were freely accessible on another website); see also Svensson v. Retriever Sverige AB, Case C-466/12, EU:C:2014:76 (ECJ), [24]-[30].<a href="#back13" class="back-to-ref">[13]</a></p>
    <p id="ref14">14.  Stichting Brein v. Ziggo BV, Case C-610/15, EU:C:2017:456, [38], [45] (ECJ).<a href="#back14" class="back-to-ref">[14]</a></p>
    <p id="ref15">15. Ibid, [26]-[36], (ECJ); [AG50] (AG Szpunar); see also Stichting Brein v. Jack Frederik Wullems, Case C-527/15, EU:C:2017:300 (ECJ) (structured menu of hyperlinks on multimedia player helped users to access unauthorised streams.); EMI Records Ltd v. British Sky Broadcasting Ltd [2013] EWHC 379 (Ch), [45]-[46], [52]-[70].<a href="#back15" class="back-to-ref">[15]</a></p>
    <p id="ref16">16. Info. Soc. Dir., Recital 33; see also Bently, Sherman, Gangjee, & Johnson, Intellectual Property Law (5th edn, OUP, 2018), 236.<a href="#back16" class="back-to-ref">[16]</a></p>
    <p id="ref17">17. FAPL, Joined Cases C-403/08 and C-429/08 [2011] ECR I-9083 (ECJ, Grand Chamber), [175]-[177] (copies created in the buffer of a broadcast receiver); Newspaper Licensing Agency (NLA) v. Public Relations Consultants Association (PRCA) [2013] UKSC 18; see also Infopaq I, [2009] ECR I-6569; Infopaq International A/S v. Danske Dagblades Forening, Case C-302/10, EU:C:2012:16 (’Infopaq II’); FAPL, Joined Cases C-403/08 and C-429/08 [2011] ECR I-9083 (ECJ, Grand Chamber).<a href="#back17" class="back-to-ref">[17]</a></p>
    <p id="ref18">18. Stichting Brein v. Jack Frederik Wullems, Case C-527/15, EU:C:2017:300, [69]-[72] (ECJ) (multimedia device which produced transient and unlawful copies of stream)<a href="#back18" class="back-to-ref">[18]</a></p>
    <p id="ref19">19. CDPA 1988, ss 50A<a href="#back19" class="back-to-ref">[19]</a></p>
    <p id="ref20">20. Sony Computer Entertainment Inc. v. Owen [2002] EMLR (34) 742; EWHC 742 (defendant reverse engineered Japanese PS2 game to be compatible with region specific PS2).<a href="#back20" class="back-to-ref">[20]</a></p>
    <p id="ref21">21. CDPA 1988, ss 50B<a href="#back21" class="back-to-ref">[21]</a></p>
    <p id="ref22">22. CDPA 1988, s. 50B(2); see also Page 274 IP book; CDPA 1988, s. 81(2) also exempts computer programs from the right to integrity.<a href="#back22" class="back-to-ref">[22]</a></p>
    <p id="ref23">23. CDPA 1988, s. 29(4).<a href="#back23" class="back-to-ref">[23]</a></p>
    <p id="ref24">24. CDPA 1988, s. 50B(3)<a href="#back24" class="back-to-ref">[24]</a></p>    
    <p id="ref25">25. CDPA 1988, s. 50B(3)(b)<a href="#back25" class="back-to-ref">[25]</a></p>    
    <p id="ref26">26. CDPA 1988, s. 50B(3)(d)<a href="#back26" class="back-to-ref">[26]</a></p>   
    <p id="ref27">27. CDPA 1988, ss 50BA<a href="#back27" class="back-to-ref">[27]</a></p> 
    <p id="ref28">28. SAS Institute v. World Programming (WPL) [2010] EWHC 1829 (Ch), [290].<a href="#back28" class="back-to-ref">[28]</a></p>
    <p id="ref29">29. CDPA 1988, s 50C(1)<a href="#back29" class="back-to-ref">[29]</a></p> 
    <p id="ref30">30. CDPA 1988, s 50C(2)<a href="#back30" class="back-to-ref">[30]</a></p>
    <p id="ref31">31. UsedSoft GmbH v. Oracle, Case C-128/11, EU:C:2012:407, [78], [87]. See also CDPA 1988, s. 56(2)-(3) ‘any copy, adaptation or copy of an adaptation made by the purchaser which is not also transferred shall be treated as an infringing copy for all purposes after the transfer.’<a href="#back31" class="back-to-ref">[31]</a></p>
    <p id="ref32">32. [2013] EWHC 379 (Ch), [45]-[46], [52]-[70] <a href="#back32" class="back-to-ref">[32]</a></p> 
    <p id="ref33">33. Twentieth Century Fox Film v. Newzbin [2010] EWHC 608 (Ch), [46], [78], [102]. <a href="#back33" class="back-to-ref">[33]</a></p>
    <p id="ref34">34. For more discussion on what amounts to active involvement, see Football Association Premier League v. British Sky Broadcasting [2013] EWHC 2058 (Ch), [2013] ECDR (14) 377, [39]-[42]; for other cases involving s97A see Paramount Home Entertainment International v. British Sky Broadcasting [2014] EWHC 937 (Ch) (Viooz website).<a href="#back34" class="back-to-ref">[34]</a></p> 
    <p id="ref35">35. See also Metro-Goldwyn-Mayer Studios Inc v. Grokster, 545 US 913, 125 S. Ct. 2764 (2005); A & M Records, Inc. v. Napster, Inc 239 F.3d 1004 (Court of Appeals, 9th Circuit 2001)<a href="#back35" class="back-to-ref">[35]</a></p> 
    <p id="ref36">36. [2015] EWHC 1082 (Ch).<a href="#back36" class="back-to-ref">[36]</a></p> 
    <p id="ref37">37. e-Commerce Regs, SI 2002/2013.<a href="#back37" class="back-to-ref">[37]</a></p> 
    <p id="ref38">38. Ibid, regs. 17, 18, 19<a href="#back38" class="back-to-ref">[38]</a></p> 
    <p id="ref39">39. Ibid, regs. 18(b)(v), 19(ii)<a href="#back39" class="back-to-ref">[39]</a></p> 
    <p id="ref40">40. L’Oréal SA v. eBay International AG, Case C-324/09 [2011] ECR I-6011, EU:C:2011:474, [123] (ECJ, Grand Chamber).<a href="#back40" class="back-to-ref">[40]</a></p> 
    <p id="ref40">40. Bently, Sherman, Gangjee, & Johnson, Intellectual Property Law (5th edn, OUP, 2018), 1291. <a href="#back40" class="back-to-ref">[40]</a></p>    
  
</div>
