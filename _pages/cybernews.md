---
title: Cyber News
layout: default
permalink: /cybernews/
---

<style>
.cybernews-container {
    max-width: 1200px;
    margin: 0 auto;
    background: var(--bg-color-dark, #2a2a2a);
    border: 1px solid #444;
    overflow: hidden;
    font-family: 'Courier New', monospace;
    color: var(--txt-color-dark, #e0e0e0);
}

[data-theme="light"] .cybernews-container {
    background: #f8f8f8;
    color: #333;
    border: 1px solid #ddd;
}

.cybernews-header {
    background: #1e1e1e;
    color: #00ff00;
    padding: 8px 15px;
    border-bottom: 1px solid #444;
    font-size: 0.9em;
}

[data-theme="light"] .cybernews-header {
    background: #e0e0e0;
    color: #006600;
    border-bottom: 1px solid #ccc;
}

.cybernews-header h1 {
    font-size: 1.1em;
    margin-bottom: 2px;
    font-weight: normal;
    display: inline;
}

.cybernews-header .subtitle {
    font-size: 0.8em;
    color: #888;
    display: inline;
    margin-left: 10px;
}

.cybernews-header .api-status {
    float: right;
    color: #888;
    font-size: 0.8em;
}

.cybernews-controls {
    padding: 8px 15px;
    background: var(--bg-color-dark, #2a2a2a);
    border-bottom: 1px solid #444;
}

[data-theme="light"] .cybernews-controls {
    background: #f0f0f0;
    border-bottom: 1px solid #ccc;
}

.controls-row {
    display: flex;
    gap: 8px;
    align-items: center;
    justify-content: flex-start;
    flex-wrap: wrap;
    padding: 2px 0;
}

.cyber-btn {
    background: #333;
    color: #ccc;
    border: 1px solid #555;
    padding: 3px 8px;
    border-radius: 2px;
    cursor: pointer;
    font-family: 'Courier New', monospace;
    font-size: 0.8em;
    transition: all 0.2s ease;
    white-space: nowrap;
}

[data-theme="light"] .cyber-btn {
    background: #ddd;
    color: #333;
    border: 1px solid #bbb;
}

.cyber-btn:hover {
    background: #444;
    border-color: #666;
}

[data-theme="light"] .cyber-btn:hover {
    background: #ccc;
    border-color: #999;
}

.cyber-btn.active {
    background: #00ff00 !important;
    color: #000 !important;
    border-color: #00ff00 !important;
}

.refresh-btn {
    background: #333;
    color: #00ff00;
    border: 1px solid #555;
    padding: 3px 8px;
    border-radius: 2px;
    cursor: pointer;
    font-family: 'Courier New', monospace;
    font-size: 0.8em;
    transition: all 0.2s ease;
}

[data-theme="light"] .refresh-btn {
    background: #ddd;
    color: #006600;
    border: 1px solid #bbb;
}

.refresh-btn:hover {
    background: #00ff00;
    color: #000;
}

.cyber-dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-btn {
    background: #333;
    color: #0099ff;
    border: 1px solid #555;
    padding: 3px 8px;
    border-radius: 2px;
    cursor: pointer;
    font-family: 'Courier New', monospace;
    font-size: 0.8em;
    transition: all 0.2s ease;
}

[data-theme="light"] .dropdown-btn {
    background: #ddd;
    color: #0066cc;
    border: 1px solid #bbb;
}

.dropdown-btn:hover {
    background: #444;
    border-color: #666;
}

[data-theme="light"] .dropdown-btn:hover {
    background: #ccc;
    border-color: #999;
}

.dropdown-content {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    background: #333;
    min-width: 180px;
    border: 1px solid #555;
    border-radius: 2px;
    z-index: 1000;
    margin-top: 2px;
}

[data-theme="light"] .dropdown-content {
    background: #fff;
    border: 1px solid #ccc;
}

.cyber-dropdown.open .dropdown-content {
    display: block;
}

.dropdown-item {
    padding: 6px 10px;
    cursor: pointer;
    font-size: 0.8em;
    color: #ccc;
    transition: background 0.2s ease;
    display: flex;
    align-items: center;
    gap: 6px;
}

[data-theme="light"] .dropdown-item {
    color: #333;
}

.dropdown-item:hover {
    background: #444;
}

[data-theme="light"] .dropdown-item:hover {
    background: #f0f0f0;
}

.dropdown-checkbox {
    width: 12px;
    height: 12px;
    border: 1px solid #666;
    background: #222;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 10px;
    color: #00ff00;
}

[data-theme="light"] .dropdown-checkbox {
    background: #fff;
    border: 1px solid #999;
    color: #006600;
}

.loading {
    text-align: center;
    padding: 40px;
    color: #00ff00;
    font-size: 1.2em;
}

[data-theme="light"] .loading {
    color: #006600;
}

.error {
    text-align: center;
    padding: 40px;
    color: #ff6666;
    background: #2a1a1a;
    margin: 20px;
    border: 1px solid #ff6666;
}

[data-theme="light"] .error {
    color: #cc0000;
    background: #ffe0e0;
    border: 1px solid #cc0000;
}

/* Keywords panel - now outside the grid */
.keywords-panel {
    background: #1e1e1e;
    border: 1px solid #444;
    border-radius: 4px;
    margin: 15px;
}

[data-theme="light"] .keywords-panel {
    background: #f0f0f0;
    border: 1px solid #ccc;
}

.keywords-header {
    padding: 8px 12px;
    border-bottom: 1px solid #444;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #2a2a2a;
}

[data-theme="light"] .keywords-header {
    background: #e8e8e8;
    border-bottom: 1px solid #ccc;
}

.keywords-header h3 {
    margin: 0;
    font-size: 0.9em;
    color: #00ff00;
}

[data-theme="light"] .keywords-header h3 {
    color: #006600;
}

.keywords-toggle {
    font-size: 0.8em;
    color: #888;
    transition: transform 0.2s ease;
}

.keywords-toggle.collapsed {
    transform: rotate(-90deg);
}

.keywords-content {
    padding: 10px 12px;
    font-size: 0.8em;
    line-height: 1.4;
    max-height: 200px;
    overflow-y: auto;
}

.keywords-content.collapsed {
    display: none;
}

.keyword-item {
    display: inline-block;
    margin: 2px 4px 2px 0;
    padding: 2px 6px;
    background: #333;
    border: 1px solid #555;
    border-radius: 3px;
    cursor: pointer;
    transition: all 0.2s ease;
    white-space: nowrap;
    font-size: 0.75em;
}

[data-theme="light"] .keyword-item {
    background: #e0e0e0;
    border: 1px solid #bbb;
    color: #333;
}

.keyword-item:hover {
    background: #444;
    border-color: #00ff00;
}

[data-theme="light"] .keyword-item:hover {
    background: #d0d0d0;
    border-color: #006600;
}

.keyword-item.active {
    background: #00ff00;
    color: #000;
    border-color: #00ff00;
}

.keyword-count {
    color: #888;
    font-weight: bold;
}

.filter-status {
    padding: 5px 12px;
    border-top: 1px solid #444;
    background: #1a1a1a;
    font-size: 0.7em;
    color: #00ff00;
    display: none;
}

[data-theme="light"] .filter-status {
    background: #f8f8f8;
    border-top: 1px solid #ccc;
    color: #006600;
}

.filter-status.active {
    display: block;
}

.clear-filter-btn {
    background: #ff4444;
    color: #fff;
    border: 1px solid #ff6666;
    padding: 2px 8px;
    border-radius: 3px;
    cursor: pointer;
    font-family: 'Courier New', monospace;
    font-size: 0.7em;
    transition: all 0.2s ease;
    margin-top: 5px;
}

.clear-filter-btn:hover {
    background: #ff6666;
}

.debug-info {
    background: #1a1a2e;
    border: 1px solid #333;
    padding: 8px;
    margin: 15px;
    font-family: monospace;
    font-size: 0.75em;
    color: #ccc;
    max-height: 180px;
    overflow-y: auto;
    line-height: 1.2;
    display: block;
}

[data-theme="light"] .debug-info {
    background: #f8f8f8;
    border: 1px solid #ddd;
    color: #333;
}

.progress-container {
    margin: 15px;
    background: #333;
    border: 1px solid #555;
    height: 20px;
    border-radius: 4px;
    overflow: hidden;
    position: relative;
}

[data-theme="light"] .progress-container {
    background: #e0e0e0;
    border: 1px solid #ccc;
}

.progress-bar {
    height: 100%;
    background: linear-gradient(90deg, #00ff00, #00cc00);
    width: 0%;
    transition: width 0.3s ease;
    border-radius: 3px;
}

[data-theme="light"] .progress-bar {
    background: linear-gradient(90deg, #006600, #004400);
}

.progress-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 0.75em;
    color: #fff;
    font-family: 'Courier New', monospace;
    font-weight: bold;
    text-shadow: 1px 1px 1px rgba(0,0,0,0.8);
    white-space: nowrap;
}

.info-notice {
    background: #1a2a1a;
    border: 1px solid #555;
    padding: 8px 15px;
    margin: 8px 15px;
    font-size: 0.8em;
    color: #ccc;
    border-left: 3px solid #00ff00;
}

[data-theme="light"] .info-notice {
    background: #f0f8f0;
    border: 1px solid #ddd;
    color: #333;
    border-left: 3px solid #006600;
}

.main-content {
    margin: 0 15px;
}

.stories {
    padding: 0 0 15px 0;
}

.story {
    background: var(--bg-color-dark, #2a2a2a);
    margin: 8px 0;
    padding: 12px;
    border: 1px solid #444;
    transition: all 0.2s ease;
    border-left: 2px solid #666;
}

[data-theme="light"] .story {
    background: #fff;
    border: 1px solid #ddd;
    border-left: 2px solid #999;
}

.story:hover {
    border-left-color: #00ff00;
    background: #2e2e2e;
}

[data-theme="light"] .story:hover {
    border-left-color: #006600;
    background: #f8f8f8;
}

.story.reddit {
    border-left-color: #ff4500;
}

.story.rss-feed {
    border-left-color: #9966cc;
}

.story.hn {
    border-left-color: #ff6600;
}

.story.priority {
    border-left-color: #ff0066;
    background: #2a2a3a;
}

[data-theme="light"] .story.priority {
    background: #fff0f8;
}

.story-title {
    font-size: 1em;
    font-weight: normal;
    color: var(--txt-color-dark, #e0e0e0);
    margin-bottom: 8px;
    line-height: 1.3;
    cursor: pointer;
    transition: color 0.3s ease;
}

[data-theme="light"] .story-title {
    color: #333;
}

.story-title:hover {
    color: #00ff00;
}

[data-theme="light"] .story-title:hover {
    color: #006600;
}

.story-meta {
    display: flex;
    gap: 15px;
    margin-bottom: 8px;
    font-size: 0.8em;
    color: #888;
    flex-wrap: wrap;
}

.meta-item {
    display: flex;
    align-items: center;
    gap: 3px;
}

.meta-item.clickable {
    cursor: pointer;
    transition: color 0.2s ease;
}

.meta-item.clickable:hover {
    color: #00ff00;
}

[data-theme="light"] .meta-item.clickable:hover {
    color: #006600;
}

.source-indicator {
    font-size: 0.7em;
    margin-left: 5px;
    padding: 1px 4px;
    border-radius: 2px;
}

.source-hn {
    background: #ff6600;
    color: #000;
}

.source-reddit {
    background: #ff4500;
    color: #fff;
}

.source-rss {
    background: #9966cc;
    color: #fff;
}

.priority-indicator {
    background: #ff0066;
    color: #fff;
    font-size: 0.6em;
    padding: 1px 3px;
    border-radius: 2px;
    margin-left: 5px;
}

@media (max-width: 768px) {
    /* Fix hamburger menu overflow */
    .cybernews-container {
        width: 100%;
        max-width: 100vw;
        overflow-x: hidden;
    }
    
    /* Mobile button layout - arrange in 2 rows */
    .controls-row {
        justify-content: center;
        gap: 4px;
        flex-direction: row;
        align-items: center;
        flex-wrap: wrap;
    }
    
    /* Create visual separation between button groups */
    .controls-row .refresh-btn,
    .controls-row #debug-btn,
    .controls-row #btn-1d,
    .controls-row #btn-3d,
    .controls-row #btn-7d,
    .controls-row #btn-14d {
        order: 1;
        margin: 2px 1px;
    }
    
    /* Force line break before sources dropdown */
    .controls-row .cyber-dropdown,
    .controls-row span[style*="color: #888"],
    .controls-row #btn-30,
    .controls-row #btn-50,
    .controls-row #pagination-nav {
        order: 2;
        margin: 2px 1px;
    }
    
    /* Add line break between the two groups */
    .controls-row .cyber-dropdown {
        margin-left: 8px;
    }
    
    /* Force wrap after timeframe buttons */
    .controls-row #btn-14d::after {
        content: "";
        flex-basis: 100%;
        height: 0;
    }
    
    /* Smaller buttons on mobile */
    .cyber-btn,
    .refresh-btn,
    .dropdown-btn {
        font-size: 0.7em;
        padding: 2px 6px;
    }
    
    /* Constrain dropdown width */
    .dropdown-content {
        min-width: 160px;
        max-width: 90vw;
        left: 0;
        right: auto;
    }
    
    /* Make sure dropdown doesn't overflow */
    .cyber-dropdown {
        position: relative;
    }
    
    .cyber-dropdown.open .dropdown-content {
        position: absolute;
        z-index: 1000;
    }
    
    .story-meta {
        gap: 6px;
    }
    
    /* Stack story meta on very small screens */
    @media (max-width: 480px) {
        .story-meta {
            flex-direction: column;
            align-items: flex-start;
            gap: 4px;
        }
    }
}

@keyframes spin {
    0% { opacity: 0.3; }
    50% { opacity: 1; }
    100% { opacity: 0.3; }
}
</style>

<div class="cybernews-container">
    <div class="cybernews-header">
        <h1>cybersec/news</h1>
        <span class="subtitle">enhanced reliability v4.2</span>
        <span class="api-status">3-tier + intelligent filtering</span>
    </div>

    <div class="cybernews-controls">
        <div class="controls-row">
            <button class="refresh-btn" onclick="fetchStories()">refresh</button>
            <button class="cyber-btn active" id="debug-btn" onclick="toggleDebug()">hide</button>
            <button class="cyber-btn" id="btn-1d" onclick="setTimeframe(1)">1d</button>
            <button class="cyber-btn active" id="btn-3d" onclick="setTimeframe(3)">3d</button>
            <button class="cyber-btn" id="btn-7d" onclick="setTimeframe(7)">7d</button>
            <button class="cyber-btn" id="btn-14d" onclick="setTimeframe(14)">14d</button>
            
            <div class="cyber-dropdown" id="sources-dropdown">
                <button class="dropdown-btn" onclick="toggleSourcesDropdown()">sources ▼</button>
                <div class="dropdown-content">
                    <div class="dropdown-item" onclick="toggleSource('hackernews')">
                        <div class="dropdown-checkbox" id="check-hackernews">✓</div>
                        <span>hacker news</span>
                    </div>
                    <div class="dropdown-item" onclick="toggleSource('reddit-proxy')">
                        <div class="dropdown-checkbox" id="check-reddit-proxy">✓</div>
                        <span>reddit (proxy)</span>
                    </div>
                    <div class="dropdown-item" onclick="toggleSource('rss-feeds')">
                        <div class="dropdown-checkbox" id="check-rss-feeds">✓</div>
                        <span>rss feeds (25+)</span>
                    </div>
                </div>
            </div>
            
            <span style="color: #888; font-size: 0.8em;">show:</span>
            <button class="cyber-btn active" id="btn-30" onclick="setDisplay(30)">30</button>
            <button class="cyber-btn" id="btn-50" onclick="setDisplay(50)">50</button>
            <div id="pagination-nav" style="display: flex; gap: 5px;"></div>
        </div>
    </div>

    <div class="info-notice">
        <strong>Enhanced Reliability v4.2:</strong> 25+ specialized security RSS feeds → 3-tier proxy fallbacks → Intelligent content filtering. CVE/zero-day priority scoring.
    </div>

    <div id="debug-info" class="debug-info"></div>
    
    <div id="progress-container" class="progress-container" style="display: none;">
        <div id="progress-bar" class="progress-bar"></div>
        <div id="progress-text" class="progress-text">Initializing...</div>
    </div>

    <div class="keywords-panel">
        <div class="keywords-header" onclick="toggleKeywords()">
            <h3>Trending Keywords (from displayed titles)</h3>
            <span class="keywords-toggle" id="keywords-toggle">▼</span>
        </div>
        <div class="keywords-content" id="keywords-content">
            <div id="keywords-list">Loading keywords...</div>
        </div>
        <div class="filter-status" id="filter-status">
            <div id="filter-text"></div>
            <button class="clear-filter-btn" onclick="clearKeywordFilter()">Clear Filter</button>
        </div>
    </div>

    <div class="main-content">
        <div id="content">
            <div class="loading">
                <div style="display: inline-block; animation: spin 1s linear infinite;">3-tier reliability system loading...</div>
            </div>
        </div>
    </div>
</div>

<!-- RSS Parser Library -->
<script src="https://unpkg.com/rss-parser@3.13.0/dist/rss-parser.min.js"></script>

<script>
    // Global state
    let currentTimeframe = 3;
    let debugMode = true;
    let displayPerPage = 30;
    let currentPage = 1;
    let allStories = [];
    let filteredStories = [];
    let debugOutput = '';
    let keywordsExpanded = true;
    let activeKeywordFilter = null;
    let extractedKeywords = {};
    
    // Progress tracking
    let totalOperations = 0;
    let completedOperations = 0;
    
    const sources = {
        hackernews: true,
        'reddit-proxy': true,
        'rss-feeds': true
    };

    // Tier 1: Specialized RSS feeds
    const rssFeeds = {
        bleeping: 'https://www.bleepingcomputer.com/feed/',
        thehackernews: 'https://thehackernews.com/feeds/posts/default',
        darkreading: 'https://www.darkreading.com/rss.xml',
        infosecmag: 'https://www.infosecurity-magazine.com/rss/news/',
        exploitdb: 'https://www.exploit-db.com/rss.xml',
        apisecurity: 'https://apisecurity.io/feed/index.xml',
        f5labs: 'https://www.f5.com/labs/rss-feeds/all.xml',
        cisa: 'https://www.cisa.gov/cybersecurity-advisories/all.xml',
        krebs: 'https://krebsonsecurity.com/feed/',
        securityweek: 'https://www.securityweek.com/feed/',
        cybersecuritynews: 'https://cybersecuritynews.com/feed/',
        securityaffairs: 'https://securityaffairs.co/wordpress/feed',
        hackread: 'https://www.hackread.com/feed/',
        crowdstrike: 'https://www.crowdstrike.com/blog/feed/',
        checkpoint: 'https://blog.checkpoint.com/feed/',
        paloalto: 'https://unit42.paloaltonetworks.com/feed/',
        microsoft_security: 'https://www.microsoft.com/security/blog/feed/',
        google_security: 'https://security.googleblog.com/feeds/posts/default',
        fireeye: 'https://www.mandiant.com/resources/blog/rss.xml',
        securelist: 'https://securelist.com/feed/',
        recorded_future: 'https://www.recordedfuture.com/feed',
        badcyber: 'https://badcyber.com/feed/',
        schneier: 'https://www.schneier.com/blog/atom.xml',
        malwaretech: 'https://www.malwaretech.com/feed',
        cyberscoop: 'https://www.cyberscoop.com/feed/'
    };

    const corsProxies = [
        'https://corsproxy.io/?',
        'https://api.allorigins.win/get?url=',
        'https://thingproxy.freeboard.io/fetch/',
        'https://api.codetabs.com/v1/proxy?quest='
    ];
    
    function log(message) {
        console.log(message);
        const timestamp = new Date().toLocaleTimeString();
        debugOutput += `<div>[${timestamp}] ${message}</div>`;
        const debugDiv = document.getElementById('debug-info');
        if (debugDiv && debugMode) {
            debugDiv.innerHTML = debugOutput;
            debugDiv.scrollTop = debugDiv.scrollHeight;
        }
        updateProgress();
    }
    
    // FIXED: New function that extracts keywords only from the final displayed story titles
    function extractKeywordsFromFinalResults(stories) {
        const keywordCounts = {};
        const stopWords = new Set([
            'the', 'and', 'or', 'but', 'in', 'on', 'at', 'to', 'for', 'of', 'with', 'by', 
            'from', 'up', 'about', 'into', 'through', 'during', 'before', 'after', 'above', 
            'below', 'between', 'among', 'against', 'within', 'without', 'throughout', 'upon',
            'a', 'an', 'is', 'are', 'was', 'were', 'be', 'been', 'being', 'have', 'has', 'had',
            'do', 'does', 'did', 'will', 'would', 'could', 'should', 'may', 'might', 'must',
            'can', 'this', 'that', 'these', 'those', 'i', 'you', 'he', 'she', 'it', 'we', 'they',
            'new', 'now', 'more', 'also', 'just', 'how', 'what', 'when', 'where', 'why', 'who'
        ]);
        
        // Only analyze titles from the final displayed stories
        stories.forEach(story => {
            const titleText = story.title?.toLowerCase() || '';
            
            // Extract CVE patterns from titles only
            const cveMatches = titleText.match(/cve-\d{4}-\d+/g);
            if (cveMatches) {
                cveMatches.forEach(cve => {
                    const normalizedCVE = cve.toUpperCase();
                    keywordCounts[normalizedCVE] = (keywordCounts[normalizedCVE] || 0) + 1;
                });
            }
            
            // Extract security-relevant terms from titles only
            const words = titleText.match(/\b[a-zA-Z]+\b/g) || [];
            words.forEach(word => {
                const cleanWord = word.toLowerCase().trim();
                if (stopWords.has(cleanWord) || cleanWord.length < 3) return;
                
                // Focus on security terms and company names
                const securityTerms = [
                    'whatsapp', 'telegram', 'microsoft', 'google', 'apple', 'meta', 'facebook',
                    'security', 'vulnerability', 'exploit', 'malware', 'ransomware', 'phishing', 'breach',
                    'attack', 'hack', 'cyber', 'threat', 'patch', 'critical', 'zero-day', 'apt',
                    'cisa', 'china', 'russia', 'iran', 'android', 'ios', 'windows', 'linux',
                    'bitcoin', 'cryptocurrency', 'api', 'database', 'cloud', 'aws', 'azure',
                    'chrome', 'firefox', 'safari', 'edge', 'github', 'docker', 'kubernetes',
                    'nvidia', 'intel', 'amd', 'cisco', 'zoom', 'slack', 'teams', 'discord'
                ];
                
                if (securityTerms.includes(cleanWord)) {
                    keywordCounts[cleanWord] = (keywordCounts[cleanWord] || 0) + 1;
                }
            });
        });
        
        // Filter and sort keywords - only show keywords that appear at least once
        return Object.entries(keywordCounts)
            .filter(([word, count]) => count >= 1)
            .sort((a, b) => b[1] - a[1])
            .slice(0, 20)
            .reduce((obj, [word, count]) => {
                obj[word] = count;
                return obj;
            }, {});
    }
    
    // FIXED: Simplified function that only regenerates keywords when filtering
    function updateKeywordsFromVisibleStories() {
        // For filtering, re-extract from the stories being shown
        const storiesToAnalyze = activeKeywordFilter ? filteredStories : allStories;
        
        if (storiesToAnalyze.length === 0) {
            // Don't clear keywords if we have no stories to show
            updateKeywordsDisplay();
            return;
        }
        
        // Only regenerate keywords if we're filtering, otherwise keep the original keywords from the 150 stories
        if (activeKeywordFilter) {
            extractedKeywords = extractKeywordsFromFinalResults(storiesToAnalyze);
            log(`Keywords updated for filtered view: ${storiesToAnalyze.length} stories`);
        }
        
        updateKeywordsDisplay();
    }
    
    function updateKeywordsDisplay() {
        const keywordsList = document.getElementById('keywords-list');
        if (!keywordsList) return;
        
        if (Object.keys(extractedKeywords).length === 0) {
            keywordsList.innerHTML = '<span style="color: #888;">No keywords found</span>';
            return;
        }
        
        const keywordItems = Object.entries(extractedKeywords).map(([keyword, count]) => {
            const isActive = activeKeywordFilter === keyword;
            const activeClass = isActive ? ' active' : '';
            return `<span class="keyword-item${activeClass}" onclick="filterByKeyword('${keyword}')">${keyword} <span class="keyword-count">(${count})</span></span>`;
        }).join('');
        
        keywordsList.innerHTML = keywordItems;
        log(`Keywords panel updated with ${Object.keys(extractedKeywords).length} trending terms from displayed titles`);
    }
    
    function toggleKeywords() {
        keywordsExpanded = !keywordsExpanded;
        const content = document.getElementById('keywords-content');
        const toggle = document.getElementById('keywords-toggle');
        
        if (keywordsExpanded) {
            content.classList.remove('collapsed');
            toggle.classList.remove('collapsed');
            toggle.textContent = '▼';
        } else {
            content.classList.add('collapsed');
            toggle.classList.add('collapsed');
            toggle.textContent = '▶';
        }
    }
    
    function filterByKeyword(keyword) {
        if (activeKeywordFilter === keyword) {
            clearKeywordFilter();
            return;
        }
        
        activeKeywordFilter = keyword;
        // Filter based on title only, not description
        filteredStories = allStories.filter(story => {
            const titleText = story.title?.toLowerCase() || '';
            return titleText.includes(keyword.toLowerCase());
        });
        
        currentPage = 1;
        updateKeywordsFromVisibleStories();
        displayStories();
        
        // Show filter status
        const filterStatus = document.getElementById('filter-status');
        const filterText = document.getElementById('filter-text');
        filterStatus.classList.add('active');
        filterText.textContent = `Filtering by "${keyword}" in titles - ${filteredStories.length} stories`;
        
        log(`Applied title filter: "${keyword}" - ${filteredStories.length} matching stories`);
    }
    
    function clearKeywordFilter() {
        activeKeywordFilter = null;
        filteredStories = [];
        currentPage = 1;
        
        // Reset keywords back to the original 150-story keywords
        extractedKeywords = extractKeywordsFromFinalResults(allStories);
        updateKeywordsDisplay();
        displayStories();
        
        const filterStatus = document.getElementById('filter-status');
        filterStatus.classList.remove('active');
        
        log('Cleared keyword filter - restored original keywords from 150 stories');
    }
    
    function updateProgress(customText = null) {
        const progressContainer = document.getElementById('progress-container');
        const progressBar = document.getElementById('progress-bar');
        const progressText = document.getElementById('progress-text');
        
        if (!progressContainer || !progressBar || !progressText) return;
        
        if (totalOperations === 0) {
            progressContainer.style.display = 'none';
            return;
        }
        
        const percentage = Math.min(100, (completedOperations / totalOperations) * 100);
        progressBar.style.width = percentage + '%';
        
        if (customText) {
            progressText.textContent = customText;
        } else if (percentage === 100) {
            progressText.textContent = 'Complete!';
        } else {
            progressText.textContent = `${Math.round(percentage)}% - ${completedOperations}/${totalOperations} operations`;
        }
        
        if (totalOperations > 0 && progressContainer.style.display === 'none') {
            progressContainer.style.display = 'block';
        }
        
        if (percentage >= 100) {
            setTimeout(() => {
                if (progressContainer) {
                    progressContainer.style.display = 'none';
                }
            }, 1500);
        }
    }
    
    function initializeProgress(total, text = 'Starting...') {
        totalOperations = total;
        completedOperations = 0;
        updateProgress(text);
    }
    
    function incrementProgress(text = null) {
        completedOperations++;
        updateProgress(text);
    }
    
    function resetProgress() {
        totalOperations = 0;
        completedOperations = 0;
        const progressContainer = document.getElementById('progress-container');
        if (progressContainer) {
            progressContainer.style.display = 'none';
        }
    }
    
    async function fetchWithTimeout(fetchFunction, timeoutMs = 15000) {
        return Promise.race([
            fetchFunction(),
            new Promise((_, reject) => 
                setTimeout(() => reject(new Error('Request timeout')), timeoutMs)
            )
        ]).catch(error => {
            log(`Error: ${error.message}`);
            return [];
        });
    }
    
    function updateButtons() {
        document.querySelectorAll('.cyber-btn').forEach(btn => btn.classList.remove('active'));
        
        const timeframeBtnId = currentTimeframe === 1 ? 'btn-1d' :
                             currentTimeframe === 3 ? 'btn-3d' :
                             currentTimeframe === 7 ? 'btn-7d' :
                             currentTimeframe === 14 ? 'btn-14d' : 'btn-3d';
        document.getElementById(timeframeBtnId).classList.add('active');
        
        document.getElementById(`btn-${displayPerPage}`).classList.add('active');
        
        const debugBtn = document.getElementById('debug-btn');
        debugBtn.textContent = debugMode ? 'hide' : 'debug';
        if (debugMode) debugBtn.classList.add('active');
        
        Object.keys(sources).forEach(source => {
            const cb = document.getElementById(`check-${source}`);
            if (cb) cb.textContent = sources[source] ? '✓' : '';
        });
        
        const debugDiv = document.getElementById('debug-info');
        if (debugDiv) {
            debugDiv.style.display = debugMode ? 'block' : 'none';
            if (debugMode) debugDiv.innerHTML = debugOutput;
        }
    }

    async function fetchRSSWithEnhancedFallback(feedUrl, sourceName) {
        const parser = new RSSParser({
            headers: {
                'User-Agent': 'Mozilla/5.0 (compatible; RSS Reader)',
            }
        });
        
        for (let i = 0; i < corsProxies.length; i++) {
            const proxy = corsProxies[i];
            try {
                log(`${sourceName}: trying proxy ${i + 1}/${corsProxies.length}`);
                
                let proxyUrl;
                if (proxy.includes('allorigins')) {
                    proxyUrl = proxy + encodeURIComponent(feedUrl);
                } else if (proxy.includes('corsproxy.io')) {
                    proxyUrl = proxy + encodeURIComponent(feedUrl);  
                } else {
                    proxyUrl = proxy + feedUrl;
                }
                
                let feedData;
                if (proxy.includes('allorigins')) {
                    const response = await fetch(proxyUrl);
                    if (response.ok) {
                        const data = await response.json();
                        if (data.contents) {
                            feedData = await parser.parseString(data.contents);
                        }
                    }
                } else {
                    feedData = await parser.parseURL(proxyUrl);
                }
                
                if (feedData && feedData.items && feedData.items.length > 0) {
                    const stories = feedData.items.map((item, index) => ({
                        objectID: `rss_${sourceName}_${index}_${Date.now()}`,
                        title: item.title,
                        author: sourceName,
                        points: Math.floor(Math.random() * 50) + 25,
                        num_comments: 0,
                        created_at: item.pubDate || item.isoDate || new Date().toISOString(),
                        url: item.link,
                        description: item.contentSnippet || item.content || '',
                        source: 'rss',
                        rss_source: sourceName
                    })).filter(story => story.title && story.url);
                    
                    log(`${sourceName}: proxy ${i + 1} succeeded with ${stories.length} stories`);
                    return stories;
                }
                
            } catch (error) {
                log(`${sourceName}: proxy ${i + 1} failed - ${error.message}`);
            }
            
            await new Promise(r => setTimeout(r, 300));
        }
        
        log(`${sourceName}: all proxy methods failed`);
        return [];
    }

    async function fetchAllRSSFeeds() {
        if (!sources['rss-feeds']) return [];
        
        log('TIER 1: Fetching RSS feeds with enhanced proxy fallbacks');
        let allRSSStories = [];
        
        const feedEntries = Object.entries(rssFeeds);
        const batchSize = 4;
        
        for (let i = 0; i < feedEntries.length; i += batchSize) {
            const batch = feedEntries.slice(i, i + batchSize);
            log(`Processing batch ${Math.floor(i/batchSize) + 1}/${Math.ceil(feedEntries.length/batchSize)}`);
            
            const batchPromises = batch.map(([feedName, feedUrl]) => 
                fetchWithTimeout(() => fetchRSSWithEnhancedFallback(feedUrl, feedName), 20000)
            );
            
            const batchResults = await Promise.all(batchPromises);
            batchResults.forEach(stories => {
                allRSSStories = allRSSStories.concat(stories);
            });
            
            incrementProgress(`RSS batch ${Math.floor(i/batchSize) + 1} complete`);
            await new Promise(r => setTimeout(r, 800));
        }
        
        log(`TIER 1 complete: ${allRSSStories.length} stories from RSS feeds`);
        return allRSSStories;
    }

    async function fetchRedditViaProxy() {
        if (!sources['reddit-proxy']) return [];
        
        log('TIER 2: Fetching Reddit via proxy');
        const subreddits = ['cybersecurity', 'netsec'];
        let allStories = [];
        
        for (const sub of subreddits) {
            const workingProxies = ['https://corsproxy.io/?', 'https://api.allorigins.win/get?url='];
            
            for (const proxy of workingProxies) {
                try {
                    const url = `${proxy}${encodeURIComponent(`https://www.reddit.com/r/${sub}/hot.json?limit=25`)}`;
                    const response = await fetch(url);
                    
                    if (response.ok) {
                        let data;
                        if (proxy.includes('allorigins')) {
                            const json = await response.json();
                            data = JSON.parse(json.contents);
                        } else {
                            data = await response.json();
                        }
                        
                        const posts = data.data?.children || [];
                        const now = new Date();
                        const cutoff = new Date(now.getTime() - (currentTimeframe * 24 * 60 * 60 * 1000));
                        
                        const stories = posts.filter(post => {
                            const p = post.data;
                            const createdDate = new Date(p.created_utc * 1000);
                            return createdDate >= cutoff && 
                                   p.url && 
                                   !p.url.includes('reddit.com/r/') && 
                                   p.score >= 10;
                        }).map(post => {
                            const p = post.data;
                            return {
                                objectID: `reddit_${p.id}`,
                                title: p.title,
                                author: `u/${p.author}`,
                                points: p.score,
                                num_comments: p.num_comments,
                                created_at: new Date(p.created_utc * 1000).toISOString(),
                                url: p.url,
                                reddit_url: `https://reddit.com${p.permalink}`,
                                source: 'reddit',
                                subreddit: sub
                            };
                        });
                        
                        allStories = allStories.concat(stories);
                        log(`Reddit r/${sub}: ${stories.length} stories`);
                        break;
                    }
                } catch (error) {
                    log(`Reddit r/${sub} failed: ${error.message}`);
                }
            }
            
            incrementProgress(`Reddit r/${sub} complete`);
            await new Promise(r => setTimeout(r, 600));
        }
        
        log(`TIER 2 complete: ${allStories.length} stories from Reddit`);
        return allStories;
    }
    
    async function fetchHackerNewsSimple() {
        if (!sources.hackernews) return [];
        
        log('TIER 3: Fetching Hacker News');
        try {
            const now = new Date();
            const cutoff = new Date(now.getTime() - (currentTimeframe * 24 * 60 * 60 * 1000));
            const timestamp = Math.floor(cutoff.getTime() / 1000);
            
            const queries = ['security', 'vulnerability', 'WhatsApp', 'cybersecurity', 'breach', 'malware'];
            let stories = [];
            
            for (let i = 0; i < queries.length; i++) {
                const query = queries[i];
                try {
                    const url = `https://hn.algolia.com/api/v1/search?query=${encodeURIComponent(query)}&tags=story&hitsPerPage=15&numericFilters=created_at_i>${timestamp}`;
                    const response = await fetch(url);
                    
                    if (response.ok) {
                        const data = await response.json();
                        stories = stories.concat(data.hits.map(hit => ({ ...hit, source: 'hackernews' })));
                        log(`HN "${query}": ${data.hits.length} results`);
                    }
                } catch (e) {
                    log(`HN query "${query}" failed: ${e.message}`);
                }
                
                incrementProgress(`HN query "${query}" complete`);
                await new Promise(r => setTimeout(r, 400));
            }
            
            log(`TIER 3 complete: ${stories.length} stories from Hacker News`);
            return stories;
            
        } catch (error) {
            log(`HN error: ${error.message}`);
            return [];
        }
    }
    
    function isRelevantCybersecStory(story) {
        const title = story.title?.toLowerCase() || '';
        const description = story.description?.toLowerCase() || '';
        const text = title + ' ' + description;
        
        const priorityKeywords = [
            'cve-202', 'cve-201', 'zero-day', '0-day', 'vulnerability', 'exploit',
            'critical security', 'security patch', 'emergency update', 'zero click',
            'whatsapp', 'ransomware', 'malware', 'spyware', 'backdoor', 'rootkit',
            'trojan', 'botnet', 'apt ', 'advanced persistent', 'supply chain attack',
            'data breach', 'cisa alert', 'security incident', 'cyber attack',
            'threat actor', 'nation state', 'security advisory'
        ];
        
        if (priorityKeywords.some(word => text.includes(word))) {
            return true;
        }
        
        const strongExclude = [
            'sports', 'weather', 'cooking', 'travel', 'music', 'movie', 'entertainment',
            'fashion', 'celebrity', 'immigration', 'election', 'politics', 'climate',
            'economy', 'stock market', 'oil price', 'interest rate', 'unemployment'
        ];
        
        if (strongExclude.some(word => text.includes(word))) {
            return false;
        }
        
        if (story.source === 'rss') {
            const highTrustSources = [
                'bleeping', 'krebs', 'securityweek', 'cybersecuritynews',
                'infosecmag', 'darkreading', 'thehackernews', 'securityaffairs',
                'hackread', 'cisa', 'exploitdb', 'apisecurity', 'f5labs',
                'crowdstrike', 'checkpoint', 'paloalto', 'microsoft_security',
                'google_security', 'fireeye', 'securelist', 'recorded_future',
                'malwaretech', 'schneier', 'badcyber'
            ];
            
            if (highTrustSources.some(source => story.rss_source?.includes(source))) {
                return true;
            }
        }
        
        const include = [
            'cyber', 'security', 'hack', 'breach', 'threat', 'attack', 'phishing',
            'privacy', 'encryption', 'surveillance', 'incident', 'forensics',
            'pentest', 'firewall', 'antivirus', 'endpoint', 'siem', 'soc',
            'authentication', 'authorization', 'compliance', 'gdpr', 'hipaa'
        ];
        
        return include.some(word => text.includes(word));
    }
    
    async function fetchStories() {
        const contentDiv = document.getElementById('content');
        debugOutput = '';
        resetProgress();
        
        log('Enhanced Reliability v4.2 starting...');
        log(`3-Tier Stack: RSS Feeds → Reddit → HN`);
        log(`Config: ${currentTimeframe}d timeframe, ${displayPerPage} per page`);
        
        let totalOps = 0;
        if (sources['rss-feeds']) {
            totalOps += Math.ceil(Object.keys(rssFeeds).length / 4);
        }
        if (sources['reddit-proxy']) {
            totalOps += 2;
        }
        if (sources.hackernews) {
            totalOps += 6;
        }
        totalOps += 5; // Processing stages + keyword extraction
        
        initializeProgress(totalOps, 'Initializing 3-tier system...');
        
        contentDiv.innerHTML = '<div class="loading"><div style="animation: spin 1s linear infinite;">3-tier reliability system loading...</div></div>';
        
        try {
            let all = [];
            
            const rssStories = await fetchWithTimeout(fetchAllRSSFeeds, 60000);
            all = all.concat(rssStories);
            log(`TIER 1 summary: ${rssStories.length} stories`);
            
            const reddit = await fetchWithTimeout(fetchRedditViaProxy, 20000);
            all = all.concat(reddit);
            log(`TIER 2 summary: ${reddit.length} stories`);
            
            const hn = await fetchWithTimeout(fetchHackerNewsSimple, 15000);
            all = all.concat(hn);
            log(`TIER 3 summary: ${hn.length} stories`);
            
            log(`=== TOTAL COLLECTED: ${all.length} stories ===`);
            incrementProgress('Processing: Time filtering...');
            
            const now = new Date();
            const cutoff = new Date(now.getTime() - (currentTimeframe * 24 * 60 * 60 * 1000));
            
            const timeFiltered = all.filter(story => {
                if (!story.created_at) return true;
                const storyDate = new Date(story.created_at);
                return storyDate >= cutoff || isNaN(storyDate.getTime());
            });
            
            log(`After time filtering: ${timeFiltered.length} stories`);
            incrementProgress('Processing: Deduplication...');
            
            const unique = [];
            const seen = new Set();
            timeFiltered.forEach(story => {
                const titleKey = story.title?.toLowerCase().replace(/[^\w\s]/g, '').substring(0, 70);
                const urlKey = story.url?.replace(/^https?:\/\/(www\.)?/, '').toLowerCase();
                const key = `${titleKey}|${urlKey}`;
                
                if (key && !seen.has(key) && story.title && story.url) {
                    seen.add(key);
                    unique.push(story);
                }
            });
            
            log(`After deduplication: ${unique.length} stories`);
            incrementProgress('Processing: Content filtering...');
            
            const filtered = unique.filter(isRelevantCybersecStory);
            log(`After cybersecurity filtering: ${filtered.length} stories`);
            
            incrementProgress('Processing: Ranking & scoring...');
            
            allStories = filtered
                .map(story => {
                    let sourceMultiplier = 1;
                    let contentBonus = 0;
                    
                    if (story.source === 'rss') sourceMultiplier = 1.8;
                    else if (story.source === 'hackernews') sourceMultiplier = 1.3;
                    else if (story.source === 'reddit') sourceMultiplier = 1.1;
                    
                    const title = story.title?.toLowerCase() || '';
                    const desc = story.description?.toLowerCase() || '';
                    const text = title + ' ' + desc;
                    
                    if (text.includes('cve-202') || text.includes('zero-day') || text.includes('0-day')) {
                        contentBonus += 50;
                    }
                    if (text.includes('critical') && text.includes('vulnerability')) {
                        contentBonus += 30;
                    }
                    if (text.includes('whatsapp') || text.includes('telegram') || text.includes('signal')) {
                        contentBonus += 25;
                    }
                    if (text.includes('ransomware') || text.includes('apt ') || text.includes('nation state')) {
                        contentBonus += 20;
                    }
                    if (text.includes('data breach') || text.includes('security incident')) {
                        contentBonus += 15;
                    }
                    
                    const recencyScore = (new Date(story.created_at).getTime() / 1000000);
                    const totalScore = ((story.points || 0) * sourceMultiplier) + contentBonus + recencyScore;
                    
                    return { ...story, totalScore, contentBonus, sourceMultiplier };
                })
                .sort((a, b) => b.totalScore - a.totalScore)
                .slice(0, 150);
            
            log(`=== FINAL RANKED SET: ${allStories.length} stories ===`);
            
            // Clear any previous filter state
            activeKeywordFilter = null;
            filteredStories = [];
            
            // FIXED: NOW extract keywords from the final 150 displayed stories ONLY
            incrementProgress('Processing: Extracting trending keywords from final results...');
            extractedKeywords = extractKeywordsFromFinalResults(allStories);
            
            log(`=== EXTRACTED ${Object.keys(extractedKeywords).length} TRENDING KEYWORDS FROM ${allStories.length} FINAL STORIES ===`);
            
            if (debugMode && allStories.length > 0) {
                log("=== TOP 15 STORIES ===");
                allStories.slice(0, 15).forEach((story, i) => {
                    const sourceDisplay = story.source === 'rss' ? `RSS-${story.rss_source}` : story.source;
                    const bonusInfo = story.contentBonus > 0 ? ` +${story.contentBonus}bonus` : '';
                    log(`${i + 1}. [${sourceDisplay}] "${story.title.substring(0, 80)}..." (${story.points}pts, x${story.sourceMultiplier?.toFixed(1)}${bonusInfo})`);
                });
                
                const priorityStories = allStories.filter(story => {
                    const text = (story.title + ' ' + story.description).toLowerCase();
                    return text.includes('cve-202') || text.includes('zero-day') || 
                           text.includes('whatsapp') || text.includes('critical') ||
                           text.includes('ransomware') || text.includes('breach');
                });
                
                if (priorityStories.length > 0) {
                    log(`🎯 FOUND ${priorityStories.length} HIGH-PRIORITY SECURITY STORIES!`);
                    priorityStories.slice(0, 10).forEach((story, i) => {
                        const source = story.source === 'rss' ? story.rss_source : story.source;
                        log(`  ${i + 1}. [${source}] "${story.title.substring(0, 85)}"`);
                    });
                } else {
                    log("ℹ️ No high-priority CVE/zero-day/breach stories found in this fetch");
                }
            }
            
            updateProgress('Complete! Displaying results...');
            displayStories();
            
        } catch (error) {
            log(`Fatal error: ${error.message}`);
            resetProgress();
            displayError();
        }
    }
    
    function displayStories() {
        const contentDiv = document.getElementById('content');
        const storiesToShow = activeKeywordFilter ? filteredStories : allStories;
        
        if (storiesToShow.length === 0) {
            contentDiv.innerHTML = '<div class="error"><h3>No cybersecurity stories found</h3><p>Try refresh or different timeframe. Check debug for details.</p></div>';
            return;
        }
        
        const totalPages = Math.ceil(storiesToShow.length / displayPerPage);
        const start = (currentPage - 1) * displayPerPage;
        const currentStories = storiesToShow.slice(start, start + displayPerPage);
        
        let paginationHTML = '';
        if (totalPages > 1) {
            paginationHTML = `<span style="color: #888; font-size: 0.8em;">${currentPage}/${totalPages}</span>`;
            if (currentPage > 1) paginationHTML += `<button class="cyber-btn" onclick="changePage(${currentPage - 1})" style="padding: 2px 6px; font-size: 0.8em;"><</button>`;
            if (currentPage < totalPages) paginationHTML += `<button class="cyber-btn" onclick="changePage(${currentPage + 1})" style="padding: 2px 6px; font-size: 0.8em;">></button>`;
        }
        document.getElementById('pagination-nav').innerHTML = paginationHTML;
        
        const storiesHTML = currentStories.map((story, i) => {
            const num = start + i + 1;
            const date = new Date(story.created_at).toLocaleDateString();
            const domain = story.url ? new URL(story.url).hostname : 'unknown';
            
            let sourceLabel, sourceCss;
            if (story.source === 'reddit') {
                sourceLabel = 'r';
                sourceCss = 'reddit';
            } else if (story.source === 'hackernews') {
                sourceLabel = 'hn';
                sourceCss = 'hn';
            } else if (story.source === 'rss') {
                sourceLabel = story.rss_source?.substring(0, 8) || 'rss';
                sourceCss = 'rss';
            } else {
                sourceLabel = 'feed';
                sourceCss = 'rss';
            }
            
            const isPriority = story.contentBonus >= 20;
            const priorityClass = isPriority ? ' priority' : '';
            const priorityIndicator = isPriority ? '<span class="priority-indicator">HIGH</span>' : '';
            
            const commentsUrl = story.reddit_url || 
                              (story.source === 'hackernews' ? `https://news.ycombinator.com/item?id=${story.objectID}` : story.url);
            
            return `
                <div class="story ${sourceCss}${priorityClass}">
                    <div style="font-size: 0.8em; color: #666; margin-bottom: 5px;">
                        ${num}. <span class="source-indicator source-${sourceCss}">${sourceLabel}</span>${priorityIndicator}
                    </div>
                    <div class="story-title" onclick="window.open('${story.url}', '_blank')">
                        ${story.title}
                    </div>
                    <div class="story-meta">
                        <div class="meta-item"><span>${story.author}</span></div>
                        <div class="meta-item"><span>${story.points}pts</span></div>
                        ${story.contentBonus > 0 ? `<div class="meta-item"><span style="color: #00ff00;">+${story.contentBonus}</span></div>` : ''}
                        ${story.num_comments > 0 ? `<div class="meta-item clickable" onclick="window.open('${commentsUrl}', '_blank')"><span>${story.num_comments} comments</span></div>` : ''}
                        <div class="meta-item"><span>${date}</span></div>
                        <div class="meta-item"><span style="color: #666;">${domain}</span></div>
                    </div>
                </div>
            `;
        }).join('');
        
        contentDiv.innerHTML = `<div class="stories">${storiesHTML}</div>`;
        
        // Update keywords display after stories are shown
        updateKeywordsFromVisibleStories();
    }
    
    function displayError() {
        document.getElementById('content').innerHTML = '<div class="error"><h3>Error loading stories</h3><p>Check debug info and try refresh.</p><button onclick="fetchStories()" class="cyber-btn">retry</button></div>';
    }
    
    function changePage(page) {
        currentPage = page;
        displayStories();
    }
    
    function setTimeframe(days) {
        currentTimeframe = days;
        currentPage = 1;
        activeKeywordFilter = null;
        filteredStories = [];
        updateButtons();
        fetchStories();
    }
    
    function setDisplay(count) {
        displayPerPage = count;
        currentPage = 1;
        updateButtons();
        displayStories();
    }
    
    function toggleDebug() {
        debugMode = !debugMode;
        updateButtons();
    }
    
    function toggleSourcesDropdown() {
        document.getElementById('sources-dropdown').classList.toggle('open');
    }
    
    function toggleSource(source) {
        sources[source] = !sources[source];
        currentPage = 1;
        activeKeywordFilter = null;
        filteredStories = [];
        updateButtons();
        fetchStories();
    }
    
    document.addEventListener('click', (e) => {
        if (!e.target.closest('.cyber-dropdown')) {
            document.querySelectorAll('.cyber-dropdown').forEach(d => d.classList.remove('open'));
        }
    });
    
    window.addEventListener('load', () => {
        log('Enhanced Reliability v4.2 loaded');
        log('3-Tier Stack: RSS Feeds → Reddit → HN');
        updateButtons();
        
        setTimeout(() => {
            fetchStories();
        }, 1000);
    });
</script>
