---
title: Guest
permalink: /guest/
layout: default
---

<style>
  :root {
    --r: #f2a7bb;
    --p: #f7cba8;
    --l: #c9b8f0;
    --m: #a8e6cf;
    --c: #fdf6ee;
    --t: #4a3f5c;
  }

  .purge-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 3rem 1rem;
    min-height: 60vh;
    position: relative;
  }

  .purge-card {
    position: relative;
    background: rgba(253,246,238,.95);
    border: 3px solid var(--r);
    box-shadow: 6px 6px 0 var(--l), 12px 12px 0 var(--p);
    padding: 2.5rem;
    width: min(460px, 100%);
    color: var(--t);
    animation: fadeUp 0.6s cubic-bezier(.22,1,.36,1) both;
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .purge-card.reveal {
    display: none;
    border-color: var(--l);
    box-shadow: 6px 6px 0 var(--r), 12px 12px 0 var(--p);
  }

  .corner {
    position: absolute; font-family: monospace;
    font-size: 10px; color: var(--p); line-height: 1;
  }
  .tl { top: 6px; left: 8px; }
  .tr { top: 6px; right: 8px; }
  .bl { bottom: 6px; left: 8px; }
  .br { bottom: 6px; right: 8px; }

  .purge-card h2 {
    font-family: monospace; font-size: 1.8rem;
    text-align: center; letter-spacing: 1px;
    margin-bottom: .2rem; color: var(--t);
  }
  .purge-card h2 span { color: var(--r); }

  .purge-sub {
    font-style: italic; text-align: center;
    color: #9e8fad; margin-bottom: 1.5rem;
    font-size: .95rem; font-family: Georgia, serif;
  }

  .purge-div {
    display: flex; align-items: center;
    gap: .5rem; margin-bottom: 1.3rem;
  }
  .purge-dl {
    flex: 1; height: 2px;
    background: repeating-linear-gradient(90deg, var(--r) 0 4px, transparent 4px 8px);
  }

  .purge-card label {
    display: block; font-family: monospace;
    font-size: .68rem; color: #9e8fad;
    letter-spacing: 1px; text-transform: uppercase; margin-bottom: .3rem;
  }
  .purge-field { margin-bottom: 1.1rem; }

  .purge-card input[type=text],
  .purge-card input[type=password] {
    width: 100%; padding: .6rem .8rem;
    border: 2px solid var(--l);
    background: rgba(255,255,255,.85);
    font-family: Georgia, serif; font-size: 1rem;
    color: var(--t); outline: none;
    transition: border-color .2s;
    border-radius: 0;
  }
  .purge-card input:focus { border-color: var(--r); box-shadow: none; }
  .purge-card input::placeholder { color: #c4b8d0; font-style: italic; }

  .purge-btn {
    width: 100%; padding: .7rem;
    background: var(--r); border: 2px solid var(--t);
    box-shadow: 3px 3px 0 var(--t); font-family: monospace;
    font-size: .85rem; color: var(--t); cursor: pointer;
    letter-spacing: 1px; margin-top: .3rem;
    transition: background .15s, transform .1s, box-shadow .1s;
  }
  .purge-btn:hover {
    background: var(--p);
    transform: translate(-1px, -1px);
    box-shadow: 4px 4px 0 var(--t);
  }
  .purge-btn:active {
    transform: translate(2px, 2px);
    box-shadow: 1px 1px 0 var(--t);
  }
  .purge-btn.mint { background: var(--m); }
  .purge-btn.mint:hover { background: var(--p); }

  .purge-note {
    font-size: .75rem; font-style: italic;
    color: #b5a8c4; text-align: center;
    margin-top: 1rem; line-height: 1.5;
    font-family: Georgia, serif;
  }

  /* Loading overlay */
  .purge-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(253,246,238,.96); z-index: 200;
    flex-direction: column; align-items: center;
    justify-content: center; gap: 1rem;
  }
  .purge-overlay.on { display: flex; }
  .purge-lt {
    font-family: monospace; font-size: 1rem;
    color: var(--t); animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
  .purge-lw {
    width: 200px; height: 16px;
    border: 2px solid var(--t); background: var(--c); overflow: hidden;
  }
  .purge-lb {
    height: 100%; width: 0%;
    background: repeating-linear-gradient(90deg, var(--r) 0 8px, var(--l) 8px 16px);
    transition: width 1.8s steps(20);
  }

  /* Ghost */
  .ghost {
    font-family: monospace; font-size: 11px; line-height: 1.4;
    color: var(--l); display: block; white-space: pre;
    text-align: center; margin-bottom: 1rem;
    animation: wb 2s ease-in-out infinite;
  }
  @keyframes wb {
    0%, 100% { transform: translateY(0) rotate(-1deg); }
    50%       { transform: translateY(-5px) rotate(1deg); }
  }

  .reveal-title {
    font-family: monospace; font-size: 1.5rem;
    text-align: center; margin-bottom: .2rem; color: var(--t);
    animation: shake .5s ease .2s both;
  }
  @keyframes shake {
    0%, 100% { transform: translateX(0); }
    20%       { transform: translateX(-6px); }
    40%       { transform: translateX(6px); }
    60%       { transform: translateX(-4px); }
    80%       { transform: translateX(4px); }
  }
  .reveal-title span { color: var(--r); }
  .reveal-tag {
    font-family: monospace; font-size: .7rem; color: var(--l);
    letter-spacing: 2px; text-align: center;
    margin-bottom: 1.3rem; text-transform: uppercase;
  }
  .reveal-msg {
    font-size: 1.05rem; font-style: italic; line-height: 1.7;
    text-align: center; margin-bottom: 1rem;
    font-family: Georgia, serif; color: var(--t);
  }
  .reveal-msg strong { font-style: normal; color: var(--r); }

  .info-box {
    background: rgba(201,184,240,.15); border: 2px solid var(--l);
    padding: .9rem 1.1rem; margin-bottom: 1.3rem;
  }
  .info-box-title {
    font-family: monospace; font-size: .68rem; color: var(--l);
    letter-spacing: 1px; text-transform: uppercase; margin-bottom: .5rem;
  }
  .info-item {
    display: flex; gap: .5rem; margin-bottom: .4rem;
    font-size: .85rem; line-height: 1.5; color: var(--t);
  }
  .info-dot {
    font-family: monospace; font-size: 10px;
    color: var(--r); margin-top: 2px; flex-shrink: 0;
  }
  .purge-sig {
    font-family: monospace; font-size: .65rem;
    color: var(--p); letter-spacing: 1px;
    text-align: center; margin-top: .9rem;
  }

  /* Stars */
  .stars { position: fixed; inset: 0; pointer-events: none; z-index: 0; }
  .star {
    position: absolute; width: 4px; height: 4px;
    animation: tw var(--d) ease-in-out infinite; opacity: 0;
  }
  @keyframes tw { 0%, 100% { opacity: 0; } 50% { opacity: .5; } }

  /* Confetti */
  .confetti-wrap { position: fixed; inset: 0; pointer-events: none; z-index: 1; display: none; }
  .confetti-wrap.on { display: block; }
  .cp { position: absolute; animation: fall linear infinite; opacity: 0; }
  @keyframes fall {
    0%   { transform: translateY(-20px) rotate(0deg);   opacity: 1; }
    100% { transform: translateY(110vh)  rotate(720deg); opacity: .3; }
  }

  /* Dark mode overrides */
  [data-theme="dark"] .purge-card {
    background: rgba(20, 15, 30, 0.95);
    color: #e8d5f0;
  }
  [data-theme="dark"] .purge-card h2 { color: #e8d5f0; }
  [data-theme="dark"] .purge-card input[type=text],
  [data-theme="dark"] .purge-card input[type=password] {
    background: rgba(30, 20, 45, 0.9);
    color: #e8d5f0;
    border-color: #9b7fc0;
  }
  [data-theme="dark"] .purge-card label { color: #b59fd4; }
  [data-theme="dark"] .info-item { color: #e8d5f0; }
  [data-theme="dark"] .reveal-msg { color: #e8d5f0; }
  [data-theme="dark"] .reveal-title { color: #e8d5f0; }
  [data-theme="dark"] .purge-overlay { background: rgba(10,5,20,.96); }
  [data-theme="dark"] .purge-lt { color: #e8d5f0; }
</style>

<div class="stars" id="st"></div>
<div class="confetti-wrap" id="cf"></div>

<div class="purge-wrap">

  <!-- LOGIN CARD -->
  <div class="purge-card" id="lv">
    <span class="corner tl">✦</span><span class="corner tr">✦</span>
    <span class="corner bl">✦</span><span class="corner br">✦</span>
    <h2>Guest <span>Access</span> Portal</h2>
    <p class="purge-sub">Create an account to continue</p>
    <div class="purge-div">
      <div class="purge-dl"></div>
      <span style="font-family:monospace;color:var(--r)">☁</span>
      <div class="purge-dl"></div>
    </div>
    <form onsubmit="go(event)">
      <div class="purge-field">
        <label>Your Name</label>
        <input type="text" id="uname" placeholder="e.g. Guest" autocomplete="off" required>
      </div>
      <div class="purge-field">
        <label>Create a Password</label>
        <input type="password" id="upass" placeholder="something memorable..." required>
      </div>
      <button class="purge-btn" type="submit">✦ REQUEST ACCESS ✦</button>
    </form>
    <p class="purge-note">By creating an account you agree to our terms &amp; conditions and privacy policy.</p>
  </div>

  <!-- REVEAL CARD -->
  <div class="purge-card reveal" id="rv">
    <span class="corner tl">✦</span><span class="corner tr">✦</span>
    <span class="corner bl">✦</span><span class="corner br">✦</span>
    <div class="ghost" id="gh"></div>
    <div class="reveal-title">you silly <span>goober!</span></div>
    <div class="reveal-tag">✦ you just got phished ✦</div>
    <div class="purge-div">
      <div class="purge-dl" style="background:repeating-linear-gradient(90deg,var(--l) 0 4px,transparent 4px 8px)"></div>
      <span style="font-family:monospace;color:var(--l)">♡</span>
      <div class="purge-dl" style="background:repeating-linear-gradient(90deg,var(--l) 0 4px,transparent 4px 8px)"></div>
    </div>
    <p class="reveal-msg">
      This isn't a real guest access portal —<br>
      it's a <strong>fake phishing page</strong>, lovingly crafted<br>
      by your host, <strong>Cicero343</strong>. ʕ•ᴥ•ʔ
    </p>
    <div class="info-box">
      <div class="info-box-title">✦ what just happened?</div>
      <div class="info-item"><span class="info-dot">▶</span><span>This page was designed to look like a legitimate guest access portal — it isn't.</span></div>
      <div class="info-item"><span class="info-dot">▶</span><span>A fake registration form asking for credentials is a classic social engineering trick.</span></div>
      <div class="info-item"><span class="info-dot">▶</span><span>In the real world, credentials entered here could have been logged by an attacker.</span></div>
      <div class="info-item"><span class="info-dot">▶</span><span>Always verify you're on a legitimate site before entering any personal information.</span></div>
    </div>
    <button class="purge-btn mint" onclick="purgeReset()">✦ try again (you won't) ✦</button>
    <p class="purge-note">no credentials were stored. this page is a demonstration of phishing awareness. ♡</p>
    <div class="purge-sig">— cicero343's fake guest access portal —</div>
  </div>

</div>

<!-- LOADING OVERLAY -->
<div class="purge-overlay" id="ov">
  <div style="font-family:monospace;color:var(--l);letter-spacing:2px;font-size:16px">✦ ✦ ✦</div>
  <div class="purge-lt">PROCESSING YOUR SOUL...</div>
  <div class="purge-lw"><div class="purge-lb" id="lb"></div></div>
</div>

<script>
  document.getElementById('gh').textContent =
    "  ░░░░░░  \n ░██████░ \n░█♡░░░♡█░\n░████████░\n░█░░██░░█░\n░████████░\n ░██░░██░ \n  ░░  ░░  ";

  // Stars
  var sc = ['#f2a7bb','#c9b8f0','#a8e6cf','#f7cba8'];
  var st = document.getElementById('st');
  for (var i = 0; i < 30; i++) {
    var x = document.createElement('div');
    x.className = 'star';
    x.style.cssText = 'left:'+Math.random()*100+'%;top:'+Math.random()*100+'%;--d:'+(2+Math.random()*4)+'s;animation-delay:'+(Math.random()*4)+'s;background:'+sc[Math.floor(Math.random()*4)]+';';
    st.appendChild(x);
  }

  // Confetti
  var cf = document.getElementById('cf');
  var cc = ['#f2a7bb','#c9b8f0','#a8e6cf','#f7cba8','#ffd6e0'];
  for (var i = 0; i < 50; i++) {
    var c = document.createElement('div');
    c.className = 'cp';
    c.style.cssText = 'left:'+Math.random()*100+'%;background:'+cc[Math.floor(Math.random()*5)]+';animation-duration:'+(3+Math.random()*4)+'s;animation-delay:'+Math.random()*3+'s;width:'+(4+Math.random()*6)+'px;height:'+(4+Math.random()*6)+'px;';
    cf.appendChild(c);
  }

  function go(e) {
    e.preventDefault();
    var ov = document.getElementById('ov');
    var lb = document.getElementById('lb');
    ov.classList.add('on');
    setTimeout(function() { lb.style.width = '100%'; }, 50);
    setTimeout(function() {
      ov.classList.remove('on');
      lb.style.width = '0%';
      document.getElementById('lv').style.display = 'none';
      document.getElementById('rv').style.display = 'block';
      document.getElementById('cf').classList.add('on');
    }, 2000);
  }

  function purgeReset() {
    document.getElementById('rv').style.display = 'none';
    document.getElementById('cf').classList.remove('on');
    document.getElementById('lv').style.display = 'block';
  }
</script>
