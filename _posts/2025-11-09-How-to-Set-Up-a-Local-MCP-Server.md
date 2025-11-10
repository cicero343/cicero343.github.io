---
title: "How to Set Up a Local MCP Server"
date: 2025-11-09
layout: default
---

<header class="post-header">
  <h1 class="post-title p-name" itemprop="name headline">How to Set Up a Local MCP Server</h1>
  <p class="post-meta">
    <time class="dt-published" datetime="2025-11-09T00:00:00+00:00" itemprop="datePublished">Nov 9, 2025</time>
  </p>
</header>

<div class="post-content e-content" itemprop="articleBody">

<head>
  <link rel="apple-touch-icon" sizes="180x180" href="{{ '/assets/apple-touch-icon.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="32x32" href="{{ '/assets/favicon-32x32.png' | relative_url }}" />
  <link rel="icon" type="image/png" sizes="16x16" href="{{ '/assets/favicon-16x16.png' | relative_url }}" />
  <link rel="icon" type="image/x-icon" href="{{ '/assets/favicon.ico' | relative_url }}" />
  
  <!-- Add Font Awesome for the up arrow icon -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
</head>

<style>
  /* Table of Contents */
  .tableOfContents_bqdL {
    position: fixed;
    top: 120px;
    right: 20px;
    width: 250px;
    background-color: #e8e8e8;
    color: #000000;
    padding: 15px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    z-index: 1000;
    max-height: 70vh;
    overflow-y: auto;
  }

  [data-theme="dark"] .tableOfContents_bqdL {
    background-color: #2a2a2a;
    color: #ffffff;
  }

  .tableOfContents_bqdL h3 {
    margin-top: 0;
    font-size: 1.1rem;
    border-bottom: 2px solid currentColor;
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
    color: inherit;
    transition: font-weight 0.2s;
  }

  .tableOfContents_bqdL a.toc-highlight {
    font-weight: bold;
    color: blue;
  }

  [data-theme="dark"] .tableOfContents_bqdL a.toc-highlight {
    color: #00ff00;
  }

  @media (max-width: 1200px) {
    .tableOfContents_bqdL {
      display: none;
    }
  }

  /* Dark mode fixes for code blocks and tables */
  [data-theme="dark"] code {
    background-color: #1e1e1e;
    color: #00ff00;
  }

  [data-theme="dark"] pre {
    background-color: #1e1e1e;
    color: #00ff00;
  }

  [data-theme="dark"] pre code {
    color: #00ff00;
  }

  /* Mobile-friendly code blocks - prevent horizontal overflow */
  code {
    word-wrap: break-word;
    word-break: break-all;
    white-space: pre-wrap;
    overflow-wrap: break-word;
  }

  pre {
    overflow-x: auto;
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  pre code {
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  [data-theme="dark"] table {
    background-color: #1e1e1e;
  }

  [data-theme="dark"] th {
    background-color: #2a2a2a;
    color: #00ff00;
  }

  [data-theme="dark"] td {
    background-color: #1e1e1e;
    color: #00ff00;
  }

  [data-theme="dark"] tr:nth-child(even) td {
    background-color: #2a2a2a;
  }

  /* Circular back to top button */
  .back-to-top {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background-color: #000000;
    color: #ffffff;
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
    z-index: 9999;
  }

  .back-to-top:hover {
    background-color: #333333;
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.5);
  }

  [data-theme="dark"] .back-to-top {
    background-color: #000000;
    color: #00ff00;
  }

  [data-theme="dark"] .back-to-top:hover {
    background-color: #333333;
  }

  /* Collapsible code box with copy button */
  .code-container {
    margin: 20px 0;
    border: 1px solid #ddd;
    border-radius: 5px;
    background-color: #f5f5f5;
  }

  [data-theme="dark"] .code-container {
    background-color: #1e1e1e;
    border-color: #444;
  }

  .code-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 15px;
    background-color: #e8e8e8;
    border-bottom: 1px solid #ddd;
    border-radius: 5px 5px 0 0;
    cursor: pointer;
    user-select: none;
  }

  [data-theme="dark"] .code-header {
    background-color: #2a2a2a;
    border-bottom-color: #444;
  }

  .code-title {
    font-weight: bold;
    color: #000;
  }

  [data-theme="dark"] .code-title {
    color: #00ff00;
  }

  .code-actions {
    display: flex;
    gap: 10px;
    align-items: center;
  }

  .copy-btn {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 5px 12px;
    border-radius: 3px;
    cursor: pointer;
    font-size: 12px;
    transition: background-color 0.2s;
  }

  .copy-btn:hover {
    background-color: #0056b3;
  }

  .copy-btn.copied {
    background-color: #28a745;
  }

  [data-theme="dark"] .copy-btn {
    background-color: #00ff00;
    color: #000;
  }

  [data-theme="dark"] .copy-btn:hover {
    background-color: #00cc00;
  }

  [data-theme="dark"] .copy-btn.copied {
    background-color: #00aa00;
  }

  .expand-icon {
    color: #666;
    font-size: 14px;
    transition: transform 0.3s;
  }

  [data-theme="dark"] .expand-icon {
    color: #00ff00;
  }

  .expand-icon.expanded {
    transform: rotate(180deg);
  }

  .code-content {
    max-height: 300px;
    overflow-y: auto;
    padding: 15px;
    display: none;
  }

  .code-content.show {
    display: block;
  }

  .code-content pre {
    margin: 0;
    background: none;
    border: none;
    padding: 0;
  }

  .code-content code {
    font-family: 'Courier New', Monaco, monospace;
    font-size: 13px;
    line-height: 1.5;
  }
</style>

<!-- Table of Contents -->
<div class="tableOfContents_bqdL">
  <h3>Contents</h3>
  <ul>
    <li><a href="#introduction">Introduction</a></li>
    <li><a href="#what-is-mcp">What is MCP?</a></li>
    <li><a href="#requirements">Requirements</a></li>
    <li><a href="#step1">Step 1: Install LM Studio</a></li>
    <li><a href="#step2">Step 2: Download a Model</a></li>
    <li><a href="#step3">Step 3: Enable Server Mode</a></li>
    <li><a href="#step4">Step 4: Install Open WebUI</a></li>
    <li><a href="#step5">Step 5: Connect Open WebUI to LM Studio</a></li>
    <li><a href="#step6">Step 6: Install mcpo</a></li>
    <li><a href="#step7">Step 7: Create MCP Servers</a></li>
    <li><a href="#step8">Step 8: Configure PowerShell</a></li>
    <li><a href="#step9">Step 9: Connect to Open WebUI</a></li>
    <li><a href="#testing">Testing Your Setup</a></li>
    <li><a href="#troubleshooting">Troubleshooting</a></li>
  </ul>
</div>

<p><em>A beginner-friendly guide to running a local AI model with file access on your own computer</em></p>

<h2 id="introduction">Introduction</h2>
<p>This guide will walk you through setting up a local MCP (Model Context Protocol) server that allows your AI to interact with files on your computer. By the end, you'll have an AI assistant that can read, write, search files, and monitor your system - all running privately on your machine with no cloud services required.</p>

<div class="info-box">
  <strong>What You'll Build:</strong>
  <ul>
    <li>Local AI model running on your computer</li>
    <li>File system tools (read, write, search files)</li>
    <li>System monitoring tools (CPU, RAM, processes)</li>
    <li>Easy PowerShell commands to manage everything</li>
  </ul>
</div>

<h2 id="what-is-mcp">What is MCP?</h2>
<p>MCP (Model Context Protocol) is essentially a <strong>wrapper for APIs</strong> that allows AI models to use tools. Think of it like this:</p>

<ul>
  <li><strong>Without MCP:</strong> Your AI can only chat - it can't interact with your computer</li>
  <li><strong>With MCP:</strong> Your AI can read files, search documents, check system stats, and more</li>
</ul>

<p>In this setup:</p>
<ul>
  <li><strong>You create Python scripts</strong> that define what tools the AI can use (like "read this file")</li>
  <li><strong>mcpo</strong> (a translator) converts those Python scripts into an API that your AI can call</li>
  <li><strong>Your AI</strong> decides when to use these tools to help answer your questions</li>
</ul>

<div class="info-box">
  <strong>The Flow:</strong><br>
<p><img src="/assets/images/mcpflow.png" alt="LM Studio Server Mode" style="max-width: 100%; height: auto;"></p>
</div>

<h2 id="requirements">Requirements</h2>

<h3>Hardware</h3>
<p>Your GPU determines which AI models you can run. Here's a quick reference:</p>

<table>
  <tr>
    <th>GPU VRAM</th>
    <th>Recommended Model Size</th>
    <th>Example GPUs</th>
  </tr>
  <tr>
    <td>4-6 GB</td>
    <td>3B models</td>
    <td>GTX 1060, RTX 3050</td>
  </tr>
  <tr>
    <td>8-12 GB</td>
    <td>7-8B models</td>
    <td>RTX 3060, RTX 4060, RTX 4070</td>
  </tr>
  <tr>
    <td>16-24 GB</td>
    <td>13-20B models</td>
    <td>RTX 4080, RTX 4090</td>
  </tr>
  <tr>
    <td>24+ GB</td>
    <td>30B+ models</td>
    <td>RTX 4090, Professional GPUs</td>
  </tr>
</table>

<div class="info-box">
  <strong>Tip:</strong> LM Studio will recommend appropriate models based on your hardware when you browse the model library. Look for the green checkmark next to models that will work well on your system.
</div>

<h3>Software Prerequisites</h3>
<ul>
  <li>Windows 10/11</li>
  <li>Python 3.8 or higher (<a href="https://www.python.org/downloads/">Download Python</a>)</li>
  <li>PowerShell (comes with Windows)</li>
  <li>An NVIDIA GPU with updated drivers (for best performance)</li>
</ul>

<br>

<h2 id="step1">Step 1: Install LM Studio</h2>
<p>LM Studio is a desktop app for running AI models locally on your computer.</p>

<ol>
  <li>Download LM Studio from <a href="https://lmstudio.ai/">lmstudio.ai</a></li>
  <li>Install and open the application</li>
  <li>You'll see a welcome screen - we'll download a model in the next step</li>
</ol>

<p>N.B. Select "Power User" at the bottom as shown in the screenshot below, as we will need the extra features it enables later, such as the Developer tab for "Server Mode"</p>
<p>N.B.B Use the search bar at the top to search for models, if it says 'No matching results', then select 'Search more results'</p>

<p><img src="/assets/images/lmstudio2.png" alt="LM Studio" style="max-width: 100%; height: auto;"></p>

<br>

<h2 id="step2">Step 2: Download a Model</h2>
<p>We'll download an <strong>uncensored model</strong> for more flexible conversations. Uncensored models don't have content filters, making them better for creative writing, technical discussions, or any topic without arbitrary restrictions.</p>

<h3>Why Nous Hermes 2 Mistral?</h3>
<ul>
  <li>7 billion parameters - runs well on most GPUs</li>
  <li>Uncensored - no content filtering</li>
  <li>Good at following instructions and using tools</li>
  <li>Not available on Ollama (LM Studio exclusive)</li>
</ul>

<ol>
  <li>In LM Studio, click the <strong>Search</strong> icon (🔍)</li>
  <li>Search for: <code>nous-hermes-2-mistral</code></li>
  <li>Find <strong>NousResearch/Nous-Hermes-2-Mistral-7B-DPO</strong></li>
  <li>Download the <code>Q4_K_M</code> quantization (good balance of quality and speed)</li>
  <li>Wait for the download to complete (several GB)</li>
</ol>

<p>N.B. Notice in the screenshot below that LM Studio tags models your computer can run with a green icon saying "Full GPU Offload Possible" </p>

<p><img src="/assets/images/noushermes.png" alt="Nous Hermes 2 Mistral" style="max-width: 100%; height: auto;"></p>

<div class="warning-box">
  <strong>Alternative:</strong> If you want a code-focused model instead, search for <code>starcoder2</code> or <code>deepseek-coder</code>.
</div>

<br>

<h2 id="step3">Step 3: Enable Server Mode</h2>
<p>Server mode allows other applications (like Open WebUI) to send requests to your AI model via API.</p>

<ol>
  <li>In LM Studio, click the <strong>Developer</strong> tab on the left (2nd tab)</li>
  <li>Select your downloaded model from the dropdown</li>
  <li>Click the toggle next to <strong>Status: Stopped</strong></li>
  <li>You should see: <code>Server started on http://localhost:1234</code></li>
</ol>

<p><img src="/assets/images/lmstudioservermode.png" alt="LM Studio Server Mode" style="max-width: 100%; height: auto;"></p>

<div class="info-box">
  <strong>Keep LM Studio running</strong> while you complete the rest of the setup. The server needs to stay active for your AI to work.
</div>

<br>

<h2 id="step4">Step 4: Install Open WebUI</h2>
<p><a href="https://docs.openwebui.com/">Open WebUI</a> is a ChatGPT-like interface that connects to your local model and supports MCP tools.</p>

<h3>Installation</h3>
<p>Open PowerShell and run:</p>

<pre><code>pip install open-webui</code></pre>

<h3>Start Open WebUI</h3>
<pre><code>open-webui serve</code></pre>

<p>You should see output like:</p>
<pre><code>INFO:     Uvicorn running on http://127.0.0.1:8080</code></pre>

<h3>Access the Interface</h3>
<ol>
  <li>Open your web browser</li>
  <li>Go to: <code>http://localhost:8080</code></li>
  <li>Create an account (stored locally - no internet connection needed)</li>
  <li>You'll see a ChatGPT-like interface</li>
</ol>

<p><img src="/assets/images/openwebui.png" alt="Open WebUI" style="max-width: 100%; height: auto;"></p>

<br>

<h2 id="step5">Step 5: Connect Open WebUI to LM Studio</h2>
<p>Before we can use our local model, we need to connect OpenWebUI to LM Studio's API server.</p>

<h3>Add LM Studio Connection</h3>
<ol>
  <li>Open Open WebUI in your browser (<code>http://localhost:8080</code>)</li>
  <li>Click your profile icon → <strong>Admin Panel</strong></li>
  <li>Go to <strong>Settings</strong> → <strong>Connections</strong></li>
  <li>Under <strong>OpenAI API</strong>, click the <strong>+</strong> button</li>
  <li>In the <strong>Edit Connection</strong> dialog, fill in:
    <ul>
      <li><strong>Connection Type:</strong> Local</li>
      <li><strong>URL:</strong> <code>http://127.0.0.1:1234/v1</code></li>
      <li><strong>Auth:</strong> None (no authentication needed for local connection)</li>
      <li><strong>Provider Type:</strong> OpenAI</li>
    </ul>
  </li>
  <li>Click <strong>Save</strong></li>
</ol>

<p><img src="/assets/images/adminpanelopenwebui.png" alt="Open WebUI Admin Panel" style="max-width: 100%; height: auto;"></p>

<p><img src="/assets/images/openwebuitolmstudio.png" alt="Open WebUI to LM Studio Connection" style="max-width: 100%; height: auto;"></p>

<h3>Verify the Connection</h3>

<p>Once saved, your LM Studio models should appear in Open WebUI's model selector dropdown. You'll now be able to chat with your locally-running model through the Open WebUI interface.</p>

<p><img src="/assets/images/lmstudiomodelsinopenwebui.png" alt="LM Studio models appear in Open WebUI" style="max-width: 100%; height: auto;"></p>

<div class="info-box">
  <strong>Note:</strong> LM Studio must be running with the server active (from Step 3) for this connection to work. If you don't see your models, make sure LM Studio's server is still running.
</div>

<br>

<h2 id="step6">Step 6: Install mcpo</h2>
<p><strong>mcpo</strong> is the translator that bridges MCP servers and Open WebUI. It's officially recommended by Open WebUI.</p>
<p>The Python scripts we will be working with use the MCP protocol (communicating via stdin/stdout), but Open WebUI expects HTTP APIs. mcpo converts between these two, creating a local web server at localhost:8765 that Open WebUI can talk to.</p>

<h3>What mcpo Does</h3>
<ul>
  <li>Takes your Python MCP server as input</li>
  <li>Translates MCP protocol messages into HTTP API endpoints</li>
  <li>Creates a web server that Open WebUI can connect to</li>
  <li>Auto-generates documentation at <code>/docs</code></li>
</ul>

<p>Read more: <a href="https://docs.openwebui.com/openapi-servers/mcp/">Open WebUI's MCP Documentation</a></p>

<h3>Installation</h3>
<pre><code>pip install mcpo</code></pre>

<p>That's it! We'll use mcpo in the next steps to run your MCP servers.</p>

<br>

<h2 id="step7">Step 7: Create Your MCP Servers</h2>
<p>Now we'll create two Python scripts that define what tools your AI can use.</p>

<h3>Setup</h3>
<p>First, create a folder to store your MCP servers:</p>
<pre><code>mkdir C:\Users\YourUsername\MCPServers</code></pre>

<h3>Filesystem MCP (filesystem_mcp.py)</h3>
<p>This server gives your AI the ability to read, write, and search files.</p>

<p><strong>Create a new file:</strong> <code>C:\Users\YourUsername\MCPServers\filesystem_mcp.py</code></p>

<div class="code-container">
  <div class="code-header" onclick="toggleCode(this)">
    <span class="code-title">📄 filesystem_mcp.py</span>
    <div class="code-actions">
      <button class="copy-btn" onclick="copyCode(event, this)">Copy</button>
      <span class="expand-icon">▼</span>
    </div>
  </div>
  <div class="code-content">
    <pre><code>import os
import logging
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp.types import Tool, TextContent

# Setup logging so you can see what's happening
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger("filesystem-mcp")

# === SECURITY: Define allowed directories ===
# Only these paths (and their subdirectories) can be accessed
ALLOWED_PATHS = [
    r"C:\Users", # CHANGE THIS DIRECTORY TO WHERE YOU WANT YOUR MODEL TO ACCESS
]

def is_safe_path(path):
    """Check if the requested path is within allowed directories"""
    try:
        abs_path = os.path.abspath(path)
        for allowed in ALLOWED_PATHS:
            if abs_path.startswith(os.path.abspath(allowed)):
                return True
        return False
    except Exception as e:
        logger.error(f"Error checking path safety: {e}")
        return False

# Create MCP server
app = Server("filesystem-mcp")

@app.list_tools()
async def list_tools() -> list[Tool]:
    """Tell the AI what tools are available"""
    logger.info("AI requested tool list")

    return [
        Tool(
            name="read_file",
            description="Read the complete contents of a text file. Only works for files in allowed directories.",
            inputSchema={
                "type": "object",
                "properties": {
                    "path": {
                        "type": "string",
                        "description": "Full path to the file to read (e.g., C:\\Users\\YourUsername\\Documents\\notes.txt)"
                    }
                },
                "required": ["path"]
            }
        ),
        Tool(
            name="write_file",
            description="Write or overwrite a text file with new content. Creates the file if it doesn't exist.",
            inputSchema={
                "type": "object",
                "properties": {
                    "path": {
                        "type": "string",
                        "description": "Full path where the file should be written"
                    },
                    "content": {
                        "type": "string",
                        "description": "The text content to write to the file"
                    }
                },
                "required": ["path", "content"]
            }
        ),
        Tool(
            name="list_directory",
            description="List all files and folders in a directory. Shows file names only, not contents.",
            inputSchema={
                "type": "object",
                "properties": {
                    "path": {
                        "type": "string",
                        "description": "Full path to the directory to list"
                    }
                },
                "required": ["path"]
            }
        ),
        Tool(
            name="search_files",
            description="Search for files by name pattern in a directory (recursive). Case-insensitive.",
            inputSchema={
                "type": "object",
                "properties": {
                    "directory": {
                        "type": "string",
                        "description": "Directory to search in"
                    },
                    "pattern": {
                        "type": "string",
                        "description": "File name pattern to search for (e.g., '*.txt' or 'meeting')"
                    }
                },
                "required": ["directory", "pattern"]
            }
        ),
        Tool(
            name="search_file_contents",
            description="Search for text INSIDE files (not just filenames). Returns matching lines with context. Useful for finding specific text, code, or notes across multiple files.",
            inputSchema={
                "type": "object",
                "properties": {
                    "directory": {
                        "type": "string",
                        "description": "Directory to search in (searches recursively)"
                    },
                    "search_text": {
                        "type": "string",
                        "description": "Text to search for inside files"
                    },
                    "file_extensions": {
                        "type": "array",
                        "items": {"type": "string"},
                        "description": "Optional: specific file extensions to search (e.g., ['.txt', '.py']). Defaults to common text files."
                    }
                },
                "required": ["directory", "search_text"]
            }
        ),
        Tool(
            name="find_and_replace_file",
            description="Find the FIRST file containing specific text, then replace its ENTIRE contents with new text. This is a combined search + replace operation in one step.",
            inputSchema={
                "type": "object",
                "properties": {
                    "directory": {
                        "type": "string",
                        "description": "Directory to search in"
                    },
                    "search_text": {
                        "type": "string",
                        "description": "Text to search for inside files (will find first file containing this)"
                    },
                    "new_content": {
                        "type": "string",
                        "description": "New content to replace the ENTIRE file contents with"
                    }
                },
                "required": ["directory", "search_text", "new_content"]
            }
        )
    ]

@app.call_tool()
async def call_tool(name: str, arguments: dict) -> list[TextContent]:
    """Handle tool calls from the AI"""
    logger.info(f"Tool called: {name} with arguments: {arguments}")

    if name == "read_file":
        path = arguments["path"]

        if not is_safe_path(path):
            error_msg = f"❌ Access denied: {path}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked read attempt: {path}")
            return [TextContent(type="text", text=error_msg)]

        try:
            with open(path, 'r', encoding='utf-8') as f:
                content = f.read()
            logger.info(f"✅ Successfully read {len(content)} chars from {path}")
            return [TextContent(type="text", text=content)]
        except FileNotFoundError:
            return [TextContent(type="text", text=f"❌ File not found: {path}")]
        except Exception as e:
            logger.error(f"Error reading file: {e}")
            return [TextContent(type="text", text=f"❌ Error reading file: {str(e)}")]

    elif name == "write_file":
        path = arguments["path"]
        content = arguments["content"]

        if not is_safe_path(path):
            error_msg = f"❌ Access denied: {path}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked write attempt: {path}")
            return [TextContent(type="text", text=error_msg)]

        try:
            os.makedirs(os.path.dirname(path), exist_ok=True)
            with open(path, 'w', encoding='utf-8') as f:
                f.write(content)
            logger.info(f"✅ Successfully wrote {len(content)} chars to {path}")
            return [TextContent(type="text", text=f"✅ Successfully wrote to {path} ({len(content)} characters)")]
        except Exception as e:
            logger.error(f"Error writing file: {e}")
            return [TextContent(type="text", text=f"❌ Error writing file: {str(e)}")]

    elif name == "list_directory":
        path = arguments["path"]

        if not is_safe_path(path):
            error_msg = f"❌ Access denied: {path}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked list attempt: {path}")
            return [TextContent(type="text", text=error_msg)]

        try:
            items = os.listdir(path)
            files = []
            dirs = []
            for item in items:
                full_path = os.path.join(path, item)
                if os.path.isdir(full_path):
                    dirs.append(f"📁 {item}")
                else:
                    size = os.path.getsize(full_path)
                    size_str = f"{size:,} bytes" if size < 1024 else f"{size/1024:.1f} KB"
                    files.append(f"📄 {item} ({size_str})")

            result = f"Contents of {path}:\n\n"
            if dirs:
                result += "Directories:\n" + "\n".join(sorted(dirs)) + "\n\n"
            if files:
                result += "Files:\n" + "\n".join(sorted(files))
            if not dirs and not files:
                result += "(empty directory)"

            logger.info(f"✅ Listed {len(dirs)} dirs and {len(files)} files in {path}")
            return [TextContent(type="text", text=result)]
        except FileNotFoundError:
            return [TextContent(type="text", text=f"❌ Directory not found: {path}")]
        except Exception as e:
            logger.error(f"Error listing directory: {e}")
            return [TextContent(type="text", text=f"❌ Error listing directory: {str(e)}")]

    elif name == "search_files":
        directory = arguments["directory"]
        pattern = arguments["pattern"].lower()

        if not is_safe_path(directory):
            error_msg = f"❌ Access denied: {directory}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked search attempt: {directory}")
            return [TextContent(type="text", text=error_msg)]

        try:
            matches = []
            for root, dirs, files in os.walk(directory):
                if not is_safe_path(root):
                    continue
                for file in files:
                    if pattern in file.lower():
                        full_path = os.path.join(root, file)
                        rel_path = os.path.relpath(full_path, directory)
                        matches.append(rel_path)

            if matches:
                result = f"Found {len(matches)} file(s) matching '{pattern}':\n\n"
                result += "\n".join(f"📄 {match}" for match in sorted(matches))
            else:
                result = f"No files found matching '{pattern}' in {directory}"

            logger.info(f"✅ Search completed: {len(matches)} matches for '{pattern}'")
            return [TextContent(type="text", text=result)]
        except Exception as e:
            logger.error(f"Error searching files: {e}")
            return [TextContent(type="text", text=f"❌ Error searching: {str(e)}")]

    elif name == "search_file_contents":
        directory = arguments["directory"]
        search_text = arguments["search_text"].lower()
        file_extensions = arguments.get("file_extensions", [".txt", ".md", ".py", ".js", ".json", ".log", ".csv"])
        
        if not is_safe_path(directory):
            error_msg = f"❌ Access denied: {directory}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked content search attempt: {directory}")
            return [TextContent(type="text", text=error_msg)]
        
        try:
            matches = []
            files_searched = 0
            
            for root, dirs, files in os.walk(directory):
                if not is_safe_path(root):
                    continue
                
                for file in files:
                    file_ext = os.path.splitext(file)[1].lower()
                    if file_extensions and file_ext not in file_extensions:
                        continue
                    
                    full_path = os.path.join(root, file)
                    files_searched += 1
                    
                    try:
                        with open(full_path, 'r', encoding='utf-8', errors='ignore') as f:
                            lines = f.readlines()
                            
                        for line_num, line in enumerate(lines, start=1):
                            if search_text in line.lower():
                                rel_path = os.path.relpath(full_path, directory)
                                match_info = {
                                    'file': rel_path,
                                    'line': line_num,
                                    'content': line.strip()
                                }
                                matches.append(match_info)
                                
                    except (UnicodeDecodeError, PermissionError):
                        continue
            
            if matches:
                result = f"Found '{search_text}' in {len(matches)} location(s) across {files_searched} files:\n\n"
                
                files_with_matches = {}
                for match in matches:
                    if match['file'] not in files_with_matches:
                        files_with_matches[match['file']] = []
                    files_with_matches[match['file']].append(match)
                
                for file_path, file_matches in files_with_matches.items():
                    result += f"📄 {file_path}\n"
                    for match in file_matches[:5]:
                        result += f"   Line {match['line']}: {match['content']}\n"
                    if len(file_matches) > 5:
                        result += f"   ... and {len(file_matches) - 5} more match(es)\n"
                    result += "\n"
            else:
                result = f"No matches found for '{search_text}' in {files_searched} files searched."
            
            logger.info(f"✅ Content search completed: {len(matches)} matches in {files_searched} files")
            return [TextContent(type="text", text=result)]
            
        except Exception as e:
            logger.error(f"Error searching file contents: {e}")
            return [TextContent(type="text", text=f"❌ Error searching: {str(e)}")]

    elif name == "find_and_replace_file":
        directory = arguments["directory"]
        search_text = arguments["search_text"].lower()
        new_content = arguments["new_content"]
        
        if not is_safe_path(directory):
            error_msg = f"❌ Access denied: {directory}\nOnly allowed directories: {', '.join(ALLOWED_PATHS)}"
            logger.warning(f"Blocked find_and_replace attempt: {directory}")
            return [TextContent(type="text", text=error_msg)]
        
        try:
            # Search for the first file containing the text
            found_file = None
            file_extensions = [".txt", ".md", ".py", ".js", ".json", ".log", ".csv"]
            
            for root, dirs, files in os.walk(directory):
                if not is_safe_path(root):
                    continue
                
                for file in files:
                    file_ext = os.path.splitext(file)[1].lower()
                    if file_ext not in file_extensions:
                        continue
                    
                    full_path = os.path.join(root, file)
                    
                    try:
                        with open(full_path, 'r', encoding='utf-8', errors='ignore') as f:
                            content = f.read()
                            
                        if search_text in content.lower():
                            found_file = full_path
                            break
                            
                    except (UnicodeDecodeError, PermissionError):
                        continue
                
                if found_file:
                    break
            
            if not found_file:
                return [TextContent(type="text", text=f"❌ No file found containing '{search_text}' in {directory}")]
            
            # Now replace the file contents
            try:
                with open(found_file, 'w', encoding='utf-8') as f:
                    f.write(new_content)
                
                rel_path = os.path.relpath(found_file, directory)
                logger.info(f"✅ Found and replaced contents of {found_file}")
                return [TextContent(type="text", text=f"✅ Found file '{rel_path}' containing '{search_text}' and replaced its contents with new text ({len(new_content)} characters)")]
                
            except Exception as e:
                logger.error(f"Error writing to file: {e}")
                return [TextContent(type="text", text=f"❌ Found file but failed to write: {str(e)}")]
            
        except Exception as e:
            logger.error(f"Error in find_and_replace: {e}")
            return [TextContent(type="text", text=f"❌ Error: {str(e)}")]

    return [TextContent(type="text", text=f"❌ Unknown tool: {name}")]

if __name__ == "__main__":
    logger.info("=== MCP Filesystem Server Starting ===")
    logger.info(f"Allowed directories: {ALLOWED_PATHS}")
    logger.info("Press Ctrl+C to stop")

    try:
        import asyncio

        async def main():
            async with stdio_server() as (read_stream, write_stream):
                await app.run(
                    read_stream,
                    write_stream,
                    app.create_initialization_options()
                )

        asyncio.run(main())
    except KeyboardInterrupt:
        logger.info("\n=== Server stopped by user ===")
    except Exception as e:
        logger.error(f"Server error: {e}")</code></pre>
  </div>
</div>

<div class="warning-box">
  <strong>Security Note:</strong> Edit the <code>ALLOWED_PATHS</code> at the top of the script to specify which folders the AI can access. Never give it access to system folders or sensitive directories!
</div>

<br>

<h3>System Info MCP (systeminfo_mcp.py)</h3>
<p>This server lets your AI check system stats like CPU usage, RAM, disk space, and running processes.</p>

<p><strong>Create a new file:</strong> <code>C:\Users\YourUsername\MCPServers\systeminfo_mcp.py</code></p>

<div class="code-container">
  <div class="code-header" onclick="toggleCode(this)">
    <span class="code-title">📄 systeminfo_mcp.py</span>
    <div class="code-actions">
      <button class="copy-btn" onclick="copyCode(event, this)">Copy</button>
      <span class="expand-icon">▼</span>
    </div>
  </div>
  <div class="code-content">
    <pre><code>import os
import logging
import psutil
import platform
from datetime import datetime
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp.types import Tool, TextContent

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger("system-info-mcp")

# === SECURITY: Define allowed directories for file searches ===
ALLOWED_SEARCH_PATHS = [
    r"C:\Users", # CHANGE THIS DIRECTORY TO WHERE YOU WANT YOUR MODEL TO ACCESS
]

def is_safe_path(path):
    """Check if path is within allowed directories"""
    try:
        abs_path = os.path.abspath(path)
        for allowed in ALLOWED_SEARCH_PATHS:
            if abs_path.startswith(os.path.abspath(allowed)):
                return True
        return False
    except:
        return False

app = Server("system-info-mcp")

@app.list_tools()
async def list_tools() -> list[Tool]:
    return [
        Tool(
            name="get_full_system_report",
            description="Get a comprehensive system report with ALL information: CPU, RAM, disk, battery, network, uptime, top processes. Use this when asked for complete system overview or 'all stats'.",
            inputSchema={"type": "object", "properties": {}}
        ),
        Tool(
            name="get_system_stats",
            description="Get current CPU usage, RAM usage, and disk space. Read-only, safe.",
            inputSchema={"type": "object", "properties": {}}
        ),
        Tool(
            name="list_processes",
            description="List all running processes with their CPU and memory usage. Read-only, safe.",
            inputSchema={
                "type": "object",
                "properties": {
                    "top_n": {
                        "type": "integer",
                        "description": "Show top N processes by CPU usage (default: 10)"
                    }
                }
            }
        ),
        Tool(
            name="get_disk_info",
            description="Get detailed disk space information for all drives. Read-only, safe.",
            inputSchema={"type": "object", "properties": {}}
        ),
        Tool(
            name="get_network_info",
            description="Get current WiFi network name and IP address. Read-only, safe.",
            inputSchema={"type": "object", "properties": {}}
        ),
        Tool(
            name="get_battery_status",
            description="Get battery percentage and charging status (if laptop). Read-only, safe.",
            inputSchema={"type": "object", "properties": {}}
        ),
        Tool(
            name="find_recent_files",
            description="Find recently modified files in allowed directories only. Read-only, safe.",
            inputSchema={
                "type": "object",
                "properties": {
                    "directory": {
                        "type": "string",
                        "description": "Directory to search (must be in allowed paths)"
                    },
                    "hours": {
                        "type": "integer",
                        "description": "Show files modified in last N hours (default: 24)"
                    }
                },
                "required": ["directory"]
            }
        ),
        Tool(
            name="get_system_info",
            description="Get basic system information (OS, hostname, uptime). Read-only, safe.",
            inputSchema={"type": "object", "properties": {}}
        )
    ]

@app.call_tool()
async def call_tool(name: str, arguments: dict) -> list[TextContent]:
    logger.info(f"Tool called: {name}")

    try:
        if name == "get_full_system_report":
            import socket

            # Gather all information
            cpu_percent = psutil.cpu_percent(interval=1)
            memory = psutil.virtual_memory()
            disk = psutil.disk_usage('C:\\')

            boot_time = datetime.fromtimestamp(psutil.boot_time())
            uptime = datetime.now() - boot_time

            hostname = socket.gethostname()
            local_ip = socket.gethostbyname(hostname)

            battery = psutil.sensors_battery()
            if battery:
                charging = "Charging" if battery.power_plugged else "On Battery"
                battery_str = f"\n\nBattery:\n  Status: {charging}\n  Level: {battery.percent}%"
            else:
                battery_str = "\n\nBattery: Desktop (no battery detected)"

            # Top 5 processes
            processes = []
            for proc in psutil.process_iter(['name', 'cpu_percent']):
                try:
                    processes.append({
                        'name': proc.info['name'],
                        'cpu': proc.info['cpu_percent'] or 0
                    })
                except:
                    continue

            processes.sort(key=lambda x: x['cpu'], reverse=True)
            top_procs = "\n".join([f"  {i+1}. {p['name']} - {p['cpu']:.1f}% CPU"
                                   for i, p in enumerate(processes[:5])])

            # Build report
            result = f"""SYSTEM REPORT
=============

Hardware & OS:
  OS: {platform.system()} {platform.release()}
  Hostname: {hostname}
  Processor: {platform.processor()}
  Uptime: {uptime.days} days, {uptime.seconds//3600} hours

Performance:
  CPU Usage: {cpu_percent}%
  RAM Usage: {memory.percent}% ({memory.used / (1024**3):.1f} GB / {memory.total / (1024**3):.1f} GB)
  RAM Available: {memory.available / (1024**3):.1f} GB
  Disk C Usage: {disk.percent}% ({disk.used / (1024**3):.1f} GB used, {disk.free / (1024**3):.1f} GB free)

Network:
  IP Address: {local_ip}{battery_str}

Top 5 Processes (by CPU):
{top_procs}"""

            return [TextContent(type="text", text=result)]

        elif name == "get_system_stats":
            cpu_percent = psutil.cpu_percent(interval=1)
            memory = psutil.virtual_memory()
            disk = psutil.disk_usage('C:\\')

            result = f"""System Statistics:

CPU Usage: {cpu_percent}%
RAM Usage: {memory.percent}% ({memory.used / (1024**3):.1f} GB / {memory.total / (1024**3):.1f} GB)
Disk C Usage: {disk.percent}% ({disk.used / (1024**3):.1f} GB / {disk.total / (1024**3):.1f} GB)
Available RAM: {memory.available / (1024**3):.1f} GB"""

            return [TextContent(type="text", text=result)]

        elif name == "list_processes":
            top_n = arguments.get("top_n", 10)

            # Get all processes
            processes = []
            for proc in psutil.process_iter(['name', 'cpu_percent', 'memory_percent']):
                try:
                    processes.append({
                        'name': proc.info['name'],
                        'cpu': proc.info['cpu_percent'] or 0,
                        'memory': proc.info['memory_percent'] or 0
                    })
                except (psutil.NoSuchProcess, psutil.AccessDenied):
                    continue

            # Sort by CPU usage
            processes.sort(key=lambda x: x['cpu'], reverse=True)
            top_processes = processes[:top_n]

            result = f"Top {top_n} Processes by CPU Usage:\n\n"
            for i, proc in enumerate(top_processes, 1):
                result += f"{i}. {proc['name']}\n"
                result += f"   CPU: {proc['cpu']:.1f}% | RAM: {proc['memory']:.1f}%\n"

            return [TextContent(type="text", text=result)]

        elif name == "get_disk_info":
            result = "Disk Information:\n\n"

            for partition in psutil.disk_partitions():
                try:
                    usage = psutil.disk_usage(partition.mountpoint)
                    result += f"Drive {partition.device} ({partition.fstype})\n"
                    result += f"   Total: {usage.total / (1024**3):.1f} GB\n"
                    result += f"   Used: {usage.used / (1024**3):.1f} GB ({usage.percent}%)\n"
                    result += f"   Free: {usage.free / (1024**3):.1f} GB\n\n"
                except PermissionError:
                    continue

            return [TextContent(type="text", text=result)]

        elif name == "get_network_info":
            import socket

            hostname = socket.gethostname()
            local_ip = socket.gethostbyname(hostname)

            result = f"""Network Information:

Hostname: {hostname}
Local IP: {local_ip}"""

            # Try to get WiFi name (Windows specific)
            try:
                import subprocess
                output = subprocess.check_output(['netsh', 'wlan', 'show', 'interfaces'],
                                                encoding='utf-8', errors='ignore')
                for line in output.split('\n'):
                    if 'SSID' in line and 'BSSID' not in line:
                        wifi_name = line.split(':')[1].strip()
                        result += f"\nWiFi: {wifi_name}"
                        break
            except:
                pass

            return [TextContent(type="text", text=result)]

        elif name == "get_battery_status":
            battery = psutil.sensors_battery()

            if battery is None:
                result = "No battery detected (desktop computer)"
            else:
                charging = "Charging" if battery.power_plugged else "On Battery"
                percent = battery.percent
                time_left = battery.secsleft

                result = f"""Battery Status:

{charging}
Level: {percent}%"""

                if time_left != psutil.POWER_TIME_UNLIMITED and time_left > 0:
                    hours = time_left // 3600
                    minutes = (time_left % 3600) // 60
                    result += f"\nTime Remaining: {hours}h {minutes}m"

            return [TextContent(type="text", text=result)]

        elif name == "find_recent_files":
            directory = arguments["directory"]
            hours = arguments.get("hours", 24)

            # Security check
            if not is_safe_path(directory):
                return [TextContent(type="text",
                    text=f"Access denied: {directory}\nAllowed: {', '.join(ALLOWED_SEARCH_PATHS)}")]

            if not os.path.exists(directory):
                return [TextContent(type="text", text=f"Directory not found: {directory}")]

            # Find recent files
            now = datetime.now()
            cutoff_time = now.timestamp() - (hours * 3600)
            recent_files = []

            for root, dirs, files in os.walk(directory):
                if not is_safe_path(root):
                    continue

                for file in files:
                    full_path = os.path.join(root, file)
                    try:
                        mtime = os.path.getmtime(full_path)
                        if mtime > cutoff_time:
                            rel_path = os.path.relpath(full_path, directory)
                            age_hours = (now.timestamp() - mtime) / 3600
                            size = os.path.getsize(full_path)
                            size_str = f"{size:,} bytes" if size < 1024 else f"{size/1024:.1f} KB"

                            recent_files.append({
                                'path': rel_path,
                                'age_hours': age_hours,
                                'size': size_str
                            })
                    except:
                        continue

            # Sort by most recent
            recent_files.sort(key=lambda x: x['age_hours'])

            if recent_files:
                result = f"Files modified in last {hours} hours:\n\n"
                for f in recent_files[:20]:
                    age = f"{f['age_hours']:.1f}h ago" if f['age_hours'] >= 1 else f"{f['age_hours']*60:.0f}m ago"
                    result += f"{f['path']}\n   Modified: {age} | Size: {f['size']}\n"

                if len(recent_files) > 20:
                    result += f"\n... and {len(recent_files) - 20} more files"
            else:
                result = f"No files modified in the last {hours} hours in {directory}"

            return [TextContent(type="text", text=result)]

        elif name == "get_system_info":
            boot_time = datetime.fromtimestamp(psutil.boot_time())
            uptime = datetime.now() - boot_time

            result = f"""System Information:

OS: {platform.system()} {platform.release()}
Hostname: {platform.node()}
Uptime: {uptime.days} days, {uptime.seconds//3600} hours
Processor: {platform.processor()}
Python: {platform.python_version()}"""

            return [TextContent(type="text", text=result)]

        return [TextContent(type="text", text=f"Unknown tool: {name}")]

    except Exception as e:
        logger.error(f"Error in {name}: {e}")
        return [TextContent(type="text", text=f"Error: {str(e)}")]

if __name__ == "__main__":
    logger.info("=== System Info MCP Server Starting ===")
    logger.info("READ-ONLY MODE - Safe system monitoring")
    logger.info("Press Ctrl+C to stop")

    try:
        import asyncio

        async def main():
            async with stdio_server() as (read_stream, write_stream):
                await app.run(read_stream, write_stream, app.create_initialization_options())

        asyncio.run(main())
    except KeyboardInterrupt:
        logger.info("\n=== Server stopped by user ===")
    except Exception as e:
        logger.error(f"Server error: {e}")
</code></pre>
  </div>
</div>

<h3>Install Required Library</h3>
<p>The system info script needs the <code>psutil</code> library:</p>
<pre><code>pip install psutil</code></pre>

<br>

<h2 id="step8">Step 8: Configure PowerShell Profile</h2>
<p>We'll create a convenient command to start your MCP servers with an auto-discovery menu. This command handles starting mcpo automatically, so you don't need to run it manually.</p>

<h3>Edit Your PowerShell Profile</h3>
<pre><code>notepad $PROFILE</code></pre>

<p>If you get an error saying the file doesn't exist, create it first:</p>
<pre><code>New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE</code></pre>

<h3>Add This Function</h3>

<div class="code-container">
  <div class="code-header" onclick="toggleCode(this)">
    <span class="code-title">📄 Microsoft.PowerShell_profile.ps1</span>
    <div class="code-actions">
      <button class="copy-btn" onclick="copyCode(event, this)">Copy</button>
      <span class="expand-icon">▼</span>
    </div>
  </div>
  <div class="code-content">
    <pre><code># === MCP SERVER FUNCTIONS ===

function Start-MCPFileSystem {
    param([int]$Port = 8765)

    $mcpFolder = "C:\Users\YourUsername\MCPServers" # PATH TO FOLDER CONTAINING YOUR MCP PYTHON SCRIPTS

    # Find all Python files in the MCP folder
    $scripts = Get-ChildItem "$mcpFolder\*.py" -ErrorAction SilentlyContinue | Sort-Object Name

    if (-not $scripts) {
        Write-Host "No MCP servers found in $mcpFolder" -ForegroundColor Red
        Write-Host "Create Python MCP scripts in that folder to get started." -ForegroundColor Gray
        return
    }

    # If only one script, use it automatically
    if ($scripts.Count -eq 1) {
        $selectedScript = $scripts[0].FullName
        $serverName = $scripts[0].BaseName
        Write-Host "Auto-selected: $serverName" -ForegroundColor Cyan
    } else {
        # Show menu
        Write-Host "Available MCP Servers:" -ForegroundColor Cyan
        Write-Host ""

        for ($i = 0; $i -lt $scripts.Count; $i++) {
            $name = $scripts[$i].BaseName
            $size = [math]::Round($scripts[$i].Length / 1KB, 1)
            Write-Host "  $($i+1). $name" -NoNewline -ForegroundColor White
            Write-Host " ($size KB)" -ForegroundColor DarkGray
        }

        Write-Host ""
        $choice = Read-Host "Select server (1-$($scripts.Count))"

        # Validate choice
        $choiceNum = 0
        if ([int]::TryParse($choice, [ref]$choiceNum) -and $choiceNum -ge 1 -and $choiceNum -le $scripts.Count) {
            $selectedScript = $scripts[$choiceNum - 1].FullName
            $serverName = $scripts[$choiceNum - 1].BaseName
        } else {
            Write-Host "Invalid selection" -ForegroundColor Red
            return
        }
    }

    # Start the server
    Write-Host ""
    Write-Host "Starting MCP Server: $serverName" -ForegroundColor Green
    Write-Host "Access your files through Open WebUI!" -ForegroundColor Green
    Write-Host "API Docs at localhost:$Port/docs" -ForegroundColor Cyan
    Write-Host "Press Ctrl+C to stop" -ForegroundColor Yellow
    Write-Host ""

    mcpo --port $Port -- python $selectedScript
}

Set-Alias -Name startmcp -Value Start-MCPFileSystem</code></pre>
  </div>
</div>

<h3>Reload Your Profile</h3>
<pre><code>. $PROFILE</code></pre>

<h3>Test It</h3>
<pre><code>startmcp</code></pre>

<p>You should see a menu listing your MCP servers:</p>
<pre><code>Available MCP Servers:

  1. filesystem_mcp (3.2 KB)
  2. systeminfo_mcp (2.8 KB)

Select server (1-2):</code></pre>

<p><img src="/assets/images/startmcp.png" alt="startmcp" style="max-width: 100%; height: auto;"></p>

<br>

<h2 id="step9">Step 9: Connect Open WebUI to Your MCP Server</h2>

<h3>Start an MCP Server</h3>
<ol>
  <li>Open PowerShell</li>
  <li>Run: <code>startmcp</code></li>
  <li>Select <code>1</code> for filesystem tools (or <code>2</code> for system info)</li>
  <li>You'll see: <code>Starting MCP Server... API Docs at localhost:8765/docs</code></li>
</ol>

<h3>Connect in Open WebUI</h3>
<ol>
  <li>Open Open WebUI in your browser (<code>http://localhost:8080</code>)</li>
  <li>Click your profile icon → <strong>Admin Panel</strong></li>
  <li>Go to <strong>Settings</strong> → <strong>External Tools</strong></li>
  <li>Click <strong>+ Add Connection</strong></li>
  <li>Fill in:
    <ul>
      <li><strong>Type:</strong> OpenAPI</li>
      <li><strong>Name:</strong> Local MCP Tools</li>
      <li><strong>URL:</strong> <code>http://localhost:8765/openapi.json</code></li>
      <li><strong>Description:</strong> Dynamic tool server - changes based on active MCP server</li>
    </ul>
  </li>
  <li>Click <strong>Save</strong></li>
</ol>

<p><img src="/assets/images/addtooltoopenwebui.png" alt="Open WebUI Add Tool" style="max-width: 100%; height: auto;"></p>

<div class="info-box">
  <strong>Tip:</strong> You can verify the connection by clicking the cycle icon to "Verify Connection" or visiting <code>http://localhost:8765/docs</code> in your browser to see the auto-generated API documentation.
</div>

<br>

<p>Now when you click the button next to the '+' icon, as shown in the screenshot below, you should have a 'Tools' option which will allow your local AI to utilise the MCP tools.</p>

<p><img src="/assets/images/mcptoolsavailableinchat.png" alt="MCP Tools Available in Chat" style="max-width: 100%; height: auto;"></p>

<br>

<h2 id="testing">Testing Your Setup</h2>
<p>Time to see if everything works!</p>

<h3>Test File System Tools</h3>
<p>In Open WebUI, try these commands:</p>

<pre><code>"List the files in C:\Users\YourUsername\Documents"
"Read the file test.txt in my Projects folder"
"Create a file called hello.txt with the text 'Hello, World!'"
"Search for files containing the word 'meeting' in Documents"</code></pre>

<p><img src="/assets/images/filesystemmcp2.png" alt="File System MCP" style="max-width: 100%; height: auto;"></p>

<h3>Test System Info Tools</h3>
<p>Switch your MCP server:</p>
<ol>
  <li>Press <code>Ctrl+C</code> in the PowerShell window running mcpo</li>
  <li>Run <code>startmcp</code> again and select <code>2</code> (systeminfo)</li>
  <li>In Open WebUI, try:</li>
</ol>

<pre><code>"What's my CPU usage?"
"Tell me all stats about my computer"
"Show me the top 5 processes using memory"
"What files did I modify today?"</code></pre>

<p><img src="/assets/images/systeminfomcp.png" alt="File System MCP" style="max-width: 100%; height: auto;"></p>

<br>

<h2 id="troubleshooting">Troubleshooting</h2>

<h3>MCP Server Won't Start</h3>
<p><strong>Error:</strong> <code>ModuleNotFoundError: No module named 'mcp'</code></p>
<p><strong>Solution:</strong> Install the MCP SDK: <code>pip install mcp</code></p>

<p><strong>Error:</strong> <code>No module named 'psutil'</code></p>
<p><strong>Solution:</strong> <code>pip install psutil</code></p>

<h3>Open WebUI Can't Connect</h3>
<p><strong>Check that:</strong></p>
<ul>
  <li>Your MCP server is running (you should see it in PowerShell)</li>
  <li>The URL is exactly: <code>http://localhost:8765/openapi.json</code></li>
  <li>Port 8765 isn't being used by another program</li>
</ul>

<h3>AI Won't Use Tools</h3>
<p><strong>Try:</strong></p>
<ul>
  <li>Being more explicit: "Use the list_directory tool to show files in Documents"</li>
  <li>Check that the connection shows as active in Open WebUI settings</li>
  <li>Make sure your model supports tool use (Nous Hermes 2 does)</li>
</ul>

<h3>Model Running Slow</h3>
<p><strong>Solutions:</strong></p>
<ul>
  <li>Use a smaller quantization (Q4_K_M or Q4_K_S instead of Q8)</li>
  <li>Close other GPU-intensive programs</li>
  <li>Try a smaller model (3B or 1B parameters)</li>
  <li>Check GPU usage in Task Manager → Performance → GPU</li>
</ul>

<h3>Getting "Access Denied" Errors</h3>
<p><strong>Solution:</strong> Check the <code>ALLOWED_PATHS</code> in your MCP script. The folder you're trying to access must be listed there.</p>

<hr>
<br>

<p><strong>Congratulations!</strong> You now have a fully functional local AI with tool use capabilities. Your AI can interact with files, monitor your system, and all of this runs privately on your own computer.</p>

<div class="info-box">
  <strong>More ideas:</strong>
  <ul>
    <li>Create more MCP servers (Git integration, calendar access, etc.)</li>
    <li>Try different AI models for different tasks</li>
    <li>Experiment with tool combinations and refine model instructions</li>
  </ul>
</div>

<!-- Back to Top Button -->
<button onclick="topFunction()" class="back-to-top" title="Go to top">
  <i class="fas fa-chevron-up"></i>
</button>

<script>
  // Back to top button
  const backToTop = document.querySelector('.back-to-top');
  
  window.addEventListener('scroll', function() {
    if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
      backToTop.style.display = "flex";
    } else {
      backToTop.style.display = "none";
    }
    highlightToc();
  });

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

  // Toggle code visibility
  function toggleCode(header) {
    const content = header.nextElementSibling;
    const icon = header.querySelector('.expand-icon');
    
    content.classList.toggle('show');
    icon.classList.toggle('expanded');
  }

  // Copy code to clipboard
  function copyCode(event, button) {
    event.stopPropagation(); // Prevent toggle when clicking copy
    
    const container = button.closest('.code-container');
    const code = container.querySelector('code').textContent;
    
    navigator.clipboard.writeText(code).then(() => {
      const originalText = button.textContent;
      button.textContent = 'Copied!';
      button.classList.add('copied');
      
      setTimeout(() => {
        button.textContent = originalText;
        button.classList.remove('copied');
      }, 2000);
    }).catch(err => {
      console.error('Failed to copy:', err);
      button.textContent = 'Error';
      setTimeout(() => {
        button.textContent = 'Copy';
      }, 2000);
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
