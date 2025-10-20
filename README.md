<!DOCTYPE html>
<html lang="tl" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DAAN DAAN: A Traffic Solution for Metro Manila</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">
    <script>
        // Tailwind dark mode configuration
        tailwind.config = {
            darkMode: 'class',
        }
    </script>
    <style>
        :root {
            /* Light Mode (Matte) */
            --bg-color: #F8F8F8;
            --text-primary: #1D1D1F;
            --text-secondary: #6B6B6B;
            --border-color: #E5E5E5;
            --card-bg: rgba(255, 255, 255, 0.5);
            --header-bg: rgba(248, 248, 248, 0.7);
            --dot-color: rgba(0,0,0,0.05);
            --gradient-start: #FF6034;
            --gradient-end: #FF8A65;
        }

        html.dark {
            /* Dark Mode (Shiny/Poppy) */
            --bg-color: #0A0A0A;
            --text-primary: #EAEAEA;
            --text-secondary: #888888;
            --border-color: rgba(255, 255, 255, 0.15);
            --card-bg: rgba(0, 0, 0, 0.2);
            --header-bg: rgba(10, 10, 10, 0.7);
            --dot-color: rgba(255,255,255,0.1);
            --gradient-start: #00BFFF;
            --gradient-end: #00FF7F;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            transition: background-color 0.3s, color 0.3s;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        /* --- Background Styles --- */
        .background-wrapper {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -10;
            overflow: hidden;
            transition: opacity 0.5s;
        }

        html.dark .background-wrapper.light-only { opacity: 0; }
        
        .circle-blur {
            position: absolute;
            border-radius: 50%;
            filter: blur(120px);
            opacity: 0.15;
            transition: all 1.5s cubic-bezier(0.165, 0.84, 0.44, 1);
        }

        .circle-blur.one {
            width: 500px; height: 500px; top: 10vh; left: -150px;
            background-color: var(--gradient-start);
        }
        .circle-blur.two {
            width: 600px; height: 600px; bottom: 5vh; right: -200px;
            background-color: var(--gradient-end);
        }

        body:not(.dark) {
            background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3e%3cline x1='-10' y1='10' x2='110' y2='90' stroke='rgba(0,0,0,0.02)' stroke-width='1'/%3e%3cline x1='10' y1='-10' x2='90' y2='110' stroke='rgba(0,0,0,0.03)' stroke-width='1'/%3e%3c/svg%3e");
        }

        html.dark .dot-grid-background {
            background-image: radial-gradient(circle at 1px 1px, var(--dot-color) 1px, transparent 0);
            background-size: 25px 25px;
        }
        
        /* --- General Styles --- */
        .font-black-extended { font-weight: 900; letter-spacing: -0.05em; }
        .gradient-text {
            background: linear-gradient(90deg, var(--gradient-start), var(--gradient-end));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gradient-bg { background: linear-gradient(90deg, var(--gradient-start), var(--gradient-end)); }
        
        .section-fade-in {
            opacity: 0; transform: translateY(20px);
            transition: opacity 0.8s ease-out, transform 0.8s ease-out;
        }
        .section-fade-in.is-visible { opacity: 1; transform: translateY(0); }
        
        .card {
            border: 1px solid var(--border-color);
            background-color: var(--card-bg);
            backdrop-filter: blur(12px);
            transition: transform 0.3s, box-shadow 0.3s, border-color 0.3s, background-color 0.3s;
            box-shadow: 0 4px 15px -1px rgba(0, 0, 0, 0.04), 0 2px 8px -1px rgba(0, 0, 0, 0.02);
        }
        html.dark .card { box-shadow: 0 0 15px rgba(0, 255, 127, 0.1), 0 0 5px rgba(0, 255, 127, 0.05); }
        .card:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 25px -3px rgba(0, 0, 0, 0.08), 0 4px 10px -2px rgba(0, 0, 0, 0.04);
        }
        html.dark .card:hover { box-shadow: 0 0 25px -5px var(--gradient-end), 0 0 10px var(--gradient-start); }
        
        .location-btn { transition: transform 0.2s, opacity 0.2s; }
        .location-btn:hover { transform: translateY(-2px); opacity: 0.9; }
        .location-btn.active { opacity: 1; }
        
        .nav-link { transition: color 0.2s; }
        .nav-link:hover { color: var(--gradient-start); }
        
        .accent-icon { color: var(--gradient-start); }
        .accent-bg-subtle { background-color: color-mix(in srgb, var(--gradient-start) 10%, transparent); }
        
        /* --- Braess Paradox Diagram --- */
        .paradox-container {
            position: relative; display: grid; grid-template-columns: 1fr 1fr 1fr; grid-template-rows: 1fr 1fr 1fr;
            width: 100%; max-width: 500px; aspect-ratio: 1.5 / 1; margin: auto;
        }
        .node {
            display: grid; place-items: center; font-weight: bold; color: var(--bg-color);
            background-color: var(--text-primary); border-radius: 50%;
            width: 40px; height: 40px; z-index: 3; justify-self: center; align-self: center;
        }
        #node-A { grid-area: 2 / 1 / 3 / 2; } #node-C { grid-area: 1 / 2 / 2 / 3; }
        #node-D { grid-area: 3 / 2 / 4 / 3; } #node-B { grid-area: 2 / 3 / 3 / 4; }
        .road-network { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 1; overflow: visible; }
        .road-visual { stroke: var(--border-color); stroke-width: 10; stroke-linecap: round; fill: none; }
        .road-dash { stroke: var(--text-secondary); stroke-width: 1; stroke-dasharray: 8 8; fill: none; }
        .road-visual.shortcut, .road-dash.shortcut { stroke: var(--gradient-end); opacity: 0; transition: opacity 0.3s ease; }
        .road-dash.shortcut { stroke: white; }
        .shortcut-visible .road-visual.shortcut, .shortcut-visible .road-dash.shortcut { opacity: 1; }

        /* --- Gantt Chart --- */
        .gantt-container { display: grid; grid-template-columns: 180px 1fr; gap: 1rem; }
        .gantt-header { grid-column: 2 / -1; display: grid; grid-template-columns: repeat(8, 1fr); text-align: center; font-size: 0.875rem; color: var(--text-secondary); padding-bottom: 0.5rem; border-bottom: 1px solid var(--border-color); }
        .gantt-row { display: contents; }
        .gantt-task-name { display: flex; align-items: center; font-size: 0.875rem; font-weight: 500; padding: 0.5rem 0; white-space: nowrap; }
        .gantt-grid { display: grid; grid-template-columns: repeat(8, 1fr); align-items: center; padding: 0.5rem 0; gap: 0.25rem; }
        .gantt-bar {
            grid-column-start: var(--start-week); grid-column-end: var(--end-week); height: 1.75rem; border-radius: 0.375rem;
            opacity: 0; transform: scaleX(0); transform-origin: left;
            animation: gantt-bar-in 0.8s cubic-bezier(0.165, 0.84, 0.44, 1) forwards; animation-delay: var(--delay);
        }
        @keyframes gantt-bar-in { to { opacity: 1; transform: scaleX(1); } }
        @media (max-width: 768px) { .gantt-container { grid-template-columns: 120px 1fr; } .gantt-task-name { font-size: 0.75rem; } }

        /* --- NEW: Sidebar, Header & Nav --- */
        .header {
            backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .header-hidden { transform: translateY(-100%); }

        .sidebar {
            background-color: var(--card-bg);
            backdrop-filter: blur(24px); -webkit-backdrop-filter: blur(24px);
            border-right: 1px solid var(--border-color);
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        #sidebar-trigger {
            transition: transform 0.3s ease, opacity 0.3s ease;
        }
        #sidebar-trigger:hover { transform: translateX(5px); }
        #sidebar-trigger::before {
            content: ''; position: absolute; top: -12px; left: -12px; right: -12px; bottom: -12px;
            background: radial-gradient(circle, rgba(0,0,0,0.1) 0%, rgba(0,0,0,0) 70%);
            backdrop-filter: blur(3px); -webkit-backdrop-filter: blur(3px);
            border-radius: 50%; opacity: 0; transform: scale(0.8);
            transition: opacity 0.3s, transform 0.3s;
        }
        #sidebar-trigger:hover::before { opacity: 1; transform: scale(1); }

        .sidebar-link {
            color: var(--text-primary);
            transition: color 0.2s, background-color 0.2s;
            font-weight: 500;
        }
        .sidebar-link:hover {
            color: var(--gradient-start);
            background-color: color-mix(in srgb, var(--text-secondary) 10%, transparent);
        }
    </style>
</head>
<body class="dot-grid-background">

    <!-- NEW: Sidebar Trigger -->
    <button id="sidebar-trigger" aria-label="Open Menu" class="fixed top-1/2 -translate-y-1/2 left-4 z-[60] w-12 h-12 flex items-center justify-center rounded-full opacity-50 hover:opacity-100">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" class="text-[var(--text-primary)]"><path d="m9 18 6-6-6-6"/></svg>
    </button>
    
    <!-- NEW: Sidebar & Overlay -->
    <div id="sidebar-overlay" class="fixed inset-0 bg-black/30 z-[55] opacity-0 pointer-events-none transition-opacity duration-300"></div>
    <aside id="sidebar" class="sidebar fixed top-0 left-0 h-full w-72 p-8 z-[60] -translate-x-full">
        <h3 class="text-xl font-bold">DAAN DAAN</h3>
        <p class="text-sm mt-2" style="color: var(--text-secondary);">Account & Support</p>
        <nav class="mt-8 flex flex-col gap-2">
            <a href="#" class="sidebar-link flex items-center gap-4 h-12 px-4 rounded-lg">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="flex-shrink-0"><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
                <span>Aking Account</span>
            </a>
            <a href="#" class="sidebar-link flex items-center gap-4 h-12 px-4 rounded-lg">
                 <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="flex-shrink-0"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"/><path d="M12 17h.01"/></svg>
                <span>Tulong at Suporta</span>
            </a>
            <a href="#" class="sidebar-link flex items-center gap-4 h-12 px-4 rounded-lg">
                <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="flex-shrink-0"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
                <span>Mag-log Out</span>
            </a>
        </nav>
        <div class="mt-auto text-center text-xs" style="color: var(--text-secondary);">
            <p>12 - ZARA</p>
            <p class="mt-1">ABRIGO, CALLEJA, CASIANO, ARGUIL, MACOPIA</p>
        </div>
    </aside>

    <div class="background-wrapper light-only">
        <div class="circle-blur one"></div>
        <div class="circle-blur two"></div>
    </div>

    <!-- NEW: Header with Hide/Show on scroll -->
    <header id="header" class="header fixed top-0 left-0 right-0 z-40">
        <div class="container mx-auto px-6 h-16 flex justify-between items-center" style="background-color: var(--header-bg);">
            <a href="#" class="text-xl font-bold tracking-tighter hover:opacity-80 transition-opacity">DAAN DAAN</a>
            <nav class="hidden md:flex items-center gap-6 text-sm font-medium" style="color: var(--text-secondary);">
                <a href="#problema" class="nav-link">Ang Problema</a>
                <a href="#layunin" class="nav-link">Mga Layunin</a>
                <a href="#metodolohiya" class="nav-link">Metodolohiya</a>
                <a href="#resulta" class="nav-link">Resulta</a>
                <a href="#benepisyo" class="nav-link">Benepisyo</a>
                <a href="#timeline" class="nav-link">Talatakdaan</a>
            </nav>
            <div class="flex items-center gap-2">
                <a href="DAAN_DAAN_Research_Paper.pdf" download="DAAN_DAAN_Paper.pdf" class="hidden sm:block bg-[var(--text-primary)] text-[var(--bg-color)] px-4 py-2 rounded-full text-sm font-medium hover:opacity-80 transition-opacity">Basahin ang Papel</a>
                <button id="theme-toggle" class="w-8 h-8 rounded-full flex items-center justify-center bg-gray-500/10 hover:bg-gray-500/20 transition-colors" aria-label="Toggle Dark Mode">
                    <svg id="sun-icon" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="hidden"><path d="M12 1v2m0 18v2M4.22 4.22l1.42 1.42m12.72 12.72l1.42 1.42M1 12h2m18 0h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/><circle cx="12" cy="12" r="5"/></svg>
                    <svg id="moon-icon" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="hidden"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>
                </button>
            </div>
        </div>
    </header>

    <main class="container mx-auto px-6">
        <!-- Section 1: Hero --><section class="min-h-screen flex flex-col justify-center items-center text-center pt-20">
            <div class="max-w-4xl">
                <h2 class="text-6xl md:text-8xl lg:text-9xl font-black-extended leading-none">Paglutas sa Trapiko ng <span class="gradient-text">Metro Manila</span>.</h2>
                <p class="mt-6 text-lg md:text-xl max-w-2xl mx-auto" style="color: var(--text-secondary);">Ipinapakilala ang DAAN DAAN: Isang bagong paraan ng pagtingin sa problema ng trapiko, gamit ang isang paradox para sa solusyon.</p>
            </div>
            <div class="absolute bottom-10 animate-bounce">
                <svg class="w-6 h-6 text-gray-400 dark:text-gray-600" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor"><path d="M19 14l-7 7m0 0l-7-7m7 7V3"></path></svg>
            </div>
        </section>

        <!-- Section 2: The Problem --><section id="problema" class="min-h-screen flex items-center justify-center section-fade-in">
            <div class="text-center max-w-5xl">
                <div class="text-7xl md:text-9xl font-black-extended">
                    <span class="gradient-text">₱3.5 Bilyon</span>
                </div>
                <p class="mt-4 text-2xl md:text-3xl font-medium">Ang nawawalang halaga araw-araw dahil sa masikip na trapiko.</p>
                <p class="mt-2 text-lg" style="color: var(--text-secondary);">Sinubukan nating magdagdag ng kalsada. Hindi ito ang pangmatagalang lunas.</p>
            </div>
        </section>

        <!-- Section 3: The Insight - Braess' Paradox --><section id="paradox" class="min-h-screen flex flex-col justify-center items-center section-fade-in">
            <div class="w-full max-w-4xl text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Ang Kabalintunaan ni Braess</h3>
                <p class="mt-4 text-lg" style="color: var(--text-secondary);">Kung minsan, ang pagdaragdag ng daan ay nakakapagpalala, at ang pagbabawas ay nakakapagpabuti sa daloy ng trapiko.</p>
                <div class="mt-8 p-8 rounded-2xl card">
                    <div class="paradox-container" id="paradox-container">
                        <svg class="road-network" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet">
                            <defs>
                                <path id="path-ACB" d="M 100 200 L 300 100 L 500 200" />
                                <path id="path-ADB" d="M 100 200 L 300 300 L 500 200" />
                                <path id="path-CD" d="M 300 100 L 300 300" />
                            </defs>
                            <use href="#path-ACB" class="road-visual" /> <use href="#path-ADB" class="road-visual" />
                            <use href="#path-CD" class="road-visual shortcut" /> <use href="#path-ACB" class="road-dash" />
                            <use href="#path-ADB" class="road-dash" /> <use href="#path-CD" class="road-dash shortcut" />
                        </svg>
                        <div id="node-A" class="node">A</div> <div id="node-C" class="node">C</div>
                        <div id="node-D" class="node">D</div> <div id="node-B" class="node">B</div>
                    </div>
                    <div class="mt-8 text-center">
                        <p class="text-xl font-medium">Kabuuang Oras ng Biyahe: <span id="travel-time" class="font-bold text-green-500 transition-colors duration-500">45 minuto</span></p>
                        <button id="toggle-shortcut" class="mt-4 px-6 py-2 rounded-full font-bold transition-transform hover:scale-105 gradient-bg text-white">Idagdag ang Shortcut</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 4: Layunin (Objectives) --><section id="layunin" class="min-h-screen flex items-center justify-center section-fade-in">
            <div class="max-w-4xl text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Ang Aming mga Layunin</h3>
                <p class="mt-4 text-lg" style="color: var(--text-secondary);">Ang DAAN DAAN ay binuo na may malinaw na misyon na lutasin ang problema ng trapiko sa Pilipinas.</p>
                <div class="mt-12 grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div class="card p-8 text-left">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Pangkalahatang Layunin</h4>
                        <p class="mt-2 text-base" style="color: var(--text-secondary);">Pagbutihin ang daloy ng trapiko at bawasan ang oras ng biyahe sa mga urban area sa pamamagitan ng strategic road network optimization.</p>
                    </div>
                    <div class="card p-8 text-left">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M12 2v20M17 5H7l5 5-5 5h10l-5 5"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Tiyak na Layunin</h4>
                        <ul class="mt-2 space-y-2 text-base list-disc list-inside" style="color: var(--text-secondary);">
                            <li>Mag-identify ng mga optimal na kalsada para sa pagsasara.</li>
                            <li>Mag-quantify ng oras na natipid sa system-wide travel time.</li>
                            <li>Magbigay ng data-driven na insights sa mga policymakers.</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 5: Metodolohiya (Methodology) --><section id="metodolohiya" class="min-h-screen flex flex-col justify-center section-fade-in">
            <div class="text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Ang Proseso ng DAAN DAAN</h3>
                <p class="mt-4 text-lg max-w-3xl mx-auto" style="color: var(--text-secondary);">Ang aming automated na sistema ay sumusuri sa bawat kalsada para sa epekto nito sa kabuuang network.</p>
            </div>
            <div class="mt-16 grid grid-cols-1 md:grid-cols-3 gap-8 max-w-6xl mx-auto">
                <div class="rounded-2xl p-8 card">
                    <div class="flex items-center gap-4">
                        <div class="accent-bg-subtle p-3 rounded-lg"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg></div>
                        <h4 class="text-2xl font-bold">I. Input</h4>
                    </div>
                    <ul class="mt-6 space-y-3 list-disc list-inside" style="color: var(--text-secondary);">
                        <li>Pangalan ng Lokasyon</li>
                        <li>Bilang ng Sample Trips</li>
                        <li>Congestion Severity (Oras)</li>
                        <li>Datos mula sa OpenStreetMap</li>
                    </ul>
                </div>
                <div class="rounded-2xl p-8 card">
                    <div class="flex items-center gap-4">
                        <div class="accent-bg-subtle p-3 rounded-lg"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M12 20.94c1.5 0 2.75 1.06 4 1.06 3 0 6-8 6-12.5A4.5 4.5 0 0 0 18 5.5c0 1.5-1.5 2.5-3 2.5-1.5 0-3-1-3-2.5S9 4 7.5 4 4.5 8 4.5 12.5c0 4.5 3 12.5 6 12.5 1.25 0 2.5-1.06 4-1.06Z"></path><path d="M12 2.25c-1.5 0-2.75-1.06-4-1.06-3 0-6 8-6 12.5A4.5 4.5 0 0 1 6 18.5c0-1.5 1.5-2.5 3-2.5 1.5 0 3 1 3 2.5s3 1.5 4.5 1.5 3-3.5 3-8-1.5-8.5-3-8.5c-1.25 0-2.5 1.06-4 1.06Z"></path></svg></div>
                        <h4 class="text-2xl font-bold">II. Proseso</h4>
                    </div>
                    <ul class="mt-6 space-y-3 list-disc list-inside" style="color: var(--text-secondary);">
                        <li>Network Modeling & Baseline</li>
                        <li>Iterative Closure Analysis</li>
                        <li>Simulation at Data Collection</li>
                        <li>Ranking ng mga Resulta</li>
                    </ul>
                </div>
                <div class="rounded-2xl p-8 card">
                    <div class="flex items-center gap-4">
                        <div class="accent-bg-subtle p-3 rounded-lg"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M3 3v18h18"></path><path d="M18.7 8a6 6 0 0 0-6-6"></path><path d="M13 8a2 2 0 0 0-2-2"></path></svg></div>
                        <h4 class="text-2xl font-bold">III. Output</h4>
                    </div>
                    <ul class="mt-6 space-y-3 list-disc list-inside" style="color: var(--text-secondary);">
                        <li>Optimal na Listahan ng Kalsada</li>
                        <li>Total System Travel Time Savings</li>
                        <li>Winners vs Losers Analysis</li>
                        <li>Interactive Visualizations</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Section 6: Results --><section id="resulta" class="min-h-screen flex flex-col justify-center section-fade-in">
             <div class="text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Ang Pruweba: Dalawang Lungsod.</h3>
                <p class="mt-4 text-lg max-w-3xl mx-auto" style="color: var(--text-secondary);">Sinuri ng sistema ang dalawang magkaibang urban network at nakahanap ng mga pagsasara ng kalsada na nagpabuti sa daloy ng trapiko.</p>
            </div>
            <div class="mt-12 max-w-6xl mx-auto w-full rounded-2xl card p-6">
                 <div class="p-2 border rounded-full flex justify-center items-center gap-2 max-w-sm mx-auto" style="border-color: var(--border-color)">
                    <button id="btn-alabang" class="location-btn text-white px-6 py-2 rounded-full font-bold w-full active gradient-bg">Alabang</button>
                    <button id="btn-portarea" class="location-btn bg-transparent px-6 py-2 rounded-full font-bold w-full" style="color: var(--text-secondary)">Port Area</button>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-5 gap-8 p-8">
                    <div class="md:col-span-3">
                        <h4 id="result-title" class="text-3xl font-bold tracking-tight">Resulta para sa Alabang</h4>
                        <p class="mt-2" style="color: var(--text-secondary);">Pinapakita rito ang mga kalsadang isinara na may pinakamalaking positibong epekto sa buong network.</p>
                        <div class="mt-8 space-y-4">
                            <div class="flex justify-between items-end pb-2 border-b" style="border-color: var(--border-color); color: var(--text-secondary);">
                                <span>Pangalan ng Kalsada</span> <span>Natipid na Oras (min)</span>
                            </div> <ul id="road-list" class="space-y-3"></ul>
                        </div>
                    </div>
                    <div class="md:col-span-2 md:border-l md:pl-8" style="border-color: var(--border-color)">
                        <h4 class="text-xl font-bold">Buod ng Epekto</h4>
                        <div class="mt-6">
                            <p class="text-sm" style="color: var(--text-secondary);">Inisyal na Oras ng Biyahe (Sistema)</p>
                            <p id="initial-time" class="text-3xl font-bold"></p>
                        </div>
                        <div class="mt-4">
                            <p class="text-sm" style="color: var(--text-secondary);">Pinakamahusay na Oras (matapos isara)</p>
                            <p id="final-time" class="text-3xl font-bold gradient-text"></p>
                        </div>
                        <div class="mt-8 rounded-lg p-4" style="background-color: color-mix(in srgb, var(--gradient-end) 10%, transparent); border: 1px solid color-mix(in srgb, var(--gradient-end) 30%, transparent);">
                            <p class="font-bold" style="color: var(--gradient-end);">Statistically Significant</p>
                            <p id="p-value" class="text-sm" style="color: var(--text-secondary);"></p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- Section 7: Benefits --><section id="benepisyo" class="min-h-screen flex flex-col justify-center items-center section-fade-in">
            <div class="max-w-4xl text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Ang mga Benepisyo ng DAAN DAAN</h3>
                <p class="mt-4 text-lg" style="color: var(--text-secondary);">Ang pagpapatupad ng DAAN DAAN ay nagbibigay ng malawak na benepisyo hindi lamang sa daloy ng trapiko, kundi pati na rin sa komunidad at ekonomiya.</p>
                <div class="mt-12 grid grid-cols-1 md:grid-cols-2 gap-8 text-left">
                    <div class="card p-8">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Malaking Pagtitipid sa Oras</h4>
                        <p class="mt-2 text-base" style="color: var(--text-secondary);">Bawasan ang oras na ginugugol sa biyahe ng mga motorista, na nagreresulta sa mas mataas na produktibidad at kalidad ng buhay.</p>
                    </div>
                    <div class="card p-8">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M10.39 12.07l-2.43 2.43c-.93.93-1.39 2.22-1.39 3.46v.54h12v-.54c0-1.24-.46-2.53-1.39-3.46l-2.43-2.43"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Pagbaba ng Polusyon</h4>
                        <p class="mt-2 text-base" style="color: var(--text-secondary);">Mas maayos na daloy ng trapiko ay nangangahulugan ng mas kaunting idling at mas mababang carbon emissions.</p>
                    </div>
                    <div class="card p-8">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><path d="M22 4L12 14.01l-3-3"/><path d="M15 9h5"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Data-Driven na Pagpaplano</h4>
                        <p class="mt-2 text-base" style="color: var(--text-secondary);">Magbigay ng solidong ebidensya para sa mga desisyon sa urban planning, na nagpapataas ng pagiging epektibo ng mga proyekto.</p>
                    </div>
                     <div class="card p-8">
                        <div class="accent-bg-subtle p-3 rounded-lg inline-block">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="accent-icon"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
                        </div>
                        <h4 class="text-2xl font-bold mt-4">Pagpapalakas ng Ekonomiya</h4>
                        <p class="mt-2 text-base" style="color: var(--text-secondary);">Mas mahusay na transportasyon ay nagpapababa ng gastos sa logistik at nagpapalakas ng lokal na ekonomiya.</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 8: Timeline --><section id="timeline" class="min-h-screen flex flex-col justify-center items-center section-fade-in">
            <div class="max-w-4xl w-full text-center">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Project Roadmap</h3>
                <p class="mt-4 text-lg max-w-3xl mx-auto" style="color: var(--text-secondary);">Isang 8-linggong plano para sa development at deployment ng DAAN DAAN proof-of-concept.</p>
                <div id="gantt-chart-container" class="mt-12 w-full card p-6 md:p-8 text-left"></div>
            </div>
        </section>

        <!-- Section 9: The Advantage --><section id="advantage" class="min-h-screen flex items-center justify-center section-fade-in">
            <div class="text-center max-w-6xl w-full">
                <h3 class="text-4xl md:text-5xl font-bold tracking-tight">Proactive, Hindi Reactive.</h3>
                <p class="mt-4 text-lg max-w-3xl mx-auto" style="color: var(--text-secondary);">Hindi tulad ng ibang tools na sumasagot lang sa kasalukuyang traffic, ang DAAN DAAN ay nagbibigay ng proactive na solusyon.</p>
                <div class="mt-20 grid grid-cols-1 md:grid-cols-3 gap-8 text-left items-center">
                    <div class="rounded-2xl p-8 card h-full">
                        <h4 class="text-2xl font-bold">Waze / Google Maps</h4>
                        <p class="mt-2" style="color: var(--text-secondary);">Nagbibigay ng real-time na update pero reaktibo lamang. Sinusundan nito ang trapiko, hindi ito lumulutas ng sanhi.</p>
                        <span class="inline-block mt-4 text-yellow-800 dark:text-yellow-400 bg-yellow-400/20 px-3 py-1 rounded-full text-sm font-medium">REACTIVE</span>
                    </div>
                    <div class="relative rounded-2xl p-8 card h-full md:scale-110 z-10 transition-transform duration-300">
                        <div class="absolute -top-5 left-1/2 -translate-x-1/2">
                            <div class="gradient-bg text-white px-5 py-1.5 rounded-full text-sm font-semibold tracking-wide shadow-lg">Inirerekomenda</div>
                        </div>
                        <h4 class="text-2xl font-bold">DAAN DAAN</h4>
                        <p class="mt-2" style="color: var(--text-secondary);">Pinagsasama ang proactive analysis sa isang automated at user-friendly na system para sa mabilis na pagtuklas ng solusyon.</p>
                        <span class="inline-block mt-4 text-green-800 dark:text-green-400 bg-green-500/20 px-3 py-1 rounded-full text-sm font-medium">PROACTIVE & AUTOMATED</span>
                    </div>
                    <div class="rounded-2xl p-8 card h-full">
                        <h4 class="text-2xl font-bold">SUMO / VISSIM</h4>
                        <p class="mt-2" style="color: var(--text-secondary);">Sobrang teknikal, nangangailangan ng manual na setup at mga dalubhasang data scientist para magamit.</p>
                        <span class="inline-block mt-4 text-blue-800 dark:text-blue-400 bg-blue-500/20 px-3 py-1 rounded-full text-sm font-medium">EXPERT-DRIVEN</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 10: Call to Action --><section class="min-h-[70vh] flex flex-col justify-center items-center text-center section-fade-in">
             <div class="max-w-3xl">
                <h2 class="text-5xl md:text-6xl font-black-extended leading-tight">Mas Malinaw ang Daan sa Hinaharap.</h2>
                <p class="mt-6 text-lg" style="color: var(--text-secondary);">Ang DAAN DAAN ay isang proof-of-concept na handang tumulong sa mga urban planner at LGU sa buong Pilipinas.</p>
                <div class="mt-10 flex flex-col sm:flex-row justify-center gap-4">
                    <a href="mailto:contact@daandaan.ph?subject=Inquiry%20about%20the%20DAAN%20DAAN%20Project" class="gradient-bg text-white px-8 py-4 rounded-full font-bold text-lg transition-transform hover:scale-105">Makipag-ugnayan sa Team</a>
                    <a href="https://drive.google.com/file/d/1dYpm29cCUe28CfWgTP421KB13n0SnngC/view?usp=sharing" download="DAAN_DAAN_Paper.pdf" class="px-8 py-4 rounded-full font-bold text-lg transition-colors hover:opacity-80" style="background-color: var(--border-color); color: var(--text-primary);">I-download ang Research Paper</a>
                </div>
                 <div class="mt-16">
                     <a href="https://www.americanscientist.org/article/the-braess-paradox" target="_blank" class="text-sm group" style="color: var(--text-secondary);">
                        Magbasa pa ng mga kaugnay na pag-aaral 
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="inline-block -translate-y-px transition-transform group-hover:translate-x-1"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
                    </a>
                </div>
            </div>
        </section>
        
        <footer class="text-center py-12 border-t" style="color: var(--text-secondary); border-color: var(--border-color);">
            <div class="container mx-auto px-6">
                <p class="font-bold">12 - ZARA</p>
                <p class="text-sm mt-2">ABRIGO, CALLEJA, CASIANO, ARGUIL, MACOPIA</p>
                <p class="text-xs mt-8">&copy; 2025 DAAN DAAN Initiative. All rights reserved.</p>
            </div>
        </footer>
    </main>

    <!-- Back to Top Button -->
    <a href="#" id="back-to-top" aria-label="Back to Top" class="fixed bottom-8 right-8 w-12 h-12 rounded-full flex items-center justify-center shadow-lg opacity-0 pointer-events-none transition-all duration-300" style="background-color: var(--card-bg); backdrop-filter: blur(10px);">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m18 15-6-6-6 6"/></svg>
    </a>

    <!-- Cookie Consent Banner -->
    <div id="cookie-banner" class="fixed bottom-0 left-0 right-0 p-4 transform translate-y-full transition-transform duration-500 ease-in-out z-50">
        <div class="max-w-4xl mx-auto p-4 rounded-xl flex flex-col sm:flex-row items-center justify-between gap-4 text-sm" style="background-color: var(--card-bg); backdrop-filter: blur(10px); border: 1px solid var(--border-color);">
            <p style="color: var(--text-secondary);">Gumagamit kami ng cookies para mapabuti ang iyong karanasan. Sa pagpapatuloy, sumasang-ayon ka sa aming paggamit ng cookies.</p>
            <div class="flex items-center gap-4 flex-shrink-0">
                <a href="#" class="font-semibold hover:opacity-70 transition-opacity" style="color: var(--text-secondary);">Matuto Pa</a>
                <button id="accept-cookies" class="px-5 py-2 rounded-full font-semibold" style="background-color: var(--text-primary); color: var(--bg-color);">Tanggapin</button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Sidebar Logic
            const sidebarTrigger = document.getElementById('sidebar-trigger');
            const sidebar = document.getElementById('sidebar');
            const sidebarOverlay = document.getElementById('sidebar-overlay');
            function openSidebar() {
                sidebar.classList.remove('-translate-x-full');
                sidebarOverlay.classList.remove('opacity-0', 'pointer-events-none');
            }
            function closeSidebar() {
                sidebar.classList.add('-translate-x-full');
                sidebarOverlay.classList.add('opacity-0', 'pointer-events-none');
            }
            sidebarTrigger.addEventListener('click', (e) => { e.stopPropagation(); openSidebar(); });
            sidebarOverlay.addEventListener('click', closeSidebar);

            // Theme Toggle
            const themeToggle = document.getElementById('theme-toggle');
            const sunIcon = document.getElementById('sun-icon');
            const moonIcon = document.getElementById('moon-icon');
            const applyTheme = (isDark) => {
                if (isDark) {
                    document.documentElement.classList.add('dark');
                    sunIcon.classList.remove('hidden'); moonIcon.classList.add('hidden');
                } else {
                    document.documentElement.classList.remove('dark');
                    sunIcon.classList.add('hidden'); moonIcon.classList.remove('hidden');
                }
            };
            let isDarkMode = localStorage.getItem('theme') === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches);
            applyTheme(isDarkMode);
            themeToggle.addEventListener('click', () => {
                isDarkMode = !isDarkMode;
                localStorage.setItem('theme', isDarkMode ? 'dark' : 'light');
                applyTheme(isDarkMode);
            });
            
            // Header Scroll Logic
            const header = document.getElementById('header');
            let lastScrollY = window.scrollY;
            if (header) {
                window.addEventListener('scroll', () => {
                    if (window.scrollY > lastScrollY && window.scrollY > 100) {
                        header.classList.add('header-hidden');
                    } else {
                        header.classList.remove('header-hidden');
                    }
                    lastScrollY = window.scrollY;
                });
            }

            // Braess' Paradox
            const toggleShortcutBtn = document.getElementById('toggle-shortcut');
            const paradoxContainer = document.getElementById('paradox-container');
            const travelTimeEl = document.getElementById('travel-time');
            let isShortcutAdded = false;
            toggleShortcutBtn.addEventListener('click', () => {
                isShortcutAdded = !isShortcutAdded;
                paradoxContainer.classList.toggle('shortcut-visible', isShortcutAdded);
                travelTimeEl.textContent = isShortcutAdded ? '60 minuto' : '45 minuto';
                travelTimeEl.classList.toggle('text-red-500', isShortcutAdded);
                travelTimeEl.classList.toggle('text-green-500', !isShortcutAdded);
                toggleShortcutBtn.textContent = isShortcutAdded ? 'Alisin ang Shortcut' : 'Idagdag ang Shortcut';
            });

            // Results Section
            const researchData = {
                alabang: { title: "Resulta para sa Alabang", initialTime: "44,730.54 min", finalTime: "43,386.63 min", pValue: "p < .001 (t-statistic: 6.29)", roads: [ { name: "Ilaya Street", saved: 1343.90 }, { name: "Parkway Place", saved: 593.89 }, { name: "Corporate Avenue", saved: 575.96 }, { name: "Parkway Avenue", saved: 553.91 }, { name: "Corporate Avenue", saved: 541.87 }, { name: "Corporate Avenue", saved: 537.74 }, { name: "Corporate Avenue", saved: 400.12 }, { name: "Parkway Avenue", saved: 397.57 }, { name: "Corporate Avenue", saved: 374.71 }, { name: "Corporate Avenue", saved: 373.08 } ] },
                portarea: { title: "Resulta para sa Port Area", initialTime: "869.21 min", finalTime: "832.27 min", pValue: "p < .001 (t-statistic: 15.67)", roads: [ { name: "Main Road 2", saved: 36.94 }, { name: "Newsite Road", saved: 30.27 }, { name: "Newsite Road", saved: 30.05 }, { name: "Main Road 2", saved: 28.79 }, { name: "Main Road 2", saved: 26.39 }, { name: "Newsite Road", saved: 26.02 }, { name: "Newsite Road", saved: 25.74 }, { name: "Newsite Road", saved: 25.74 }, { name: "Main Road 2", saved: 22.53 }, { name: "Newsite Road", saved: 18.62 } ] }
            };
            const resultTitle = document.getElementById('result-title');
            const initialTimeEl = document.getElementById('initial-time');
            const finalTimeEl = document.getElementById('final-time');
            const pValueEl = document.getElementById('p-value');
            const roadListEl = document.getElementById('road-list');
            const btnAlabang = document.getElementById('btn-alabang');
            const btnPortArea = document.getElementById('btn-portarea');
            function updateResults(location) {
                const data = researchData[location];
                resultTitle.textContent = data.title;
                initialTimeEl.textContent = data.initialTime;
                finalTimeEl.textContent = data.finalTime;
                pValueEl.textContent = data.pValue;
                roadListEl.innerHTML = '';
                const maxSaved = Math.max(...data.roads.map(r => r.saved));
                data.roads.forEach(road => {
                    const li = document.createElement('li');
                    li.className = 'flex justify-between items-center gap-4 text-sm';
                    li.innerHTML = `<span class="flex-shrink-0">${road.name}</span><div class="w-full bg-gray-800 rounded-full h-2.5"><div class="gradient-bg h-2.5 rounded-full" style="width: ${ (road.saved / maxSaved) * 100}%"></div></div><span class="font-bold w-20 text-right">${road.saved.toFixed(2)}</span>`;
                    roadListEl.appendChild(li);
                });
            }
            function updateLocationButtons(activeLocation) {
                [btnAlabang, btnPortArea].forEach(button => {
                    button.classList.toggle('gradient-bg', button.id.includes(activeLocation));
                    button.classList.toggle('text-white', button.id.includes(activeLocation));
                    button.classList.toggle('active', button.id.includes(activeLocation));
                    button.classList.toggle('bg-transparent', !button.id.includes(activeLocation));
                    button.style.color = button.id.includes(activeLocation) ? 'white' : 'var(--text-secondary)';
                });
            }
            btnAlabang.addEventListener('click', () => { updateResults('alabang'); updateLocationButtons('alabang'); });
            btnPortArea.addEventListener('click', () => { updateResults('portarea'); updateLocationButtons('portarea'); });
            updateResults('alabang');
            updateLocationButtons('alabang');
            
            // Gantt Chart
            const ganttContainer = document.getElementById('gantt-chart-container');
            const timelineData = [
                { task: 'Discovery & Planning', start: 1, end: 3 },
                { task: 'System Architecture & Design', start: 2, end: 4 },
                { task: 'Core Feature Development', start: 3, end: 6 },
                { task: 'Data Simulation & Analysis', start: 6, end: 8 },
                { task: 'Final Deliverables', start: 7, end: 9 }
            ];
            function createGanttChart() {
                let chartHTML = `<div class="gantt-container"><div></div><div class="gantt-header">${Array.from({length: 8}, (_, i) => `<span>W${i+1}</span>`).join('')}</div>`;
                timelineData.forEach((item, index) => {
                    chartHTML += `<div class="gantt-row"><div class="gantt-task-name">${item.task}</div><div class="gantt-grid"><div class="gantt-bar gradient-bg" style="--start-week: ${item.start}; --end-week: ${item.end}; --delay: ${index * 0.1}s"></div></div></div>`;
                });
                ganttContainer.innerHTML = chartHTML + `</div>`;
            }
            createGanttChart();

            // Scroll Fade-in
            const sections = document.querySelectorAll('.section-fade-in');
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => { if (entry.isIntersecting) entry.target.classList.add('is-visible'); });
            }, { threshold: 0.1 });
            sections.forEach(section => observer.observe(section));

            // Background circle scroll
            const circles = document.querySelectorAll('.circle-blur');
            window.addEventListener('scroll', () => {
                const scrollY = window.scrollY;
                const pageHeight = document.body.scrollHeight - window.innerHeight;
                const scrollPercent = scrollY / pageHeight;
                circles.forEach((circle, index) => {
                    const x = (scrollPercent - 0.5) * 200 * (index % 2 === 0 ? 1 : -1);
                    const y = Math.sin(scrollPercent * Math.PI) * 100;
                    circle.style.transform = `translateX(${x}px) translateY(${y}px)`;
                });
            });

            // Back to Top
            const backToTopBtn = document.getElementById('back-to-top');
            window.addEventListener('scroll', () => {
                backToTopBtn.classList.toggle('opacity-0', window.scrollY < 300);
                backToTopBtn.classList.toggle('pointer-events-none', window.scrollY < 300);
            });

            // Cookie Consent
            const cookieBanner = document.getElementById('cookie-banner');
            const acceptCookiesBtn = document.getElementById('accept-cookies');
            if (!localStorage.getItem('cookie_consent')) {
                setTimeout(() => { cookieBanner.classList.remove('translate-y-full'); }, 1000);
            }
            acceptCookiesBtn.addEventListener('click', () => {
                localStorage.setItem('cookie_consent', 'true');
                cookieBanner.classList.add('translate-y-full');
            });
        });
    </script>
</body>
</html>

