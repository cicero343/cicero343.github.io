---
title: Terminal
permalink: /terminal/
layout: default
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cyberpunk Visual Experience</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        /* Only apply custom cursor and fullscreen effects to the page content, not the header */
        .page-content {
            background: #000;
            overflow: hidden;
            font-family: 'Courier New', monospace;
            cursor: none;
            min-height: calc(100vh - 100px); /* Account for header space */
            position: relative;
        }
        
        /* Keep normal cursor for header/navbar area */
        body {
            background-color: var(--bg-color, #000);
            color: var(--txt-color, #fff);
        }
        
        /* Jekyll page structure - visible and clickable */
        .page-title {
            margin: 1rem 0;
            padding: 0;
            color: var(--txt-color, #fff);
            text-align: left;
            font-family: system-ui, -apple-system, sans-serif;
            position: relative;
            z-index: 1000;
            background: var(--bg-color, #000);
        }
        
        hr {
            margin: 0;
            position: relative;
            z-index: 1000;
        }
        
        .matrix-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(180deg, transparent 0%, rgba(0,0,0,0.8) 100%);
            z-index: 1;
        }
        
        .matrix-char {
            position: absolute;
            color: #00ff00;
            font-family: 'Courier New', monospace;
            font-size: 18px;
            text-shadow: 0 0 10px #00ff00;
            animation: fall linear infinite;
            opacity: 0.8;
        }
        
        @keyframes fall {
            0% {
                transform: translateY(-100px);
                opacity: 1;
            }
            100% {
                transform: translateY(calc(100vh + 100px));
                opacity: 0;
            }
        }
        
        #cursor {
            position: fixed;
            width: 30px;
            height: 30px;
            border: 3px solid #ff0080;
            border-radius: 50%;
            pointer-events: none;
            z-index: 10;
            box-shadow: 
                0 0 20px #ff0080, 
                inset 0 0 20px #ff0080,
                0 0 40px #ff0080;
            animation: pulse 1.5s ease-in-out infinite;
        }
        
        @keyframes pulse {
            0%, 100% { 
                transform: scale(1) rotate(0deg); 
                opacity: 0.8; 
            }
            50% { 
                transform: scale(1.3) rotate(180deg); 
                opacity: 1; 
            }
        }
        
        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: radial-gradient(circle, #00ffff, transparent);
            border-radius: 50%;
            pointer-events: none;
            z-index: 5;
            box-shadow: 0 0 10px #00ffff;
        }
        
        /* Move UI overlay down to avoid navbar */
        #ui-overlay {
            position: fixed;
            top: 120px; /* Moved down from 20px to avoid navbar */
            left: 20px;
            z-index: 9998;
            color: #00ff00;
            font-size: 14px;
            text-shadow: 0 0 10px #00ff00;
            pointer-events: none;
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #00ff00;
        }
        
        #terminal {
            position: fixed;
            bottom: 20px;
            left: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.95);
            border: 1px solid #00ff00;
            border-radius: 8px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            color: #00ff00;
            font-size: 12px;
            z-index: 9999;
            max-height: 300px;
            overflow-y: auto;
            box-shadow: 0 0 30px rgba(0, 255, 0, 0.3);
        }
        
        #terminal-output {
            margin-bottom: 10px;
        }
        
        #terminal-input-line {
            display: flex;
            align-items: center;
        }
        
        #terminal-prompt {
            color: #ff0080;
            margin-right: 5px;
        }
        
        #terminal-input {
            background: transparent;
            border: none;
            color: #00ff00;
            font-family: 'Courier New', monospace;
            font-size: 12px;
            outline: none;
            flex: 1;
            caret-color: #00ff00;
        }
        
        .command-output {
            color: #00ffff;
            margin: 2px 0 5px 0;
            white-space: pre-wrap;
        }
        
        .terminal-line {
            margin: 3px 0;
            opacity: 0;
            animation: fadeInType 0.5s ease-in-out forwards;
        }
        
        @keyframes fadeInType {
            0% { 
                opacity: 0; 
                transform: translateX(-20px); 
            }
            100% { 
                opacity: 1; 
                transform: translateX(0); 
            }
        }
        
        .neon-box {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 300px;
            height: 200px;
            border: 2px solid #ff0080;
            border-radius: 15px;
            box-shadow: 
                0 0 20px #ff0080,
                inset 0 0 20px rgba(255, 0, 128, 0.1);
            z-index: 5;
            animation: neonGlow 3s ease-in-out infinite alternate;
        }
        
        @keyframes neonGlow {
            0% {
                box-shadow: 
                    0 0 20px #ff0080,
                    inset 0 0 20px rgba(255, 0, 128, 0.1);
                border-color: #ff0080;
            }
            50% {
                box-shadow: 
                    0 0 40px #00ffff,
                    inset 0 0 40px rgba(0, 255, 255, 0.2);
                border-color: #00ffff;
            }
            100% {
                box-shadow: 
                    0 0 60px #00ff00,
                    inset 0 0 60px rgba(0, 255, 0, 0.2);
                border-color: #00ff00;
            }
        }
        
        .glitch-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            font-weight: bold;
            color: #fff;
            text-shadow: 
                2px 0 #ff0080,
                -2px 0 #00ffff;
            animation: glitch 2s infinite;
        }
        
        @keyframes glitch {
            0% {
                text-shadow: 
                    2px 0 #ff0080,
                    -2px 0 #00ffff;
            }
            25% {
                text-shadow: 
                    -2px 0 #ff0080,
                    2px 0 #00ffff;
            }
            50% {
                text-shadow: 
                    2px 2px #ff0080,
                    -2px -2px #00ffff;
            }
            75% {
                text-shadow: 
                    -2px 2px #ff0080,
                    2px -2px #00ffff;
            }
            100% {
                text-shadow: 
                    2px 0 #ff0080,
                    -2px 0 #00ffff;
            }
        }
        
        .scanlines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(
                0deg,
                transparent,
                transparent 2px,
                rgba(0, 255, 0, 0.03) 2px,
                rgba(0, 255, 0, 0.03) 4px
            );
            pointer-events: none;
            z-index: 9997;
            animation: scanlineMove 0.1s linear infinite;
        }
        
        @keyframes scanlineMove {
            0% { transform: translateY(0); }
            100% { transform: translateY(4px); }
        }
        
        .screen-distortion {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 25;
            opacity: 0;
        }
        
        .distortion-active {
            opacity: 1;
            background: linear-gradient(
                90deg,
                transparent 0%,
                rgba(255, 0, 128, 0.1) 25%,
                rgba(0, 255, 255, 0.1) 50%,
                rgba(0, 255, 0, 0.1) 75%,
                transparent 100%
            );
            animation: distort 0.3s ease-in-out;
        }
        
        @keyframes distort {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }
        
        .floating-icons {
            position: fixed;
            color: #00ffff;
            font-size: 20px;
            text-shadow: 0 0 15px #00ffff;
            z-index: 8;
            animation: float 4s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        /* Ensure navbar/header area keeps normal cursor and is clickable */
        nav, header, .header, .navbar, a {
            cursor: pointer !important;
            pointer-events: auto !important;
            position: relative;
            z-index: 1001 !important;
        }

        /* Make sure links work */
        nav a, header a, .header a, .navbar a {
            cursor: pointer !important;
            pointer-events: auto !important;
        }
    </style>
</head>
<body>

    
    <!-- Page content wrapper -->
    <div class="page-content">
        <div class="matrix-bg" id="matrix-container"></div>
        <div class="scanlines"></div>
        <div class="screen-distortion" id="distortion"></div>
        
        <div id="cursor"></div>
        
        <div class="neon-box">
            <div class="glitch-text">SYSTEM BREACH</div>
        </div>
        
        <div id="ui-overlay">
            <div>◈ NEURAL LINK: ACTIVE</div>
            <div>◈ REALITY LEVEL: <span id="reality">89</span>%</div>
            <div>◈ ANOMALIES: <span id="anomalies">0</span></div>
            <div>◈ CURSOR POS: <span id="cursor-pos">0, 0</span></div>
            <div>◈ STATUS: <span id="status">MONITORING</span></div>
        </div>
        
        <div id="terminal">
            <div id="terminal-output">
                <div class="terminal-line">[INIT] Cyberpunk reality overlay initialized...</div>
                <div class="terminal-line">[WARN] Detected anomalous neural activity</div>
                <div class="terminal-line">[INFO] Interactive terminal enabled - try Linux commands!</div>
                <div class="terminal-line">[INFO] Click anywhere to trigger system events</div>
            </div>
            <div id="terminal-input-line">
                <span id="terminal-prompt">root@matrix:~# </span>
                <input type="text" id="terminal-input" autocomplete="off" spellcheck="false">
            </div>
        </div>
    </div>

    <script>
        // Mouse tracking and cursor - only track within page content area
        let mouseX = 0, mouseY = 0;
        const cursor = document.getElementById('cursor');
        const pageContent = document.querySelector('.page-content');
        
        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            cursor.style.left = (mouseX - 15) + 'px';
            cursor.style.top = (mouseY - 15) + 'px';
            
            document.getElementById('cursor-pos').textContent = `${mouseX}, ${mouseY}`;
            
            // Only create particles if mouse is over the page content area
            if (pageContent) {
                const rect = pageContent.getBoundingClientRect();
                if (mouseY >= rect.top) {
                    createParticle(mouseX, mouseY);
                }
            }
        });
        
        // Matrix characters
        const matrixChars = 'ｱｲｳｴｵｶｷｸｹｺｻｼｽｾｿﾀﾁﾂﾃﾄﾅﾆﾇﾈﾉﾊﾋﾌﾍﾎﾏﾐﾑﾒﾓﾔﾕﾖﾗﾘﾙﾚﾛﾜｦﾝ01234567890ABCDEF';
        
        function createMatrixChar() {
            const char = document.createElement('div');
            char.className = 'matrix-char';
            char.textContent = matrixChars[Math.floor(Math.random() * matrixChars.length)];
            char.style.left = Math.random() * window.innerWidth + 'px';
            char.style.animationDuration = (Math.random() * 3 + 2) + 's';
            char.style.fontSize = (Math.random() * 10 + 14) + 'px';
            
            document.getElementById('matrix-container').appendChild(char);
            
            setTimeout(() => {
                char.remove();
            }, 5000);
        }
        
        // Create particles
        function createParticle(x, y) {
            const particle = document.createElement('div');
            particle.className = 'particle';
            particle.style.left = x + 'px';
            particle.style.top = y + 'px';
            
            const vx = (Math.random() - 0.5) * 4;
            const vy = (Math.random() - 0.5) * 4;
            
            document.body.appendChild(particle);
            
            let life = 100;
            const animate = () => {
                life -= 2;
                x += vx;
                y += vy;
                
                particle.style.left = x + 'px';
                particle.style.top = y + 'px';
                particle.style.opacity = life / 100;
                
                if (life > 0) {
                    requestAnimationFrame(animate);
                } else {
                    particle.remove();
                }
            };
            
            animate();
        }
        
        // Click effects - only trigger if clicking in page content area
        document.addEventListener('click', (e) => {
            // Don't trigger effects if clicking on terminal or if clicking on header/nav area
            if (e.target.closest('#terminal') || e.target.closest('nav') || e.target.closest('header') || e.target.closest('.header') || e.target.closest('.navbar') || e.target.tagName === 'A') {
                return;
            }

            // Only trigger if clicking in the page content area
            if (pageContent) {
                const rect = pageContent.getBoundingClientRect();
                if (e.clientY < rect.top) {
                    return; // Don't trigger effects for clicks in header area
                }
            }
            
            // Screen distortion
            const distortion = document.getElementById('distortion');
            distortion.classList.add('distortion-active');
            setTimeout(() => {
                distortion.classList.remove('distortion-active');
            }, 300);
            
            // Particle burst
            for (let i = 0; i < 20; i++) {
                setTimeout(() => createParticle(e.clientX, e.clientY), i * 20);
            }
            
            // Update anomaly counter
            const anomalies = document.getElementById('anomalies');
            anomalies.textContent = parseInt(anomalies.textContent) + 1;
        });
        
        // Terminal messages
        function addTerminalMessage(message, isCommand = false) {
            const output = document.getElementById('terminal-output');
            const line = document.createElement('div');
            
            if (isCommand) {
                line.className = 'command-output';
            } else {
                line.className = 'terminal-line';
            }
            
            line.textContent = message;
            output.appendChild(line);
            
            // Keep only last 20 lines
            while (output.children.length > 20) {
                output.removeChild(output.firstChild);
            }
            
            document.getElementById('terminal').scrollTop = document.getElementById('terminal').scrollHeight;
        }
        
        // Interactive Terminal System
        const terminalInput = document.getElementById('terminal-input');
        const currentDirectory = { path: '/home/matrix', user: 'root' };
        const fileSystem = {
            '/': ['bin', 'home', 'proc'],
            '/home': ['matrix'],
            '/home/matrix': ['secrets.txt', 'neural_net.py', 'reality.cfg'],
            '/bin': ['ls', 'cat', 'ps', 'top'],
            '/proc': ['cpuinfo', 'meminfo']
        };
        
        const processes = [
            'neural_link     1234  matrix  20   0  256M  128M  running  00:42:33  neural_interface',
            'reality_sync    5678  root    15   0  512M  256M  sleeping 01:23:45  reality_manager',
            'quantum_flux    9012  matrix  10   0  128M   64M  running  00:15:22  quantum_processor',
            'data_stream     3456  root     5   0   64M   32M  running  02:45:12  data_handler',
            'anomaly_scan    7890  matrix  25   0  1024M 512M  running  00:07:33  anomaly_detector'
        ];
        
        function executeCommand(command) {
            const args = command.trim().split(' ');
            const cmd = args[0].toLowerCase();
            
            // Show the command being executed
            addTerminalMessage(`${currentDirectory.user}@matrix:${currentDirectory.path}# ${command}`);
            
            switch (cmd) {
                case 'help':
                    addTerminalMessage('=== GAMES ===', true);
                    addTerminalMessage('snake      - Classic Snake game', true);
                    addTerminalMessage('pong       - Classic Pong game', true);
                    addTerminalMessage('=== VISUAL EFFECTS ===', true);
                    addTerminalMessage('rain       - Matrix rain storm', true);
                    addTerminalMessage('glitch     - Reality inversion', true);
                    addTerminalMessage('ghost      - Fade to transparent', true);
                    addTerminalMessage('shake      - Screen shake', true);
                    addTerminalMessage('=== HACKER COMMANDS ===', true);
                    addTerminalMessage('hack       - Multi-stage hack sequence', true);
                    addTerminalMessage('scan       - Network discovery', true);
                    addTerminalMessage('trace      - Connection tracing', true);
                    addTerminalMessage('decrypt    - File decryption', true);
                    addTerminalMessage('override   - Emergency override', true);
                    addTerminalMessage('virus      - Deploy/contain virus', true);
                    addTerminalMessage('=== SYSTEM COMMANDS ===', true);
                    addTerminalMessage('ls, cd, pwd, ps, top, cat, date, clear', true);
                    addTerminalMessage('sysinfo    - Analyze target system', true);
                    addTerminalMessage('=== EASTER EGGS ===', true);
                    addTerminalMessage('cat secrets.txt, cat reality.cfg', true);
                    break;
                case 'sysinfo':
                    addTerminalMessage('Scanning target system...', true);
                    document.querySelector('.glitch-text').textContent = 'SYSTEM SCAN';
                    
                    setTimeout(() => {
                        addTerminalMessage('=== TARGET SYSTEM ANALYSIS ===', true);
                        addTerminalMessage(`Platform: ${navigator.platform}`, true);
                        
                        // Clean up user agent for display
                        const userAgent = navigator.userAgent;
                        const browserMatch = userAgent.match(/(Chrome|Firefox|Safari|Edge|Opera)\/[\d.]+/);
                        const browser = browserMatch ? browserMatch[0] : userAgent.split(' ')[0];
                        addTerminalMessage(`Browser: ${browser}`, true);
                        
                        addTerminalMessage(`Screen Resolution: ${screen.width}x${screen.height}`, true);
                        addTerminalMessage(`Color Depth: ${screen.colorDepth}-bit`, true);
                        addTerminalMessage(`Timezone: ${Intl.DateTimeFormat().resolvedOptions().timeZone}`, true);
                        addTerminalMessage(`Language: ${navigator.language}`, true);
                        addTerminalMessage(`CPU Cores: ${navigator.hardwareConcurrency || 'Unknown'}`, true);
                        
                        // Memory info (if available)
                        if (navigator.deviceMemory) {
                            addTerminalMessage(`Device Memory: ${navigator.deviceMemory}GB`, true);
                        }
                        
                        // Connection info (if available)
                        if (navigator.connection) {
                            addTerminalMessage(`Connection: ${navigator.connection.effectiveType || 'Unknown'}`, true);
                        }
                        
                        // Battery info (if available)
                        if ('getBattery' in navigator) {
                            navigator.getBattery().then(battery => {
                                const batteryLevel = Math.round(battery.level * 100);
                                const charging = battery.charging ? 'Charging' : 'Not charging';
                                addTerminalMessage(`Battery: ${batteryLevel}% (${charging})`, true);
                            }).catch(() => {
                                addTerminalMessage('Battery: Access denied', true);
                            });
                        }
                        
                        // Other system info
                        addTerminalMessage(`Cookies: ${navigator.cookieEnabled ? 'Enabled' : 'Disabled'}`, true);
                        addTerminalMessage(`Network Status: ${navigator.onLine ? 'Online' : 'Offline'}`, true);
                        addTerminalMessage(`Java: ${navigator.javaEnabled() ? 'Enabled' : 'Disabled'}`, true);
                        
                        // Touch support
                        const touchSupport = 'ontouchstart' in window || navigator.maxTouchPoints > 0;
                        addTerminalMessage(`Touch Support: ${touchSupport ? 'Yes' : 'No'}`, true);
                        
                        // Session info
                        const sessionTime = Math.round(performance.now() / 1000);
                        addTerminalMessage(`Session Time: ${sessionTime}s`, true);
                        
                        // Fake security assessment
                        setTimeout(() => {
                            addTerminalMessage('--- SECURITY ASSESSMENT ---', true);
                            const riskFactors = [];
                            if (navigator.cookieEnabled) riskFactors.push('Cookies enabled');
                            if (navigator.javaEnabled()) riskFactors.push('Java enabled');
                            if (touchSupport) riskFactors.push('Touch interface detected');
                            
                            const riskLevel = riskFactors.length > 2 ? 'HIGH' : riskFactors.length > 0 ? 'MEDIUM' : 'LOW';
                            addTerminalMessage(`Risk Level: ${riskLevel}`, true);
                            addTerminalMessage(`Vulnerabilities Found: ${riskFactors.length}`, true);
                            
                            setTimeout(() => {
                                addTerminalMessage('System analysis complete.', true);
                                document.querySelector('.glitch-text').textContent = 'ANALYSIS COMPLETE';
                                setTimeout(() => {
                                    document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                                }, 3000);
                            }, 1000);
                        }, 2000);
                    }, 1500);
                    break;
                    
                case 'snake':
                    addTerminalMessage('Loading Snake game...', true);
                    document.querySelector('.glitch-text').textContent = 'SNAKE GAME ACTIVE';
                    setTimeout(() => createSnakeGame(), 100);
                    break;
                    
                case 'pong':
                    addTerminalMessage('Loading Pong game...', true);
                    document.querySelector('.glitch-text').textContent = 'PONG GAME ACTIVE';
                    createPongGame();
                    break;
                    
                case 'ls':
                    const path = args[1] || currentDirectory.path;
                    if (fileSystem[path]) {
                        addTerminalMessage(fileSystem[path].join('  '), true);
                    } else {
                        addTerminalMessage(`ls: cannot access '${path}': No such file or directory`, true);
                    }
                    break;
                    
                case 'cd':
                    if (!args[1]) {
                        currentDirectory.path = '/home/matrix';
                    } else if (args[1] === '..') {
                        const pathParts = currentDirectory.path.split('/');
                        pathParts.pop();
                        currentDirectory.path = pathParts.join('/') || '/';
                    } else if (args[1].startsWith('/')) {
                        if (fileSystem[args[1]]) {
                            currentDirectory.path = args[1];
                        } else {
                            addTerminalMessage(`cd: ${args[1]}: No such file or directory`, true);
                        }
                    } else {
                        const newPath = currentDirectory.path === '/' ? `/${args[1]}` : `${currentDirectory.path}/${args[1]}`;
                        if (fileSystem[newPath]) {
                            currentDirectory.path = newPath;
                        } else {
                            addTerminalMessage(`cd: ${args[1]}: No such file or directory`, true);
                        }
                    }
                    document.getElementById('terminal-prompt').textContent = `${currentDirectory.user}@matrix:${currentDirectory.path}# `;
                    break;
                    
                case 'pwd':
                    addTerminalMessage(currentDirectory.path, true);
                    break;
                    
                case 'whoami':
                    addTerminalMessage(currentDirectory.user, true);
                    break;
                    
                case 'ps':
                    addTerminalMessage('PID    PPID   USER     PRI  NI   VIRT   RES   STAT  TIME     COMMAND', true);
                    processes.forEach(proc => addTerminalMessage(proc, true));
                    break;
                    
                case 'top':
                    addTerminalMessage('Tasks: 47 total, 5 running, 42 sleeping', true);
                    addTerminalMessage('CPU usage: 23.7% user, 8.2% system, 68.1% idle', true);
                    addTerminalMessage('Memory: 4096MB total, 2048MB used, 2048MB free', true);
                    addTerminalMessage('Neural Interface Load: 67%', true);
                    break;
                    
                case 'cat':
                    if (args[1] === 'secrets.txt') {
                        addTerminalMessage('THE MATRIX HAS YOU...', true);
                        addTerminalMessage('Wake up, Neo.', true);
                        addTerminalMessage('Follow the white rabbit.', true);
                    } else if (args[1] === 'reality.cfg') {
                        addTerminalMessage('[REALITY_ENGINE]', true);
                        addTerminalMessage('physics_enabled=true', true);
                        addTerminalMessage('gravity_constant=9.81', true);
                        addTerminalMessage('matrix_mode=active', true);
                        addTerminalMessage('glitch_probability=0.01', true);
                    } else if (args[1] === '/proc/cpuinfo') {
                        addTerminalMessage('processor: Quantum Neural Processing Unit', true);
                        addTerminalMessage('model: NeuroLink X1', true);
                        addTerminalMessage('cores: 8 quantum cores', true);
                        addTerminalMessage('frequency: 3.7 THz', true);
                    } else if (args[1]) {
                        addTerminalMessage(`cat: ${args[1]}: File not found or access denied`, true);
                    } else {
                        addTerminalMessage('cat: missing file operand', true);
                    }
                    break;
                    
                case 'rain':
                    addTerminalMessage('Intensifying digital rain...', true);
                    document.querySelector('.glitch-text').textContent = 'DIGITAL RAIN ACTIVE';
                    const rainInterval = setInterval(() => {
                        for (let i = 0; i < 5; i++) {
                            createMatrixChar();
                        }
                    }, 100);
                    
                    setTimeout(() => {
                        clearInterval(rainInterval);
                        addTerminalMessage('Rain intensity normalized', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 10000);
                    break;
                    
                case 'glitch':
                    addTerminalMessage('Initiating reality glitch...', true);
                    document.querySelector('.glitch-text').textContent = 'REALITY ERROR';
                    document.body.style.filter = 'invert(1) hue-rotate(180deg) saturate(2)';
                    setTimeout(() => {
                        document.body.style.filter = '';
                        addTerminalMessage('Reality restored', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 3000);
                    break;
                    
                case 'ghost':
                    addTerminalMessage('Activating ghost mode...', true);
                    document.querySelector('.glitch-text').textContent = 'GHOST PROTOCOL';
                    document.body.style.opacity = '0.3';
                    setTimeout(() => {
                        document.body.style.opacity = '1';
                        addTerminalMessage('Ghost mode deactivated', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 5000);
                    break;
                    
                case 'shake':
                    addTerminalMessage('Initiating screen shake...', true);
                    document.querySelector('.glitch-text').textContent = 'SEISMIC ANOMALY';
                    document.body.style.animation = 'glitch 0.5s ease-in-out 6';
                    setTimeout(() => {
                        document.body.style.animation = '';
                        addTerminalMessage('Stabilizers online', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 3000);
                    break;
                    
                case 'scan':
                    addTerminalMessage('Scanning local network...', true);
                    document.querySelector('.glitch-text').textContent = 'NETWORK SCAN';
                    setTimeout(() => addTerminalMessage('Found: 127.0.0.1 (localhost)', true), 500);
                    setTimeout(() => addTerminalMessage('Found: 192.168.1.1 (router)', true), 1000);
                    setTimeout(() => addTerminalMessage('Found: UNKNOWN_DEVICE (???)', true), 1500);
                    setTimeout(() => {
                        addTerminalMessage('Scan complete. 3 devices found.', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 2000);
                    break;
                    
                case 'hack':
                    addTerminalMessage('Initializing neural hack protocol...', true);
                    document.querySelector('.glitch-text').textContent = 'HACKING...';
                    setTimeout(() => {
                        addTerminalMessage('Bypassing firewall... [OK]', true);
                        document.querySelector('.glitch-text').textContent = 'FIREWALL BYPASSED';
                    }, 1000);
                    setTimeout(() => {
                        addTerminalMessage('Cracking encryption... [OK]', true);
                        document.querySelector('.glitch-text').textContent = 'ENCRYPTION CRACKED';
                    }, 2000);
                    setTimeout(() => {
                        addTerminalMessage('Access granted to Matrix mainframe', true);
                        document.querySelector('.glitch-text').textContent = 'ACCESS GRANTED';
                    }, 3000);
                    setTimeout(() => {
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 6000);
                    break;
                    
                case 'override':
                    addTerminalMessage('Emergency override initiated...', true);
                    document.querySelector('.glitch-text').textContent = 'OVERRIDE ACTIVE';
                    let flashCount = 0;
                    const flashInterval = setInterval(() => {
                        const colors = ['invert(1)', 'hue-rotate(180deg)', 'saturate(3)', 'brightness(2)'];
                        document.body.style.filter = colors[flashCount % colors.length];
                        flashCount++;
                        if (flashCount >= 20) {
                            clearInterval(flashInterval);
                            document.body.style.filter = '';
                            addTerminalMessage('Override complete', true);
                            document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                        }
                    }, 200);
                    break;
                    
                case 'trace':
                    addTerminalMessage('Tracing connection...', true);
                    document.querySelector('.glitch-text').textContent = 'TRACING...';
                    const ips = ['203.0.113.42', '198.51.100.7', '192.0.2.146', '????.????.????.????'];
                    ips.forEach((ip, index) => {
                        setTimeout(() => {
                            addTerminalMessage(`Hop ${index + 1}: ${ip}`, true);
                        }, (index + 1) * 800);
                    });
                    setTimeout(() => {
                        addTerminalMessage('Trace complete. Origin masked.', true);
                        document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    }, 4000);
                    break;
                    
                case 'decrypt':
                    addTerminalMessage('Decrypting classified files...', true);
                    document.querySelector('.glitch-text').textContent = 'DECRYPTING...';
                    const progress = [17, 34, 56, 78, 92, 100];
                    progress.forEach((percent, index) => {
                        setTimeout(() => {
                            addTerminalMessage(`Decryption progress: ${percent}%`, true);
                            if (percent === 100) {
                                addTerminalMessage('Files decrypted successfully', true);
                                addTerminalMessage('Warning: Contents classified', true);
                                document.querySelector('.glitch-text').textContent = 'FILES DECRYPTED';
                                setTimeout(() => {
                                    document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                                }, 3000);
                            }
                        }, (index + 1) * 600);
                    });
                    break;
                    
                case 'virus':
                    addTerminalMessage('Deploying digital virus...', true);
                    document.querySelector('.glitch-text').textContent = 'VIRUS DEPLOYED';
                    document.body.style.filter = 'hue-rotate(0deg) saturate(3) brightness(0.8)';
                    document.body.style.animation = 'glitch 0.2s ease-in-out infinite';
                    setTimeout(() => {
                        addTerminalMessage('Antivirus activated. Threat neutralized.', true);
                        document.body.style.filter = '';
                        document.body.style.animation = '';
                        document.querySelector('.glitch-text').textContent = 'VIRUS CONTAINED';
                        setTimeout(() => {
                            document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                        }, 3000);
                    }, 5000);
                    break;
                    
                case 'date':
                    const now = new Date();
                    addTerminalMessage(`${now.toDateString()} ${now.toTimeString()} Matrix Standard Time`, true);
                    break;
                    
                case 'clear':
                    document.getElementById('terminal-output').innerHTML = '';
                    break;
                    
                case 'exit':
                    addTerminalMessage('logout', true);
                    addTerminalMessage('Connection to matrix terminated.', true);
                    setTimeout(() => {
                        addTerminalMessage('Terminal restarted', true);
                    }, 2000);
                    break;
                    
                case '':
                    break;
                    
                default:
                    if (cmd.includes('sudo')) {
                        addTerminalMessage(`[sudo] password for ${currentDirectory.user}: `, true);
                        setTimeout(() => addTerminalMessage('Sorry, access denied. Neural authentication required.', true), 1000);
                    } else {
                        addTerminalMessage(`bash: ${cmd}: command not found`, true);
                        addTerminalMessage('Type "help" for available commands', true);
                    }
            }
        }
        
        // Terminal input handling
        terminalInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') {
                const command = terminalInput.value;
                if (command.trim()) {
                    executeCommand(command);
                }
                terminalInput.value = '';
            }
        });
        
        // Focus terminal input when clicking on terminal
        document.getElementById('terminal').addEventListener('click', () => {
            if (!document.getElementById('game-container')) {
                terminalInput.focus();
            }
        });
        
        // Auto-focus terminal input
        setTimeout(() => {
            terminalInput.focus();
        }, 1000);
        
        // Snake Game
        function createSnakeGame() {
            const existingGame = document.getElementById('game-container');
            if (existingGame) {
                existingGame.remove();
            }
            
            terminalInput.disabled = true;
            terminalInput.style.opacity = '0.5';
            
            let gameRunning = true;
            let gameInterval = null;
            let keyHandler = null;
            
            let snake = [{x: 9, y: 9}];
            let food = {x: 5, y: 5};
            let direction = {x: 0, y: 0};
            let score = 0;
            const gridSize = 18;
            const cellSize = 20;
            
            const gameContainer = document.createElement('div');
            gameContainer.id = 'game-container';
            gameContainer.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                background: rgba(0, 0, 0, 0.95);
                border: 2px solid #00ff00;
                border-radius: 10px;
                z-index: 100;
                padding: 20px;
                text-align: center;
            `;
            
            const scoreDiv = document.createElement('div');
            scoreDiv.style.cssText = `
                color: #00ff00;
                font-family: 'Courier New', monospace;
                font-size: 16px;
                margin-bottom: 10px;
            `;
            
            const canvas = document.createElement('canvas');
            canvas.width = gridSize * cellSize;
            canvas.height = gridSize * cellSize;
            canvas.style.cssText = `
                border: 1px solid #00ff00;
                background: #001100;
                display: block;
            `;
            
            gameContainer.appendChild(scoreDiv);
            gameContainer.appendChild(canvas);
            document.body.appendChild(gameContainer);
            
            const ctx = canvas.getContext('2d');
            
            function updateScore() {
                scoreDiv.textContent = `Score: ${score} | WASD/Arrows to move | ESC to quit`;
            }
            
            function generateFood() {
                do {
                    food.x = Math.floor(Math.random() * gridSize);
                    food.y = Math.floor(Math.random() * gridSize);
                } while (snake.some(segment => segment.x === food.x && segment.y === food.y));
            }
            
            function draw() {
                if (!gameRunning) return;
                
                ctx.fillStyle = '#001100';
                ctx.fillRect(0, 0, canvas.width, canvas.height);
                
                ctx.fillStyle = '#00ff00';
                snake.forEach(segment => {
                    ctx.fillRect(
                        segment.x * cellSize + 1,
                        segment.y * cellSize + 1,
                        cellSize - 2,
                        cellSize - 2
                    );
                });
                
                ctx.fillStyle = '#ff0080';
                ctx.fillRect(
                    food.x * cellSize + 1,
                    food.y * cellSize + 1,
                    cellSize - 2,
                    cellSize - 2
                );
            }
            
            function update() {
                if (!gameRunning) return;
                
                if (direction.x === 0 && direction.y === 0) return;
                
                const head = {
                    x: snake[0].x + direction.x,
                    y: snake[0].y + direction.y
                };
                
                if (head.x < 0 || head.x >= gridSize || head.y < 0 || head.y >= gridSize) {
                    endGame('Hit wall!');
                    return;
                }
                
                if (snake.some(segment => segment.x === head.x && segment.y === head.y)) {
                    endGame('Hit yourself!');
                    return;
                }
                
                snake.unshift(head);
                
                if (head.x === food.x && head.y === food.y) {
                    score += 10;
                    generateFood();
                    updateScore();
                } else {
                    snake.pop();
                }
            }
            
            function gameLoop() {
                if (!gameRunning) return;
                update();
                draw();
            }
            
            function endGame(reason) {
                if (!gameRunning) return;
                
                gameRunning = false;
                
                if (gameInterval) {
                    clearInterval(gameInterval);
                    gameInterval = null;
                }
                
                if (keyHandler) {
                    document.removeEventListener('keydown', keyHandler);
                    keyHandler = null;
                }
                
                addTerminalMessage(`Snake: ${reason} Final score: ${score}`, true);
                document.querySelector('.glitch-text').textContent = 'GAME OVER';
                
                setTimeout(() => {
                    if (gameContainer && gameContainer.parentNode) {
                        gameContainer.remove();
                    }
                    document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                    terminalInput.disabled = false;
                    terminalInput.style.opacity = '1';
                    terminalInput.focus();
                }, 2000);
            }
            
            keyHandler = function(e) {
                e.preventDefault();
                
                if (!gameRunning) return;
                
                if (e.key === 'Escape') {
                    endGame('Game closed');
                    return;
                }
                
                switch(e.key.toLowerCase()) {
                    case 'w':
                    case 'arrowup':
                        if (direction.y !== 1) {
                            direction = {x: 0, y: -1};
                        }
                        break;
                    case 's':
                    case 'arrowdown':
                        if (direction.y !== -1) {
                            direction = {x: 0, y: 1};
                        }
                        break;
                    case 'a':
                    case 'arrowleft':
                        if (direction.x !== 1) {
                            direction = {x: -1, y: 0};
                        }
                        break;
                    case 'd':
                    case 'arrowright':
                        if (direction.x !== -1) {
                            direction = {x: 1, y: 0};
                        }
                        break;
                }
            };
            
            document.addEventListener('keydown', keyHandler);
            
            generateFood();
            updateScore();
            draw();
            
            gameInterval = setInterval(gameLoop, 200);
        }
        
        // Pong Game
        function createPongGame() {
            const existingGame = document.getElementById('game-container');
            if (existingGame) existingGame.remove();
            
            terminalInput.disabled = true;
            terminalInput.style.opacity = '0.5';
            
            const gameContainer = document.createElement('div');
            gameContainer.id = 'game-container';
            gameContainer.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                width: 600px;
                height: 400px;
                background: rgba(0, 0, 0, 0.9);
                border: 2px solid #00ff00;
                border-radius: 10px;
                z-index: 100;
                display: flex;
                flex-direction: column;
                align-items: center;
                padding: 20px;
            `;
            
            const canvas = document.createElement('canvas');
            canvas.width = 560;
            canvas.height = 360;
            canvas.style.border = '1px solid #00ff00';
            canvas.style.backgroundColor = '#001100';
            
            const scoreDiv = document.createElement('div');
            scoreDiv.style.cssText = `
                color: #00ff00;
                font-family: 'Courier New', monospace;
                font-size: 16px;
                margin-bottom: 10px;
            `;
            scoreDiv.textContent = 'Player: 0 | AI: 0 | Use W/S keys | ESC to close';
            
            gameContainer.appendChild(scoreDiv);
            gameContainer.appendChild(canvas);
            document.body.appendChild(gameContainer);
            
            const ctx = canvas.getContext('2d');
            
            const paddle1 = {x: 10, y: 150, width: 10, height: 60, dy: 0};
            const paddle2 = {x: 540, y: 150, width: 10, height: 60, dy: 0};
            const ball = {x: 280, y: 180, dx: 4, dy: 3, size: 8};
            let playerScore = 0, aiScore = 0;
            let gameRunning = true;
            let gameInterval;
            
            function drawPaddle(paddle) {
                ctx.fillStyle = '#00ff00';
                ctx.fillRect(paddle.x, paddle.y, paddle.width, paddle.height);
            }
            
            function drawBall() {
                ctx.fillStyle = '#ff0080';
                ctx.fillRect(ball.x, ball.y, ball.size, ball.size);
            }
            
            function updateBall() {
                ball.x += ball.dx;
                ball.y += ball.dy;
                
                if (ball.y <= 0 || ball.y >= 352) {
                    ball.dy = -ball.dy;
                }
                
                if (ball.x <= 20 && ball.y >= paddle1.y && ball.y <= paddle1.y + 60) {
                    ball.dx = -ball.dx;
                }
                if (ball.x >= 532 && ball.y >= paddle2.y && ball.y <= paddle2.y + 60) {
                    ball.dx = -ball.dx;
                }
                
                if (ball.x < 0) {
                    aiScore++;
                    resetBall();
                }
                if (ball.x > 560) {
                    playerScore++;
                    resetBall();
                }
                
                scoreDiv.textContent = `Player: ${playerScore} | AI: ${aiScore} | Use W/S keys | ESC to close`;
            }
            
            function resetBall() {
                ball.x = 280;
                ball.y = 180;
                ball.dx = (Math.random() > 0.5 ? 1 : -1) * 4;
                ball.dy = (Math.random() - 0.5) * 6;
            }
            
            function updateAI() {
                const ballCenter = ball.y + ball.size / 2;
                const paddleCenter = paddle2.y + paddle2.height / 2;
                
                if (ballCenter < paddleCenter - 10) {
                    paddle2.y -= 3;
                } else if (ballCenter > paddleCenter + 10) {
                    paddle2.y += 3;
                }
                
                paddle2.y = Math.max(0, Math.min(300, paddle2.y));
            }
            
            function closeGame() {
                gameRunning = false;
                if (gameInterval) clearInterval(gameInterval);
                document.removeEventListener('keydown', gameKeyHandler);
                document.removeEventListener('keyup', gameKeyUpHandler);
                if (gameContainer && gameContainer.parentNode) {
                    gameContainer.remove();
                }
                document.querySelector('.glitch-text').textContent = 'SYSTEM BREACH';
                terminalInput.disabled = false;
                terminalInput.style.opacity = '1';
                terminalInput.focus();
            }
            
            function gameLoop() {
                if (!gameRunning) return;
                
                ctx.clearRect(0, 0, 560, 360);
                
                updateBall();
                updateAI();
                
                paddle1.y += paddle1.dy;
                paddle1.y = Math.max(0, Math.min(300, paddle1.y));
                
                drawPaddle(paddle1);
                drawPaddle(paddle2);
                drawBall();
                
                ctx.strokeStyle = '#00ff00';
                ctx.setLineDash([5, 5]);
                ctx.beginPath();
                ctx.moveTo(280, 0);
                ctx.lineTo(280, 360);
                ctx.stroke();
            }
            
            gameInterval = setInterval(gameLoop, 16);
            
            const gameKeyHandler = (e) => {
                e.preventDefault();
                
                if (e.key === 'Escape') {
                    addTerminalMessage('Pong game closed', true);
                    closeGame();
                    return;
                }
                
                switch(e.key.toLowerCase()) {
                    case 'w':
                        paddle1.dy = -4;
                        break;
                    case 's':
                        paddle1.dy = 4;
                        break;
                }
            };
            
            const gameKeyUpHandler = (e) => {
                e.preventDefault();
                
                switch(e.key.toLowerCase()) {
                    case 'w':
                    case 's':
                        paddle1.dy = 0;
                        break;
                }
            };
            
            document.addEventListener('keydown', gameKeyHandler);
            document.addEventListener('keyup', gameKeyUpHandler);
        }
        
        // Floating icons
        function createFloatingIcon() {
            const icons = ['◆', '◈', '◇', '◉', '◎', '●', '○', '◐', '◑', '◒', '◓'];
            const icon = document.createElement('div');
            icon.className = 'floating-icons';
            icon.textContent = icons[Math.floor(Math.random() * icons.length)];
            icon.style.left = Math.random() * (window.innerWidth - 50) + 'px';
            icon.style.top = Math.random() * (window.innerHeight - 50) + 'px';
            icon.style.animationDelay = Math.random() * 2 + 's';
            
            document.body.appendChild(icon);
            
            setTimeout(() => {
                icon.remove();
            }, 8000);
        }
        
        // Random events
        function randomEvent() {
            const reality = document.getElementById('reality');
            const newLevel = Math.max(45, Math.min(99, parseInt(reality.textContent) + (Math.random() - 0.5) * 10));
            reality.textContent = Math.floor(newLevel);
            
            const statuses = ['MONITORING', 'SCANNING', 'ANALYZING', 'PROCESSING', 'COMPUTING'];
            document.getElementById('status').textContent = statuses[Math.floor(Math.random() * statuses.length)];
        }
        
        // Start effects
        setInterval(createMatrixChar, 200);
        setInterval(createFloatingIcon, 3000);
        setInterval(randomEvent, 4000);
        
        // Initial setup
        setTimeout(() => {
            addTerminalMessage('[BOOT] All systems online');
            addTerminalMessage('[TIP] Type "help" to see available commands');
        }, 1000);
    </script>
</body>
</html>
