<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>earthyfort // Cybersecurity Portfolio</title>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0a0e14;
            --card-bg: #131924;
            --border-color: #1e293b;
            --text-main: #e2e8f0;
            --text-muted: #94a3b8;
            --accent-green: #00ff66;
            --accent-cyan: #00f0ff;
            --accent-red: #ff3366;
            --font-mono: 'Fira Code', monospace;
            --font-sans: 'Inter', sans-serif;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            font-family: var(--font-sans);
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }

        #matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.15;
            pointer-events: none;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        .terminal-header {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            margin-bottom: 30px;
        }

        .terminal-bar {
            background: #0f172a;
            padding: 10px 15px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
        }

        .dots {
            display: flex;
            gap: 8px;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }
        .dot.red { background: #ff5f56; }
        .dot.yellow { background: #ffbd2e; }
        .dot.green { background: #27c93f; }

        .terminal-title {
            margin-left: 20px;
            font-family: var(--font-mono);
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .terminal-body {
            padding: 25px;
            font-family: var(--font-mono);
        }

        .prompt-line {
            color: var(--accent-green);
            margin-bottom: 10px;
        }

        .prompt-user { color: var(--accent-cyan); }
        .prompt-host { color: var(--accent-green); }

        .hero-title {
            font-size: 1.8rem;
            color: #fff;
            margin: 10px 0;
            font-weight: 600;
        }

        .hero-bio {
            color: var(--text-muted);
            font-family: var(--font-sans);
            font-size: 1rem;
            margin-bottom: 20px;
        }

        .status-badge {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: rgba(0, 255, 102, 0.1);
            color: var(--accent-green);
            border: 1px solid rgba(0, 255, 102, 0.3);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-family: var(--font-mono);
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: var(--accent-green);
            border-radius: 50%;
            box-shadow: 0 0 8px var(--accent-green);
        }

        .nav-tabs {
            display: flex;
            gap: 15px;
            border-bottom: 1px solid var(--border-color);
            margin-bottom: 30px;
        }

        .tab-btn {
            background: none;
            border: none;
            color: var(--text-muted);
            font-family: var(--font-mono);
            font-size: 1rem;
            padding: 10px 15px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            transition: all 0.3s ease;
        }

        .tab-btn:hover, .tab-btn.active {
            color: var(--accent-cyan);
            border-bottom-color: var(--accent-cyan);
        }

        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 20px;
            transition: transform 0.2s ease, border-color 0.2s ease;
        }

        .card:hover {
            transform: translateY(-3px);
            border-color: var(--accent-cyan);
        }

        .card-tag {
            font-family: var(--font-mono);
            font-size: 0.75rem;
            color: var(--accent-green);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 8px;
            display: block;
        }

        .card-title {
            color: #fff;
            font-size: 1.2rem;
            margin-bottom: 10px;
        }

        .card-desc {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-bottom: 15px;
        }

        .card-link {
            color: var(--accent-cyan);
            text-decoration: none;
            font-family: var(--font-mono);
            font-size: 0.9rem;
            font-weight: 600;
        }

        .card-link:hover {
            text-decoration: underline;
        }

        footer {
            margin-top: 50px;
            padding-top: 20px;
            border-top: 1px solid var(--border-color);
            text-align: center;
            font-family: var(--font-mono);
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 15px;
        }

        .social-links a {
            color: var(--text-main);
            text-decoration: none;
            transition: color 0.2s;
        }

        .social-links a:hover {
            color: var(--accent-green);
        }
    </style>
</head>
<body>

    <canvas id="matrix-bg"></canvas>

    <div class="container">
        <header class="terminal-header">
            <div class="terminal-bar">
                <div class="dots">
                    <span class="dot red"></span>
                    <span class="dot yellow"></span>
                    <span class="dot green"></span>
                </div>
                <span class="terminal-title">bash - earthyfort@defense-node: ~</span>
            </div>
            <div class="terminal-body">
                <div class="prompt-line">
                    <span class="prompt-user">earthyfort</span>@<span class="prompt-host">security-lab</span>:~$ whoami
                </div>
                <h1 class="hero-title">Defensive & Offensive Security Specialist</h1>
                <p class="hero-bio">
                    Dedicated to threat mitigation, security analysis, and safeguarding digital infrastructure behind the scenes.
                </p>
                <div class="status-badge">
                    <span class="status-dot"></span> SYSTEM ONLINE // OPEN FOR COLLABORATION
                </div>
            </div>
        </header>

        <nav class="nav-tabs">
            <button class="tab-btn active" onclick="switchTab(event, 'projects')">[ Projects ]</button>
            <button class="tab-btn" onclick="switchTab(event, 'writeups')">[ Write-ups ]</button>
            <button class="tab-btn" onclick="switchTab(event, 'skills')">[ Skills ]</button>
        </nav>

        <div id="projects" class="tab-content active">
            <div class="grid">
                <div class="card">
                    <span class="card-tag">Python // Security Tool</span>
                    <h3 class="card-title">Network Packet Inspector</h3>
                    <p class="card-desc">Monitors network traffic to detect anomalies and flag malicious signatures in real-time.</p>
                    <a href="https://github.com/earthyfort/projects" target="_blank" class="card-link">View Repo &rarr;</a>
                </div>
                <div class="card">
                    <span class="card-tag">SIEM // Defense</span>
                    <h3 class="card-title">SOC Lab Automation</h3>
                    <p class="card-desc">Simulated Active Directory environment integrated with Elastic SIEM for rule validation.</p>
                    <a href="https://github.com/earthyfort/projects" target="_blank" class="card-link">View Repo &rarr;</a>
                </div>
            </div>
        </div>

        <div id="writeups" class="tab-content">
            <div class="grid">
                <div class="card">
                    <span class="card-tag">TryHackMe // Medium</span>
                    <h3 class="card-title">Linux PrivEsc Walkthrough</h3>
                    <p class="card-desc">Step-by-step breakdown of exploiting misconfigured SUID binaries to obtain root privilege.</p>
                    <a href="#" class="card-link">Read Analysis &rarr;</a>
                </div>
            </div>
        </div>

        <div id="skills" class="tab-content">
            <div class="card">
                <span class="card-tag">Core Stack</span>
                <h3 class="card-title" style="margin-bottom:15px;">Technical Arsenal</h3>
                <p class="card-desc">
                    <strong>Languages:</strong> Python, Bash, SQL<br>
                    <strong>Tools:</strong> Wireshark, Metasploit, Nmap, Burp Suite, Elastic SIEM<br>
                    <strong>Domains:</strong> Threat Analysis, Incident Response, Network Defense
                </p>
            </div>
        </div>

        <footer>
            <div class="social-links">
                <a href="https://github.com/earthyfort" target="_blank">GitHub</a>
                <a href="https://linkedin.com/in/nia-es" target="_blank">LinkedIn</a>
            </div>
            <p>&copy; 2026 earthyfort. All security protocols verified.</p>
        </footer>
    </div>

    <script>
        function switchTab(evt, tabId) {
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            evt.currentTarget.classList.add('active');
        }

        const canvas = document.getElementById('matrix-bg');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const letters = '01ABCDEFGHIJKLMNOPQRSTUVWXYZ@#$%^&*';
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = Array(Math.floor(columns)).fill(1);

        function drawMatrix() {
            ctx.fillStyle = 'rgba(10, 14, 20, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#00ff66';
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = letters[Math.floor(Math.random() * letters.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }
        setInterval(drawMatrix, 33);

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
