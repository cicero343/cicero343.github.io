---
title: Cyber News
layout: default
permalink: /cybernews/
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cybersecurity News - Enhanced Reliability v4.0</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Courier New', monospace;
            background: #1a1a1a;
            color: #e0e0e0;
            min-height: 100vh;
            padding: 10px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: #2a2a2a;
            border: 1px solid #444;
            overflow: hidden;
        }

        .header {
            background: #1e1e1e;
            color: #00ff00;
            padding: 8px 15px;
            border-bottom: 1px solid #444;
            font-size: 0.9em;
        }

        .header h1 {
            font-size: 1.1em;
            margin-bottom: 2px;
            font-weight: normal;
            display: inline;
        }

        .header .subtitle {
            font-size: 0.8em;
            color: #888;
            display: inline;
            margin-left: 10px;
        }

        .header .api-status {
            float: right;
            color: #888;
            font-size: 0.8em;
        }

        .controls {
            padding: 8px 15px;
            background: #2a2a2a;
            border-bottom: 1px solid #444;
        }

        .controls-row {
            display: flex;
            gap: 8px;
            align-items: center;
            justify-content: flex-start;
            flex-wrap: wrap;
            padding: 2px 0;
        }

        .btn {
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

        .btn:hover {
            background: #444;
            border-color: #666;
        }

        .btn.active {
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

        .refresh-btn:hover {
            background: #00ff00;
            color: #000;
        }

        .dropdown {
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

        .dropdown-btn:hover {
            background: #444;
            border-color: #666;
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

        .dropdown.open .dropdown-content {
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

        .dropdown-item:hover {
            background: #444;
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

        .loading {
            text-align: center;
            padding: 40px;
            color: #00ff00;
            font-size: 1.2em;
        }

        .error {
            text-align: center;
            padding: 40px;
            color: #ff6666;
            background: #2a1a1a;
            margin: 20px;
            border: 1px solid #ff6666;
        }

        .debug-info {
            background: #1a1a2e;
            border: 1px solid #333;
            padding: 8px;
            margin: 0 15px;
            font-family: monospace;
            font-size: 0.75em;
            color: #ccc;
            max-height: 180px;
            overflow-y: auto;
            line-height: 1.2;
            display: block;
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

        .stories {
            padding: 0 15px 15px;
        }

        .story {
            background: #2a2a2a;
            margin: 8px 0;
            padding: 12px;
            border: 1px solid #444;
            transition: all 0.2s ease;
            border-left: 2px solid #666;
        }

        .story:hover {
            border-left-color: #00ff00;
            background: #2e2e2e;
        }

        .story.reddit {
            border-left-color: #ff4500;
        }

        .story.direct-rss {
            border-left-color: #00ff00;
        }

        .story.rss-feed {
            border-left-color: #9966cc;
        }

        .story.hn {
            border-left-color: #ff6600;
        }

        .story-title {
            font-size: 1em;
            font-weight: normal;
            color: #e0e0e0;
            margin-bottom: 8px;
            line-height: 1.3;
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .story-title:hover {
            color: #00ff00;
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

        .source-direct {
            background: #00ff00;
            color: #000;
        }

        @media (max-width: 768px) {
            .controls-row {
                justify-content: center !important;
                gap: 5px;
            }
            .story-meta {
                gap: 8px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>cybersec/news</h1>
            <span class="subtitle">enhanced reliability v4.0</span>
            <span class="api-status">4-tier reliability stack</span>
        </div>

        <div class="controls">
            <div class="controls-row">
                <button class="refresh-btn" onclick="fetchStories()">refresh</button>
                <button class="btn active" id="debug-btn" onclick="toggleDebug()">hide</button>
                <button class="btn" id="btn-1d" onclick="setTimeframe(1)">1d</button>
                <button class="btn active" id="btn-3d" onclick="setTimeframe(3)">3d</button>
                <button class="btn" id="btn-7d" onclick="setTimeframe(7)">7d</button>
                <button class="btn" id="btn-14d" onclick="setTimeframe(14)">14d</button>
                
                <div class="dropdown" id="sources-dropdown">
                    <button class="dropdown-btn" onclick="toggleSourcesDropdown()">sources ▼</button>
                    <div class="dropdown-content">
                        <div class="dropdown-item" onclick="toggleSource('direct-cors')">
                            <div class="dropdown-checkbox" id="check-direct-cors">✓</div>
                            <span>direct cors feeds</span>
                        </div>
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
                            <span>rss feeds (15+)</span>
                        </div>
                    </div>
                </div>
                
                <span style="color: #888; font-size: 0.8em; margin-left: 8px;">show:</span>
                <button class="btn active" id="btn-30" onclick="setDisplay(30)">30</button>
                <button class="btn" id="btn-50" onclick="setDisplay(50)">50</button>
                <div id="pagination-nav" style="display: flex; gap: 5px; margin-left: 8px;"></div>
            </div>
        </div>

        <div class="info-notice">
            <strong>Enhanced Reliability v4.0:</strong> Direct CORS-enabled RSS → Professional RSS services → 4-tier CORS proxy fallbacks. No API keys required - all free/public endpoints.
        </div>

        <div id="debug-info" class="debug-info"></div>
        
        <div id="content">
            <div class="loading">
                <div style="display: inline-block; animation: spin 1s linear infinite;">loading...</div>
            </div>
        </div>
    </div>

    <style>
        @keyframes spin {
            0% { opacity: 0.3; }
            50% { opacity: 1; }
            100% { opacity: 0.3; }
        }
    </style>

    <!-- RSS Parser Library -->
    <script src="https://unpkg.com/rss-parser@3.13.0/dist/rss-parser.min.js"></script>

    <script>
        // Global state
        let currentTimeframe = 3;
        let debugMode = true;
        let displayPerPage = 30;
        let currentPage = 1;
        let allStories = [];
        let debugOutput = '';
        
        const sources = {
            'direct-cors': true,
            hackernews: true,
            'reddit-proxy': true,
            'rss-feeds': true
        };

        // Tier 1: CORS-enabled RSS feeds (Direct access, most reliable)
        const corsEnabledFeeds = {
            nytimes_world: 'https://rss.nytimes.com/services/xml/rss/nyt/World.xml',
            nytimes_tech: 'https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml',
            nytimes_business: 'https://rss.nytimes.com/services/xml/rss/nyt/Business.xml'
        };

        // Tier 2: Comprehensive RSS feeds (with fallback methods)
        const rssFeeds = {
            // Major cybersecurity news sources
            bleeping: 'https://www.bleepingcomputer.com/feed/',
            krebs: 'https://krebsonsecurity.com/feed/',
            securityweek: 'https://www.securityweek.com/feed/',
            cybersecuritynews: 'https://cybersecuritynews.com/feed/',
            infosecmag: 'https://www.infosecurity-magazine.com/rss/news/',
            darkreading: 'https://www.darkreading.com/rss.xml',
            thehackernews: 'https://thehackernews.com/feeds/posts/default',
            securityaffairs: 'https://securityaffairs.co/wordpress/feed',
            hackread: 'https://www.hackread.com/feed/',
            
            // Government/official sources
            cisa: 'https://www.cisa.gov/cybersecurity-advisories/all.xml',
            exploitdb: 'https://www.exploit-db.com/rss.xml',
            
            // Additional quality sources
            apisecurity: 'https://apisecurity.io/feed/index.xml',
            f5labs: 'https://www.f5.com/labs/rss-feeds/all.xml'
        };

        // Tier 3: 4-tier CORS proxy system for maximum fallback coverage
        const corsProxies = [
            'https://api.allorigins.win/get?url=',
            'https://thingproxy.freeboard.io/fetch/',
            'https://api.codetabs.com/v1/proxy?quest=',
            'https://corsproxy.io/?'
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
            // Clear all active states
            document.querySelectorAll('.btn').forEach(btn => btn.classList.remove('active'));
            
            // Set timeframe active
            const timeframeBtnId = currentTimeframe === 1 ? 'btn-1d' :
                                 currentTimeframe === 3 ? 'btn-3d' :
                                 currentTimeframe === 7 ? 'btn-7d' :
                                 currentTimeframe === 14 ? 'btn-14d' : 'btn-3d';
            document.getElementById(timeframeBtnId).classList.add('active');
            
            // Set display active  
            document.getElementById(`btn-${displayPerPage}`).classList.add('active');
            
            // Set debug button
            const debugBtn = document.getElementById('debug-btn');
            debugBtn.textContent = debugMode ? 'hide' : 'debug';
            if (debugMode) debugBtn.classList.add('active');
            
            // Update source checkboxes
            Object.keys(sources).forEach(source => {
                const cb = document.getElementById(`check-${source}`);
                if (cb) cb.textContent = sources[source] ? '✓' : '';
            });
            
            // Update debug visibility
            const debugDiv = document.getElementById('debug-info');
            if (debugDiv) {
                debugDiv.style.display = debugMode ? 'block' : 'none';
                if (debugMode) debugDiv.innerHTML = debugOutput;
            }
        }

        // TIER 1: Direct CORS-enabled RSS feeds (No proxies needed!)
        async function fetchDirectCORSFeeds() {
            if (!sources['direct-cors']) return [];
            
            log('TIER 1: Fetching CORS-enabled RSS feeds directly');
            const parser = new RSSParser();
            let allDirectStories = [];
            
            for (const [feedName, feedUrl] of Object.entries(corsEnabledFeeds)) {
                try {
                    log(`${feedName}: fetching direct CORS feed`);
                    const feed = await parser.parseURL(feedUrl);
                    
                    if (feed && feed.items) {
                        const stories = feed.items.map((item, index) => ({
                            objectID: `direct_${feedName}_${index}_${Date.now()}`,
                            title: item.title,
                            author: feedName.replace('_', ' '),
                            points: Math.floor(Math.random() * 60) + 40, // Higher priority for direct feeds
                            num_comments: 0,
                            created_at: item.pubDate || item.isoDate || new Date().toISOString(),
                            url: item.link,
                            description: item.contentSnippet || item.content || '',
                            source: 'direct-rss',
                            rss_source: feedName
                        })).filter(story => story.title && story.url);
                        
                        allDirectStories = allDirectStories.concat(stories);
                        log(`${feedName}: direct access succeeded with ${stories.length} stories`);
                    }
                } catch (error) {
                    log(`${feedName}: direct access failed - ${error.message}`);
                }
                
                await new Promise(r => setTimeout(r, 300));
            }
            
            log(`TIER 1 complete: ${allDirectStories.length} stories from direct CORS feeds`);
            return allDirectStories;
        }

        // TIER 2: RSS feeds with enhanced multi-proxy fallback
        async function fetchRSSWithEnhancedFallback(feedUrl, sourceName) {
            const parser = new RSSParser({
                headers: {
                    'User-Agent': 'Mozilla/5.0 (compatible; RSS Reader)',
                }
            });
            
            // Try each CORS proxy in order
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
                        // AllOrigins returns JSON with contents
                        const response = await fetch(proxyUrl);
                        if (response.ok) {
                            const data = await response.json();
                            if (data.contents) {
                                feedData = await parser.parseString(data.contents);
                            }
                        }
                    } else {
                        // Direct proxy - parse the response
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

        // TIER 2: Fetch all RSS feeds with enhanced reliability
        async function fetchAllRSSFeeds() {
            if (!sources['rss-feeds']) return [];
            
            log('TIER 2: Fetching RSS feeds with enhanced proxy fallbacks');
            let allRSSStories = [];
            
            // Process feeds in smaller batches to avoid timeouts
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
                
                // Longer delay between batches for better reliability
                await new Promise(r => setTimeout(r, 800));
            }
            
            log(`TIER 2 complete: ${allRSSStories.length} stories from RSS feeds`);
            return allRSSStories;
        }

        // TIER 3: Reddit via proxy (existing implementation)
        async function fetchRedditViaProxy() {
            if (!sources['reddit-proxy']) return [];
            
            log('TIER 3: Fetching Reddit via proxy');
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
                
                await new Promise(r => setTimeout(r, 600));
            }
            
            log(`TIER 3 complete: ${allStories.length} stories from Reddit`);
            return allStories;
        }
        
        // TIER 4: Hacker News (existing implementation)
        async function fetchHackerNewsSimple() {
            if (!sources.hackernews) return [];
            
            log('TIER 4: Fetching Hacker News');
            try {
                const now = new Date();
                const cutoff = new Date(now.getTime() - (currentTimeframe * 24 * 60 * 60 * 1000));
                const timestamp = Math.floor(cutoff.getTime() / 1000);
                
                const queries = ['security', 'vulnerability', 'WhatsApp', 'cybersecurity', 'breach', 'malware'];
                let stories = [];
                
                for (const query of queries) {
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
                    
                    await new Promise(r => setTimeout(r, 400));
                }
                
                log(`TIER 4 complete: ${stories.length} stories from Hacker News`);
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
            
            // Enhanced priority keywords
            const priorityKeywords = [
                'whatsapp', 'zero-day', '0-day', 'cve-2025', 'cve-2024', 'vulnerability',
                'data breach', 'ransomware', 'malware', 'exploit', 'critical security',
                'security patch', 'cisa alert', 'emergency update', 'zero click'
            ];
            
            if (priorityKeywords.some(word => text.includes(word))) {
                return true;
            }
            
            // Exclude non-security content
            const exclude = ['gaming', 'sports', 'weather', 'cooking', 'travel', 'music', 'movie', 'entertainment'];
            if (exclude.some(word => text.includes(word))) {
                return false;
            }
            
            // Include cybersecurity content
            const include = [
                'cyber', 'security', 'hack', 'breach', 'threat', 'attack', 'phishing',
                'privacy', 'encryption', 'surveillance', 'spyware', 'backdoor',
                'incident', 'forensics', 'pentest', 'firewall', 'antivirus',
                'authentication', 'authorization', 'compliance', 'gdpr'
            ];
            
            // Direct RSS and RSS feeds are more trusted
            if (story.source === 'direct-rss' || story.source === 'rss') {
                return true;
            }
            
            return include.some(word => text.includes(word));
        }
        
        async function fetchStories() {
            const contentDiv = document.getElementById('content');
            debugOutput = '';
            log('Enhanced Reliability v4.0 starting...');
            log(`4-Tier Stack: Direct CORS → Enhanced RSS → Reddit → HN`);
            log(`Config: ${currentTimeframe}d timeframe, ${displayPerPage} per page`);
            
            contentDiv.innerHTML = '<div class="loading"><div style="animation: spin 1s linear infinite;">4-tier reliability system loading...</div></div>';
            
            try {
                let all = [];
                
                // TIER 1: Direct CORS-enabled feeds (highest priority)
                const directStories = await fetchWithTimeout(fetchDirectCORSFeeds, 20000);
                all = all.concat(directStories);
                log(`TIER 1 summary: ${directStories.length} stories`);

                // TIER 2: RSS feeds with enhanced fallbacks
                const rssStories = await fetchWithTimeout(fetchAllRSSFeeds, 40000);
                all = all.concat(rssStories);
                log(`TIER 2 summary: ${rssStories.length} stories`);
                
                // TIER 3: Reddit discussions
                const reddit = await fetchWithTimeout(fetchRedditViaProxy, 20000);
                all = all.concat(reddit);
                log(`TIER 3 summary: ${reddit.length} stories`);
                
                // TIER 4: Hacker News
                const hn = await fetchWithTimeout(fetchHackerNewsSimple, 15000);
                all = all.concat(hn);
                log(`TIER 4 summary: ${hn.length} stories`);
                
                log(`=== TOTAL COLLECTED: ${all.length} stories ===`);
                
                // Time filtering
                const now = new Date();
                const cutoff = new Date(now.getTime() - (currentTimeframe * 24 * 60 * 60 * 1000));
                
                const timeFiltered = all.filter(story => {
                    if (!story.created_at) return true;
                    const storyDate = new Date(story.created_at);
                    return storyDate >= cutoff || isNaN(storyDate.getTime());
                });
                
                log(`After time filtering: ${timeFiltered.length} stories`);
                
                // Enhanced deduplication
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
                
                // Cybersecurity relevance filtering
                const filtered = unique.filter(isRelevantCybersecStory);
                log(`After cybersecurity filtering: ${filtered.length} stories`);
                
                // Enhanced sorting with source tier priority
                allStories = filtered
                    .map(story => {
                        let sourceMultiplier = 1;
                        if (story.source === 'direct-rss') sourceMultiplier = 2.0; // Highest priority
                        else if (story.source === 'rss') sourceMultiplier = 1.5;
                        else if (story.source === 'hackernews') sourceMultiplier = 1.2;
                        else if (story.source === 'reddit') sourceMultiplier = 1.1;
                        
                        const recencyScore = (new Date(story.created_at).getTime() / 1000000);
                        const totalScore = ((story.points || 0) * sourceMultiplier) + recencyScore;
                        
                        return { ...story, totalScore };
                    })
                    .sort((a, b) => b.totalScore - a.totalScore)
                    .slice(0, 250); // Increased capacity
                
                log(`=== FINAL RANKED SET: ${allStories.length} stories ===`);
                
                if (debugMode && allStories.length > 0) {
                    log("=== TOP 15 STORIES ===");
                    allStories.slice(0, 15).forEach((story, i) => {
                        const sourceDisplay = story.source === 'direct-rss' ? `DIRECT-${story.rss_source}` : 
                                            story.source === 'rss' ? `RSS-${story.rss_source}` : story.source;
                        log(`${i + 1}. [${sourceDisplay}] "${story.title.substring(0, 85)}..." (${story.points}pts)`);
                    });
                    
                    // Check for WhatsApp stories specifically
                    const whatsappStories = allStories.filter(story => 
                        story.title.toLowerCase().includes('whatsapp') || 
                        story.description?.toLowerCase().includes('whatsapp') ||
                        story.title.toLowerCase().includes('cve-2025-55177')
                    );
                    
                    if (whatsappStories.length > 0) {
                        log(`🎯 FOUND ${whatsappStories.length} WHATSAPP STORIES!`);
                        whatsappStories.forEach((story, i) => {
                            log(`  ${i + 1}. [${story.source}] "${story.title}"`);
                        });
                    } else {
                        log("📍 No WhatsApp stories found in this fetch");
                    }
                    
                    // Source breakdown
                    const sourceBreakdown = {};
                    allStories.forEach(story => {
                        const src = story.source === 'direct-rss' ? 'Direct CORS' : 
                                   story.source === 'rss' ? 'RSS Feeds' : 
                                   story.source === 'reddit' ? 'Reddit' : 'Hacker News';
                        sourceBreakdown[src] = (sourceBreakdown[src] || 0) + 1;
                    });
                    
                    log("=== SOURCE BREAKDOWN ===");
                    Object.entries(sourceBreakdown).forEach(([source, count]) => {
                        log(`${source}: ${count} stories`);
                    });
                }
                
                displayStories();
                
            } catch (error) {
                log(`Fatal error: ${error.message}`);
                displayError();
            }
        }
        
        function displayStories() {
            const contentDiv = document.getElementById('content');
            
            if (allStories.length === 0) {
                contentDiv.innerHTML = '<div class="error"><h3>No cybersecurity stories found</h3><p>Try refresh or different timeframe. Check debug for details.</p></div>';
                return;
            }
            
            const totalPages = Math.ceil(allStories.length / displayPerPage);
            const start = (currentPage - 1) * displayPerPage;
            const currentStories = allStories.slice(start, start + displayPerPage);
            
            // Pagination
            let paginationHTML = '';
            if (totalPages > 1) {
                paginationHTML = `<span style="color: #888; font-size: 0.8em;">${currentPage}/${totalPages}</span>`;
                if (currentPage > 1) paginationHTML += `<button class="btn" onclick="changePage(${currentPage - 1})" style="padding: 2px 6px; font-size: 0.8em;"><</button>`;
                if (currentPage < totalPages) paginationHTML += `<button class="btn" onclick="changePage(${currentPage + 1})" style="padding: 2px 6px; font-size: 0.8em;">></button>`;
            }
            document.getElementById('pagination-nav').innerHTML = paginationHTML;
            
            // Stories
            const storiesHTML = currentStories.map((story, i) => {
                const num = start + i + 1;
                const date = new Date(story.created_at).toLocaleDateString();
                const domain = story.url ? new URL(story.url).hostname : 'unknown';
                
                let sourceLabel, sourceCss;
                if (story.source === 'direct-rss') {
                    sourceLabel = 'direct';
                    sourceCss = 'direct';
                } else if (story.source === 'reddit') {
                    sourceLabel = 'r';
                    sourceCss = 'reddit';
                } else if (story.source === 'hackernews') {
                    sourceLabel = 'hn';
                    sourceCss = 'hn';
                } else if (story.source === 'rss') {
                    sourceLabel = story.rss_source?.substring(0, 5) || 'rss';
                    sourceCss = 'rss';
                } else {
                    sourceLabel = 'feed';
                    sourceCss = 'rss';
                }
                
                const commentsUrl = story.reddit_url || 
                                  (story.source === 'hackernews' ? `https://news.ycombinator.com/item?id=${story.objectID}` : story.url);
                
                return `
                    <div class="story ${sourceCss}">
                        <div style="font-size: 0.8em; color: #666; margin-bottom: 5px;">
                            ${num}. <span class="source-indicator source-${sourceCss}">${sourceLabel}</span>
                        </div>
                        <div class="story-title" onclick="window.open('${story.url}', '_blank')">
                            ${story.title}
                        </div>
                        <div class="story-meta">
                            <div class="meta-item"><span>${story.author}</span></div>
                            <div class="meta-item"><span>${story.points}pts</span></div>
                            ${story.num_comments > 0 ? `<div class="meta-item clickable" onclick="window.open('${commentsUrl}', '_blank')"><span>${story.num_comments} comments</span></div>` : ''}
                            <div class="meta-item"><span>${date}</span></div>
                            <div class="meta-item"><span style="color: #666;">${domain}</span></div>
                        </div>
                    </div>
                `;
            }).join('');
            
            contentDiv.innerHTML = `<div class="stories">${storiesHTML}</div>`;
        }
        
        function displayError() {
            document.getElementById('content').innerHTML = '<div class="error"><h3>Error loading stories</h3><p>Check debug info and try refresh.</p><button onclick="fetchStories()" class="btn">retry</button></div>';
        }
        
        // Event handlers
        function setTimeframe(days) {
            currentTimeframe = days;
            currentPage = 1;
            updateButtons();
            fetchStories();
        }
        
        function setDisplay(count) {
            displayPerPage = count;
            currentPage = 1;
            updateButtons();
            displayStories();
        }
        
        function changePage(page) {
            currentPage = page;
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
            updateButtons();
            fetchStories();
        }
        
        // Close dropdowns
        document.addEventListener('click', (e) => {
            if (!e.target.closest('.dropdown')) {
                document.querySelectorAll('.dropdown').forEach(d => d.classList.remove('open'));
            }
        });
        
        // Initialize
        window.addEventListener('load', () => {
            log('Enhanced Reliability v4.0 loaded');
            log('4-Tier Stack: Direct CORS → Enhanced RSS → Reddit → HN');
            updateButtons();
            
            setTimeout(() => {
                fetchStories();
            }, 1000);
        });
    </script>
</body>
</html>
