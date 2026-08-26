---
title: "My Local AI Setup, Revisited (2026)"
date: 2026-08-19
layout: default
---

<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">My Local AI Setup, Revisited (2026)</h1>
  <p class="post-meta">
    <time class="dt-published" datetime="2026-08-19T00:00:00+00:00" itemprop="datePublished">Aug, 2026</time>
  </p>
</header>

<div class="post-content e-content" itemprop="articleBody">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">

  <style>
    :root {
      --bg-color-light: #ffffff;
      --txt-color-light: #000000;
      --link-color-light: blue;
      --link-hover-color-light: darkblue;
      --bg-color-dark: #000000;
      --txt-color-dark: #ffffff;
      --link-color-dark: #00ff00;
      --link-hover-color-dark: #00cc00;
      --navbar-bg-color: #f5f5f5;
      --hover-bg-color: #e0e0e0;
      --toc-bg-color: #e8e8e8;
      --code-bg-light: #f5f5f5;
      --code-bg-dark: #1e1e1e;
      --button-bg-light: #000000;
      --button-text-light: #ffffff;
      --button-bg-hover-light: #333333;
      --button-bg-dark: #000000;
      --button-text-dark: #00ff00;
      --button-bg-hover-dark: #333333;
    }

    [data-theme="dark"] {
      --bg-color: var(--bg-color-dark);
      --txt-color: var(--txt-color-dark);
      --link-color-light: var(--link-color-dark);
      --link-hover-color-light: var(--link-hover-color-dark);
      --navbar-bg-color: #333;
      --toc-bg-color: #2a2a2a;
      --code-bg-light: var(--code-bg-dark);
    }

    [data-theme="light"] {
      --bg-color: var(--bg-color-light);
      --txt-color: var(--txt-color-light);
    }

    body {
      background-color: var(--bg-color);
      color: var(--txt-color);
      margin: 0;
      font-family: Arial, sans-serif;
      line-height: 1.6;
    }

    a:link, a:visited {
      color: var(--link-color-light);
    }

    a:hover {
      color: var(--link-hover-color-light);
    }

    .site-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 20px;
      background-color: var(--navbar-bg-color);
    }

    .site-title {
      display: flex;
      align-items: center;
      text-decoration: none;
      color: inherit;
    }

    .site-logo {
      width: 30px;
      height: 30px;
      margin-right: 10px;
    }

    .site-title h1 {
      font-size: 1.3rem;
      margin: 0;
    }

    .toggle-switch {
      display: flex;
      align-items: center;
      margin-left: auto;
    }

    .toggle-switch input {
      display: none;
    }

    .toggle-switch label {
      width: 50px;
      height: 25px;
      position: relative;
      display: block;
      background: #ebebeb;
      border-radius: 12.5px;
      box-shadow: inset 0px 5px 15px rgba(0,0,0,0.4);
      cursor: pointer;
      transition: 0.3s;
    }

    .toggle-switch label:after {
      content: "";
      width: 23px;
      height: 23px;
      position: absolute;
      top: 1px;
      left: 1px;
      background: linear-gradient(180deg, #ffcc89, #d8860b);
      border-radius: 50%;
      box-shadow: 0px 5px 10px rgba(0,0,0,0.2);
      transition: 0.3s;
    }

    .toggle-switch input:checked + label:after {
      left: 26px;
    }

    .page-content {
      width: 100%;
      max-width: 900px;
      margin: 40px auto;
      padding: 0 20px 20px 20px;
      box-sizing: border-box;
    }

    /* The post carries its own main.page-content which nests inside the theme's
       main.page-content. The nested one's padding/margin pushed body text to the
       right of the title. Neutralise the inner one so everything left-aligns. */
    .post-content main.page-content,
    .home main.page-content {
      padding: 0;
      margin: 0;
      max-width: 100%;
      width: 100%;
    }

    .tableOfContents_bqdL {
      position: fixed;
      top: 120px;
      right: 20px;
      width: 250px;
      background-color: var(--toc-bg-color);
      color: var(--txt-color);
      padding: 15px;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      z-index: 1000;
      max-height: 70vh;
      overflow-y: auto;
    }

    .tableOfContents_bqdL h3 {
      margin-top: 0;
      font-size: 1.1rem;
      border-bottom: 2px solid var(--txt-color);
      padding-bottom: 5px;
    }

    .tableOfContents_bqdL ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    .tableOfContents_bqdL li {
      margin: 8px 0;
    }

    .tableOfContents_bqdL a {
      text-decoration: none;
      color: var(--txt-color);
      transition: font-weight 0.2s;
    }

    .tableOfContents_bqdL a.toc-highlight {
      font-weight: bold;
      color: var(--link-color-light);
    }

    @media (max-width: 1200px) {
      .tableOfContents_bqdL {
        display: none;
      }
    }

    h2 {
      color: var(--txt-color);
      border-bottom: 2px solid var(--txt-color);
      padding-bottom: 10px;
      margin-top: 40px;
    }

    h3 {
      color: var(--txt-color);
      margin-top: 30px;
    }

    code {
      background-color: var(--code-bg-light);
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }

    pre {
      background-color: var(--code-bg-light);
      padding: 15px;
      border-radius: 5px;
      overflow-x: auto;
      border-left: 4px solid var(--link-color-light);
    }

    pre code {
      background: none;
      padding: 0;
    }

    .info-box {
      background-color: var(--toc-bg-color);
      padding: 15px;
      border-radius: 5px;
      margin: 20px 0;
      border-left: 4px solid var(--link-color-light);
    }

    .warning-box {
      background-color: #fff3cd;
      color: #856404;
      padding: 15px;
      border-radius: 5px;
      margin: 20px 0;
      border-left: 4px solid #ffc107;
    }

    [data-theme="dark"] .warning-box {
      background-color: #664d03;
      color: #ffecb5;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px 0;
    }

    th, td {
      border: 1px solid var(--txt-color);
      padding: 10px;
      text-align: left;
    }

    th {
      background-color: var(--toc-bg-color);
    }

    /* Circular Back to Top Button - Updated to match GitHub Pages style */
    .back-to-top {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background-color: var(--button-bg-light);
      color: var(--button-text-light);
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 24px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
      display: none;
    }

    .back-to-top:hover {
      background-color: var(--button-bg-hover-light);
      box-shadow: 0 6px 8px rgba(0, 0, 0, 0.5);
    }

    [data-theme="dark"] .back-to-top {
      background-color: var(--button-bg-dark);
      color: var(--button-text-dark);
    }

    [data-theme="dark"] .back-to-top:hover {
      background-color: var(--button-bg-hover-dark);
    }

    img {
      max-width: 100%;
      height: auto;
      border-radius: 5px;
      margin: 15px 0;
    }

    /* Screenshot / media placeholder styling — remove before publishing */
    .placeholder {
      background-color: var(--toc-bg-color);
      border: 2px dashed var(--link-color-light);
      border-radius: 5px;
      padding: 25px 15px;
      margin: 20px 0;
      text-align: center;
      font-style: italic;
      opacity: 0.85;
    }

    /* Consistent screenshot / figure formatting.
       max-width caps how large a screenshot gets on desktop (so they don't dominate
       the column), while width:100% + height:auto lets them shrink on mobile. */
    figure.screenshot {
      margin: 25px auto;
      max-width: 720px;   /* desktop cap — lower this to ~560px for smaller shots if you like */
      text-align: center;
    }

    figure.screenshot img {
      width: 100%;
      height: auto;
      border: 1px solid var(--txt-color);
      border-radius: 6px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
      margin: 0;
    }

    figure.screenshot figcaption {
      margin-top: 8px;
      font-size: 0.85rem;
      font-style: italic;
      opacity: 0.75;
    }

    /* Responsive YouTube embed — caps the player to the content width so it
       can never push the page wider than the screen on mobile. */
    .video-embed {
      position: relative;
      width: 100%;
      max-width: 100%;
      padding-bottom: 56.25%;   /* 16:9 aspect ratio */
      height: 0;
      overflow: hidden;
      margin: 15px 0;
      border-radius: 5px;
    }

    .video-embed iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      max-width: 100%;
      border: 0;
    }

    .repo-link {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 6px 12px;
      border: 1px solid var(--txt-color);
      border-radius: 6px;
      text-decoration: none;
      font-family: 'Courier New', monospace;
      font-size: 0.9rem;
      transition: background-color 0.2s;
    }
    .repo-link:hover { background-color: var(--hover-bg-color); }
    .repo-link i { font-size: 1.1rem; }

    /* ---- Mobile overflow guards ----
       Keep wide elements (code blocks, tables, images, the video) contained so
       they can't stretch the page wider than the screen on phones. Everything
       here is scoped to the post's own content, so it won't touch the site
       header or footer. */

    /* Code blocks: scroll inside their own box instead of pushing the page. */
    pre {
      max-width: 100%;
      overflow-x: auto;
    }

    /* Long inline code (e.g. file paths) wraps instead of forcing width. */
    code {
      overflow-wrap: break-word;
      word-break: break-word;
    }
    pre code {
      overflow-wrap: normal;
      word-break: normal;
      white-space: pre;
    }

    /* Tables: allow horizontal scroll within the content column on small screens. */
    table {
      display: block;
      max-width: 100%;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    /* Images and figures never exceed the column. */
    img,
    figure.screenshot {
      max-width: 100%;
    }

    /* Responsive video wrapper hard-cap (belt and braces with its inline style). */
    .post-content iframe {
      max-width: 100%;
    }
  </style>

  <!-- Table of Contents -->
  <div class="tableOfContents_bqdL">
    <h3>Contents</h3>
    <ul>
      <li><a href="#introduction">Introduction</a></li>
      <li><a href="#voice">The Voice Layer</a></li>
      <li><a href="#models">The Model Stack</a></li>
      <li><a href="#mcp-rethink">Rethinking MCP</a></li>
      <li><a href="#opencode">Installing OpenCode</a></li>
      <li><a href="#testing">Testing in OpenCode</a></li>
      <li><a href="#speed">Local Speed on a 12&nbsp;GB Card</a></li>
      <li><a href="#karpathy">The Command-Wiki Experiment</a></li>
      <li><a href="#skills">Bonus: Skills in OpenCode</a></li>
      <li><a href="#wrap">Where This Leaves Me</a></li>
    </ul>
  </div>

  <main class="page-content">
    <p><em>Nine months on from my last post — leaner models, simpler tooling, and a better understanding of what MCP actually is.</em></p>

    <div class="info-box">
      <strong>Follow-up to:</strong> <a href="https://cicero343.github.io/2025/11/09/How-to-Set-Up-a-Local-MCP-Server.html" target="_blank" rel="noopener noreferrer">How to Set Up a Local MCP Server</a> (Nov 2025). That post was a step-by-step build guide. This one is more of a reflection — what's changed since, and what I got slightly wrong.
    </div>

    <!-- ============================================================= -->
    <h2 id="introduction">Introduction</h2>
    <!-- ============================================================= -->

    <p>Nine months ago I wrote a step-by-step guide to running a local AI with tool access. That post built a specific stack: LM Studio serving a model, OpenWebUI as the chat front-end, and (to give the AI the ability to touch files on my machine) <code>mcpo</code> plus a custom Python MCP server. The whole thing was built around Nous Hermes 2 Mistral 7B, which at the time was a sensible pick for an uncensored model that could use tools.</p>

    <p>I've kept tinkering since, and enough has changed that a "here's the current state" post felt worth writing. This one is less of a build tutorial and more of a reflection — what I'd do differently now, and what I got slightly wrong the first time. Three things in particular have shifted:</p>

    <ul>
      <li><strong>The models.</strong> Nous Hermes has been overtaken. The stack is now built on Google's Gemma 4 family and Qwen's coder model, and the reasoning for each pick is worth spelling out.</li>
      <li><strong>The tooling.</strong> I've started using OpenCode as a local coding agent, and for the file-access use case it has largely removed the need for the MCP proxy layer I built last time.</li>
      <li><strong>My understanding of MCP.</strong> I described MCP as "a wrapper for APIs" in the last post. It's a common simplification, but it isn't accurate, and I want to correct it.</li>
    </ul>

    <p>None of this is a teardown of the old setup — most of it still works. It's just that the sensible defaults moved, and following them made the whole thing leaner and simpler.</p>

    <div class="info-box">
      <strong>My hardware (unchanged since the last post):</strong>
      <ul>
        <li>Intel Core i7-14700</li>
        <li>NVIDIA RTX 4070 SUPER — 12&nbsp;GB VRAM (this is the number that decides everything below)</li>
        <li>32&nbsp;GB DDR4 RAM</li>
        <li>2&nbsp;TB NVMe SSD</li>
        <li>Windows 11</li>
      </ul>
    </div>

    <!-- ============================================================= -->
    <h2 id="voice">The Voice Layer</h2>
    <!-- ============================================================= -->

    <p>A quick note on the front-end before the substantive changes. The LM Studio &rarr; OpenWebUI setup now speaks back to me in a custom voice, cloned via a local <a href="https://github.com/resemble-ai/chatterbox" target="_blank" rel="noopener noreferrer">Chatterbox TTS</a> server. Everything stays on the machine; the text-to-speech runs locally, same as the model.</p>

    <p>The more interesting part is <em>how</em> it's wired. In an earlier iteration I had a browser extension scraping the OpenWebUI page to detect new responses and trigger playback. It worked, but it was fragile — any change to the page structure broke it, and I was effectively maintaining a scraper against a moving target. I've since replaced that with OpenWebUI's native TTS audio path, pointed at the local Chatterbox endpoint. It's a cleaner integration: the front-end hands the text to the TTS server directly instead of me intercepting the DOM. Fewer moving parts, and nothing to re-fix every time OpenWebUI updates.</p>

<!-- SCREENSHOT: OpenWebUI Admin -> Settings -> Audio, TTS engine pointed at the local Chatterbox endpoint -->
    <figure class="screenshot">
      <img src="{{ '/assets/images/OpenWebUIAudioSettings.png' | relative_url }}" alt="OpenWebUI Admin audio settings with the TTS engine pointed at the local Chatterbox endpoint">
      <figcaption>OpenWebUI's audio settings, pointed at the local Chatterbox TTS endpoint.</figcaption>
    </figure>

    <div class="placeholder">
      I was kind of inspired by <a href="https://www.youtube.com/watch?v=E-dHYiEcWN8" target="_blank" rel="noopener noreferrer">this video</a> from No place like localhost. But I note that he uses <a href="https://github.com/studio-dots-ai/dots.tts" target="_blank" rel="noopener noreferrer">dots.tts</a> on Linux for voice cloning and wires it via OpenCode. My Chatterbox setup is on Windows. I've not tried it through OpenCode yet, but I see no reason why it wouldn't work.
    </div>

    <div class="video-embed">
      <iframe src="https://www.youtube-nocookie.com/embed/P3kxNzqStdk"
              title="Local AI voice demo"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
              referrerpolicy="strict-origin-when-cross-origin"
              allowfullscreen loading="lazy">
      </iframe>
    </div>

    <div class="warning-box">
      <strong>Disclaimer:</strong> The voice used in the demo is for illustration only — I don't own the rights to it, and this is a non-commercial personal project.
    </div>

    <p>If you want to build something similar, my repo <a href="https://github.com/cicero343/openwebui-voice-clone" target="_blank" rel="noopener noreferrer">openwebui-voice-clone</a> ships the actual files plus a rebuild recipe — the regenerable stuff (the Python venv, the ~2&nbsp;GB of model weights) is deliberately left out and rebuilt on your own machine rather than committed. The core files are the Chatterbox TTS server (<code>chatterbox_tts_api.py</code>), which exposes an OpenAI-compatible <code>/v1/audio/speech</code> endpoint that OpenWebUI's native TTS calls directly, and a PowerShell profile that wires up the day-to-day commands.</p>

    <p>The fastest way in is the restore helper. After cloning the repo:</p>

    <pre><code>cd openwebui-voice-clone
.\setup.ps1</code></pre>

    <p><code>setup.ps1</code> does the fiddly parts for you — it builds the folder structure and the Python venv (installing CUDA-enabled PyTorch first, which matters), checks your GPU is visible, and prints any manual steps left. After that you drop your own voice-sample WAVs into <code>voices/</code> (they're auto-discovered) and copy the included <code>Microsoft.PowerShell_profile.template.ps1</code>, editing the USER CONFIG block to match your paths.</p>

    <div class="warning-box">
      <strong>Bring your own voice.</strong> The public repo intentionally ships <em>no</em> voice files — voice cloning needs a reference WAV, and you supply your own (a royalty-free sample, or your own recording). Nothing will speak until you've dropped at least one WAV into <code>voices/</code>. This is both the technical reality and the point at which the rights question is yours to get right.
    </div>

    <div class="info-box">
      <strong>Try it out:</strong>
      <a href="https://github.com/cicero343/openwebui-voice-clone" class="repo-link">
        <i class="fab fa-github"></i> cicero343/openwebui-voice-clone
      </a>
    </div>

    <p>For the speech-to-text side specifically, there are polished off-the-shelf options — <a href="https://wisprflow.ai/" target="_blank" rel="noopener noreferrer">Wispr Flow</a> is one many developers use for dictation. It won't do the cloned-voice output, and it isn't fully local (its cleanup step hits the cloud), so it wasn't the route for me — my openwebui-voice-clone setup uses local Whisper for that. But it's worth knowing about if you just want quick, accurate dictation.</p>

    <!-- ============================================================= -->
    <h2 id="models">The Model Stack — Why These, Why Not Others</h2>
    <!-- ============================================================= -->

    <p>The biggest change since the last post is that Nous Hermes is no longer my daily driver. Before listing what replaced it, the guiding principle, because it shaped the whole thing:</p>

    <p><strong>Don't hoard models.</strong> It is very easy to end up with a folder full of half-tested GGUFs — you read a thread, download the model everyone's excited about, run it once, and never open it again. I did a bit of a cull recently and deleted two Starcoder models that a Gemma now beats at light coding. The general rule of thumb is to ensure every model in your stack has one clearly-defined job. Below is what I currently have.</p>

    <table>
      <tr>
        <th>Model</th>
        <th>Role</th>
        <th>Fit on 12&nbsp;GB</th>
      </tr>
      <tr>
        <td><strong>Qwen3-Coder-30B-A3B Instruct</strong></td>
        <td>Dedicated coding (via OpenCode)</td>
        <td>Partial offload — "worth the wait"</td>
      </tr>
      <tr>
        <td><strong>Gemma 4 12B QAT Uncensored</strong></td>
        <td>Daily driver: general, vision, security study, light code</td>
        <td>Full GPU offload</td>
      </tr>
      <tr>
        <td><strong>Gemma 4 12B QAT</strong></td>
        <td>Will probably delete this, just wanted to test guardrails vs uncensored</td>
        <td>Full GPU offload</td>
      </tr>
      <tr>
        <td><strong>Gemma 4 E4B Uncensored</strong></td>
        <td>Fast / lightweight; big-context work in OpenCode</td>
        <td>Full GPU offload, lots of headroom</td>
      </tr>
      <tr>
        <td><strong>Gemma 4 26B A4B</strong></td>
        <td>The only one bringing reasoning + vision + tools together</td>
        <td>Partial offload</td>
      </tr>
      <tr>
        <td><strong>Nous Hermes 2 Mistral 7B DPO</strong></td>
        <td>The original — kept as a bookend; weakest in the stack now</td>
        <td>Full GPU offload</td>
      </tr>
    </table>

    <h3>Active vs. total parameters</h3>

    <p>This is the bit that can be genuinely confusing. Several of these models use a Mixture-of-Experts (MoE) architecture, and MoE models are described with two parameter counts that do very different jobs.</p>

    <p>Take Qwen3-Coder-30B-A3B. The "30B" is the <em>total</em> parameter count; the "A3B" means roughly 3B parameters are <em>active</em> per token. Those two numbers pull in opposite directions when you're planning for a 12&nbsp;GB card:</p>

    <ul>
      <li><strong>Active parameters drive speed.</strong> Only ~3B are doing work on any given token, so the model runs far faster than a dense 30B would. This is why an MoE this size is usable at all on my hardware.</li>
      <li><strong>Total parameters decide whether it fits.</strong> All ~30B still have to live <em>somewhere</em> in memory, even the inactive experts. At a 4-bit quant that's roughly 18&nbsp;GB of weights, more than my 12&nbsp;GB of VRAM, so it can't fully load onto the GPU and spills into system RAM (partial offload). That's why it takes a bit longer to respond, though it's still quick enough to be useful (I put actual numbers on this further down).</li>
    </ul>

    <p>It's easy to read the small "active" number as if it meant the model itself was small. It doesn't. Two models with the same active count can have wildly different footprints. And the naming makes it easy to conflate architectures that are genuinely different: Gemma 4 <strong>E4B</strong> is an "effective 4B" model (small, fits comfortably, lots of VRAM headroom), whereas Gemma 4 <strong>26B A4B</strong> is a 26B-total MoE with ~4B active — both have a "4B" in the description, but one loads easily and the other is a partial-offload job.</p>

    <div class="warning-box">
      <strong>A note on those LM Studio capability tags.</strong> The little "vision / tools / reasoning" badges describe what the model/runtime <em>advertises natively</em> — not a quality ranking. "Supports reasoning" means a thinking mode exists, not that it's good; "supports tools" means the format is present, not that tool-calling is reliable. Case in point: Nous Hermes shows no native tool support, yet in my last post I got it using my MCP server anyway through the right scaffolding. The tags describe native support, not the ceiling of what's possible.
    </div>

    <!-- SCREENSHOT: LM Studio model list showing the vision / tools / reasoning capability badges -->
    <figure class="screenshot">
      <img src="{{ '/assets/images/LMStudioModels.png' | relative_url }}" alt="LM Studio model list showing vision, tools and reasoning capability badges">
      <figcaption>LM Studio's capability badges — they show what a model advertises natively, not how well it does it.</figcaption>
    </figure>

    <!-- ============================================================= -->
    <h2 id="mcp-rethink">Rethinking MCP: A Correction</h2>
    <!-- ============================================================= -->

    <h3>What MCP actually is</h3>

    <p>In the last post I called MCP "essentially a wrapper for APIs." That's a common shorthand and it points roughly the right way, but it isn't accurate. MCP (Model Context Protocol) is an <strong>open standard</strong> for connecting AI applications to external systems, and it defines three kinds of capability a server can expose: <strong>tools</strong> (actions the model can call), <strong>resources</strong> (read-only data it can pull in), and <strong>prompts</strong> (reusable templates). Tool-calling, the thing I built last time, is only one of those three.</p>

    <p>An analogy I've seen is that MCP is "a USB-C port for AI applications": one standard way to plug an app into external systems instead of hand-wiring every tool to every model. MCP sits a layer <em>above</em> function calling. It standardises how tools are described and discovered, but the model still invokes them through its own function-calling underneath. "A wrapper for an API" is one thing you can build with MCP, not what MCP is.</p>

    <h3>The practical change: OpenCode and file access</h3>

    <p>Here's where the correction stops being pedantic. The fiddliest part of the last post was giving the AI file access: it needed <code>mcpo</code> plus a custom Python filesystem MCP server I had to write and maintain. With OpenCode, that whole layer disappears — its file operations (read, write, edit, shell commands) are native built-in tools, so there's no MCP and no proxy involved in letting the agent touch files.</p>

    <p>Every MCP server's tool definitions get injected into the model's context on each request, which on a 12&nbsp;GB card is memory you'd rather spend elsewhere. Native tools keep that overhead down. MCP still earns its place for genuine external tools; but if all you need is to read and write files in a folder, and your tool already does that natively, reaching for MCP is extra plumbing for no gain.</p>

    <!-- ============================================================= -->
    <h2 id="opencode">Installing OpenCode and Pointing It at LM Studio</h2>
    <!-- ============================================================= -->

    <p>This is the one properly how-to section. If you've got LM Studio running as a server already (from the last post, or otherwise), pointing OpenCode at it is quick.</p>

    <h3>Install OpenCode</h3>
    <p>I used the <a href="https://opencode.ai/download" target="_blank" rel="noopener noreferrer">OpenCode Desktop installer</a> rather than the npm/CLI route — consistent with the same GUI-first preference that had me pick LM Studio over raw <code>llama.cpp</code> in the first place. Grab it, install it, open it. Make sure LM Studio is running with your chosen model loaded and its local server started (it listens on <code>http://localhost:1234</code> by default, same as before).</p>

    <h3>Point it at LM Studio</h3>
    <p>OpenCode reads a JSON config from your user profile. Open it:</p>

    <pre><code>notepad "$env:USERPROFILE\.config\opencode\opencode.json"</code></pre>

    <p>Then define a provider that points at LM Studio's local endpoint. The important bits are the <code>baseURL</code> (LM Studio's server) and the model key, which must match the identifier LM Studio serves the model under — you can confirm that string in LM Studio's server/developer tab, or by opening <code>http://localhost:1234/v1/models</code> in a browser. Here's an example for the config:</p>

    <pre><code>{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "lmstudio": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "LM Studio",
      "options": {
        "baseURL": "http://localhost:1234/v1"
      },
      "models": {
        "qwen3-coder-30b-a3b-instruct": {
          "name": "Qwen3 Coder 30B A3B"
        }
      }
    }
  }
}</code></pre>

    <div class="info-box">
      <strong>Remember — context length.</strong> The first time I wired a model into OpenCode it kept failing, and the cause turned out to be the context window. LM Studio was loading the model with a small default context (8192 tokens), which an agent chews through quickly once it's carrying a system prompt, tool definitions and file contents. Bumping the context length up (I use 32768) in LM Studio's model load settings fixed it.
    </div>

    <p>OpenCode isn't the only option here. If you'd rather stay in a familiar & dedicated IDE, you can point VS Code at LM Studio using the <a href="https://marketplace.visualstudio.com/items?itemName=DanLambiase.lmstudio-copilot-provider" target="_blank" rel="noopener noreferrer">LM Studio for Copilot Chat</a> extension. It auto-discovers your models and adds them to VS Code's chat picker, no GitHub sign-in needed. Pick one from the dropdown and it even loads it into LM Studio's server automatically.</p>

    <figure class="screenshot" style="max-width:440px;">
      <img src="{{ '/assets/images/vscode-lmstudio-models.png' | relative_url }}" alt="VS Code chat model picker showing local LM Studio models available for selection">
      <figcaption>The LM Studio models appearing in VS Code's chat model picker.</figcaption>
    </figure>

    <!-- ============================================================= -->
    <h2 id="testing">Testing the Models in OpenCode</h2>
    <!-- ============================================================= -->

    <p>It's worth briefly explaining how OpenCode actually works before showing it in action. You point OpenCode at a folder, and that folder becomes its working directory: it can read, write and edit files inside it, and run shell commands there, all through its own native tools. If you've used Claude Code or a Cowork project, it's the same mental model — the agent operates on a project directory rather than just chatting. That's also what makes the command-wiki experiment later on possible: point it at the vault folder and it can read every note in there directly.</p>

    <p>I tried something simple with a few of my Gemma 4 models and they seemed to work fine with OpenCode. I asked Gemma 4 E4B to make me a simple python script <code>hello.py</code> that prints a greeting, and watched OpenCode create the file in the folder I pointed it at — not paste code into the chat for me to save, but actually use its native write tool to put the file on disk. Seeing the file appear in the project folder is what makes it feel like an actual agent rather than a chat model.</p>

    <!-- SCREENSHOT: OpenCode - Gemma (E4B) generating hello.py, file written to the selected folder -->
    <figure class="screenshot">
      <img src="{{ '/assets/images/Gemma4OpenCode.png' | relative_url }}" alt="OpenCode using Gemma 4 E4B to generate hello.py and write it to the selected folder">
      <figcaption>Gemma E4B in OpenCode writing <code>hello.py</code> straight into the working folder.</figcaption>
    </figure>

    <!-- ============================================================= -->
    <h2 id="speed">Local Speed on a 12&nbsp;GB Card</h2>
    <!-- ============================================================= -->

    <p>A bonus section for the hardware-minded. "Worth the wait" is vague, so here are actual numbers. I gave Qwen3-Coder-30B the same prompt in LM Studio's chat (a small Python script with commented lines) and varied only one setting — how many of the model's layers get offloaded to the GPU versus left in system RAM — while keeping the context length fixed at 32768. On my 12&nbsp;GB RTX 4070 SUPER:</p>

    <table>
      <tr>
        <th>GPU Offload</th>
        <th>Speed</th>
      </tr>
      <tr>
        <td>0 layers (all CPU)</td>
        <td>~16.8 tok/s</td>
      </tr>
      <tr>
        <td>20 layers (partial)</td>
        <td>~24.4 tok/s</td>
      </tr>
      <tr>
        <td>48 layers (maximum)</td>
        <td>~21.5 tok/s</td>
      </tr>
    </table>

    <p>Two things stood out. First, even the worst case — everything on the CPU — runs at about 17 tokens a second, which is faster than I read, so this model is usable even before you touch the offload slider. Offloading some layers to the GPU takes it from "fine" to "comfortably quick."</p>

    <p>Second, and less obviously: maxing out the offload was <em>slower</em> than a partial offload. Pushing all 48 layers onto the card still beat pure CPU, but it lost to the middle setting of 20 — at a 32K context the KV cache needs its own slice of VRAM, and cramming every layer onto a 12&nbsp;GB card leaves too little room for it. A partial offload was the sweet spot, and a good reminder that "turn it all the way up" isn't always fastest.</p>

    <!-- SCREENSHOT: LM Studio chat showing the tok/s stats line under a Qwen response (partial-offload run) -->
    <figure class="screenshot" style="max-width:560px;">
      <img src="{{ '/assets/images/GPUOffload20.png' | relative_url }}" alt="LM Studio chat showing the tokens-per-second stats line under a Qwen response">
      <figcaption>LM Studio's per-response stats line, where the tokens-per-second figures above come from.</figcaption>
    </figure>

    <!-- ============================================================= -->
    <h2 id="karpathy">The Command-Wiki Experiment</h2>
    <!-- ============================================================= -->

    <p>This is the part I'm most interested in, and the reason I wanted to write the post: getting a local model to make good use of my <em>own</em> accumulated knowledge.</p>

    <h3>What it is</h3>
    <p>Over my security study I've built up a library of offensive-security / pentest reference commands, 648 of them at the last count, kept in a single <code>commands.yaml</code>. They come from my own study notes plus curated public sources (<a href="https://gtfobins.org/" target="_blank" rel="noopener noreferrer">GTFOBins</a>, <a href="https://wadcoms.github.io/" target="_blank" rel="noopener noreferrer">WADComs</a>, <a href="https://lolad-project.github.io/" target="_blank" rel="noopener noreferrer">LOLAD</a>, <a href="https://lofl-project.github.io/" target="_blank" rel="noopener noreferrer">LOFLCAB</a>, and an <a href="https://www.stationx.net/nmap-cheat-sheet/" target="_blank" rel="noopener noreferrer">nmap cheat sheet</a>), each reworded into <code>{PLACEHOLDER}</code> templates and re-categorised into a consistent schema. A generator script, <code>generate_wiki.py</code>, projects that library into a linked Obsidian vault: one atomic note per command, a map-of-content page per category (16 of them), a page per tool (44 tools), and a Bases database view for filtering by OS, service, tool or whether a command is destructive.</p>

    <p>It's a study and reference aid for authorised engagements — it assembles and organises commands, it doesn't find or exploit anything itself, and it starts in a build-only mode by default. That scope matters for a point I'll come back to further down.</p>

    <div class="info-box">
      <strong>Try it out:</strong>
      <a href="https://github.com/cicero343/pentest-builder" class="repo-link">
        <i class="fab fa-github"></i> cicero343/pentest-builder
      </a>
    </div>

    <h3>What "Karpathy-style" buys you (and the RAG framing)</h3>

    <p>To be clear about what this does and doesn't do: the wiki doesn't make the model smarter — it doesn't touch the weights, and Qwen is exactly as capable as before. (Changing what the model itself knows would be fine-tuning, a much heavier job.) What it is, is a well-structured <strong>retrieval source</strong> — RAG in spirit. The reason the structure matters is that it fixes the classic RAG failure: naive retrieval pulls back fragments and the model does something mediocre with them. Because every command here is a self-contained note with authoritative frontmatter (the exact command, its OS, whether it's destructive, the tools it needs), the agent retrieves one whole correct note instead of a fragment. The structure <em>is</em> the value — and neatly, it's close to what MCP <em>resources</em> were designed for, except I don't need MCP here since OpenCode reads the vault files natively.</p>

    <h3>Building and maintaining it</h3>
    <p>The initial vault was generated once, with some help from a frontier model to get the structure consistent across hundreds of notes — but that's not the part you'd need to reproduce. The <code>generate_wiki.py</code> script builds and rebuilds the vault from <code>commands.yaml</code>, so keeping it current is just editing the YAML and re-running the script; no AI required. The point isn't how it was first assembled — it's that a structured vault like this works well as a retrieval source for a <em>local</em> model doing everyday lookups.</p>

    <!-- SCREENSHOT: Qwen 30B in OpenCode referencing the Obsidian vault to assemble command files -->
    <figure class="screenshot">
      <img src="{{ '/assets/images/Qwen3Coder30BOpenCode.png' | relative_url }}" alt="Qwen 30B in OpenCode reading the Obsidian vault notes before assembling command files">
      <figcaption>Qwen reading the vault's category and tool notes in OpenCode before generating a command set.</figcaption>
    </figure>

    <div class="info-box">
    <strong>On guardrails and uncensored models.</strong> Qwen worked through this security material without the refusals I'd braced for — it seems fairly uncensored by default for legitimate technical content, which surprised me. Worth being clear on why that's fine: this is a reference library from public sources, scoped to authorised testing, build-only by default. The everyday friction with guardrailed models in security <em>study</em> is false positives — refusing to explain a concept because it snagged on a keyword, not because anything harmful was asked. Avoiding those is the practical case for a local model here, and it's a different thing from wanting help with real harm.
    </div>

    <div class="warning-box">
      <strong>Does the structure actually help?</strong> Honestly, I haven't run a formal head-to-head against just grepping the raw <code>commands.yaml</code>, so I can't give you a benchmark. But it's not a shot in the dark: watching Qwen work, I could see it reading the relevant category and tool notes before generating, and the output came back noticeably more structured and complete than a bare prompt gives. So my read is that the structure does help, probably by steering retrieval to the right notes — I just haven't measured by how much.
    </div>

    <!-- ============================================================= -->
    <h2 id="skills">Bonus: trying Skills in OpenCode</h2>
    <!-- ============================================================= -->

    <p>One last thing worth a mention: <strong>skills</strong>. A skill is a small, self-contained instruction set (plus any helper scripts) you drop into a folder for the agent to pick up; a repeatable capability rather than a one-off prompt. OpenCode discovers them and the model can invoke them on request.</p>

    <p>As a quick test I gave Gemma4 12B QAT Uncensored a <a href="https://playwright.dev/agent-cli/introduction" target="_blank" rel="noopener noreferrer"><code>playwright-cli</code></a> skill and asked it to open google.com, take a screenshot, and close the window. It did exactly that, saving the screenshot into the skill's folder. It's a neat example of a skill handing the model a capability it wouldn't otherwise have.</p>

    <figure class="screenshot">
      <img src="{{ '/assets/images/opencode-skill-playwright.png' | relative_url }}" alt="OpenCode using a playwright-cli skill to open google.com, screenshot it, and close the browser">
      <figcaption>The <code>playwright-cli</code> skill driving a browser from a plain-language request.</figcaption>
    </figure>

    <!-- ============================================================= -->
    <h2 id="wrap">Where This Leaves Me</h2>
    <!-- ============================================================= -->

    <p>The thing that stands out, looking back over nine months, is that everything got <em>simpler</em>. Rather than the stack getting more complex as it got more capable, it actually became leaner: fewer models, each with one clear job. The tooling got simpler too, less MCP rather than more, once OpenCode's native file tools removed the proxy layer I'd built last time. The voice layer went the same way, from a fragile scraper to a supported native path.</p>

    <p>What's changed most, though, is the kind of question I find myself asking. Nine months ago it was "can I even run a capable model locally?" — and the answer now is a comfortable yes, on a mid-range gaming GPU, with several to choose from. The one I'm on now is a level up: "can I organise my own knowledge so a local model makes good use of it?" The command-vault is my first proper attempt, and from what I've seen so far it does seem to help. The next thing I want to poke at is browser automation with a local model — I've written Playwright scripts before, and something like <a href="https://hermes-agent.org/" target="_blank" rel="noopener noreferrer">Hermes Agent</a> (an agent layer from Nous Research that sits on top of an LM Studio server and can drive a browser) looks like a natural fit. The part that intrigues me most is that it builds up a library of reusable skills as it works, so in theory it gets more capable the more you use it.</p>
  </main>

  <!-- Back to Top Button -->
  <button onclick="topFunction()" class="back-to-top" title="Go to top">
    <i class="fas fa-chevron-up"></i>
  </button>

  <script>
    // Back to top button
    const backToTop = document.querySelector('.back-to-top');
    window.onscroll = function() {
      if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
        backToTop.style.display = "flex";
      } else {
        backToTop.style.display = "none";
      }
      highlightToc();
    };

    function topFunction() {
      document.body.scrollTop = 0;
      document.documentElement.scrollTop = 0;
    }

    // Table of contents highlighting
    function highlightToc() {
      const tocLinks = document.querySelectorAll('.tableOfContents_bqdL a');
      let scrollPos = document.documentElement.scrollTop || document.body.scrollTop;

      tocLinks.forEach(link => {
        link.classList.remove('toc-highlight');
        const section = document.querySelector(link.getAttribute('href'));
        if (section) {
          const sectionTop = section.offsetTop - 100;
          const sectionBottom = sectionTop + section.offsetHeight;
          if (scrollPos >= sectionTop && scrollPos < sectionBottom) {
            link.classList.add('toc-highlight');
          }
        }
      });
    }
  </script>

<br>
<br>

</div>

<script src="https://giscus.app/client.js"
        data-repo="cicero343/cicero343.github.io"
        data-repo-id="R_kgDOMgKHgA"
        data-category="Announcements"
        data-category-id="DIC_kwDOMgKHgM4CiNr5"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="dark"
        data-lang="en"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>
