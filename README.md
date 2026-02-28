<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KACCI FX | Pro Trading Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --neon-cyan: #00f3ff;
            --neon-pink: #ff00ff;
            --neon-gold: #ffd700;
            --dark-bg: #0a0a0f;
            --panel-bg: rgba(20, 20, 30, 0.8);
        }
        
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Rajdhani', sans-serif;
            background: var(--dark-bg);
            color: #e0e0e0;
            overflow-x: hidden;
        }
        
        .brand-font { font-family: 'Orbitron', sans-serif; }
        
        .glitch {
            position: relative;
            animation: glitch-skew 1s infinite linear alternate-reverse;
        }
        
        .glitch::before, .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
        }
        
        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 var(--neon-pink);
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }
        
        .glitch::after {
            left: -2px;
            text-shadow: -2px 0 var(--neon-cyan);
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }
        
        @keyframes glitch-anim {
            0% { clip: rect(31px, 9999px, 94px, 0); }
            20% { clip: rect(70px, 9999px, 19px, 0); }
            40% { clip: rect(15px, 9999px, 83px, 0); }
            60% { clip: rect(89px, 9999px, 11px, 0); }
            80% { clip: rect(43px, 9999px, 76px, 0); }
            100% { clip: rect(62px, 9999px, 34px, 0); }
        }
        
        @keyframes glitch-anim2 {
            0% { clip: rect(65px, 9999px, 99px, 0); }
            20% { clip: rect(12px, 9999px, 54px, 0); }
            40% { clip: rect(88px, 9999px, 23px, 0); }
            60% { clip: rect(34px, 9999px, 67px, 0); }
            80% { clip: rect(91px, 9999px, 45px, 0); }
            100% { clip: rect(56px, 9999px, 12px, 0); }
        }
        
        @keyframes glitch-skew {
            0% { transform: skew(0deg); }
            10% { transform: skew(-2deg); }
            20% { transform: skew(2deg); }
            30% { transform: skew(0deg); }
            100% { transform: skew(0deg); }
        }
        
        .neon-border {
            box-shadow: 0 0 10px rgba(0, 243, 255, 0.3), inset 0 0 10px rgba(0, 243, 255, 0.1);
            border: 1px solid rgba(0, 243, 255, 0.5);
        }
        
        .neon-gold-border {
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.4), inset 0 0 15px rgba(255, 215, 0, 0.1);
            border: 1px solid rgba(255, 215, 0, 0.6);
        }
        
        .grid-bg {
            background-image: linear-gradient(rgba(0, 243, 255, 0.03) 1px, transparent 1px),
                              linear-gradient(90deg, rgba(0, 243, 255, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            animation: grid-move 20s linear infinite;
        }
        
        @keyframes grid-move {
            0% { transform: translate(0, 0); }
            100% { transform: translate(50px, 50px); }
        }
        
        .live-pulse { animation: pulse-ring 2s cubic-bezier(0.215, 0.61, 0.355, 1) infinite; }
        
        @keyframes pulse-ring {
            0% { box-shadow: 0 0 0 0 rgba(0, 243, 255, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(0, 243, 255, 0); }
            100% { box-shadow: 0 0 0 0 rgba(0, 243, 255, 0); }
        }
        
        .glass-panel {
            background: var(--panel-bg);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .up-flash { animation: flash-green 0.5s; }
        .down-flash { animation: flash-red 0.5s; }
        
        @keyframes flash-green {
            0% { background-color: rgba(0, 255, 0, 0.3); }
            100% { background-color: transparent; }
        }
        
        @keyframes flash-red {
            0% { background-color: rgba(255, 0, 0, 0.3); }
            100% { background-color: transparent; }
        }
        
        .login-screen {
            position: fixed;
            inset: 0;
            background: linear-gradient(135deg, #0a0a0f 0%, #1a1a2e 50%, #0a0a0f 100%);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .login-container {
            width: 100%;
            max-width: 1200px;
            height: 100vh;
            display: flex;
        }
        
        .login-left {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 4rem;
        }
        
        .login-right {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 4rem;
            background: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
        }
        
        .login-form { width: 100%; max-width: 400px; }
        
        .input-group {
            position: relative;
            margin-bottom: 1.5rem;
        }
        
        .input-group input {
            width: 100%;
            padding: 1rem 1rem 1rem 3rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(0, 243, 255, 0.3);
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: var(--neon-cyan);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.3);
        }
        
        .login-btn {
            width: 100%;
            padding: 1rem;
            background: linear-gradient(45deg, var(--neon-cyan), var(--neon-pink));
            border: none;
            border-radius: 8px;
            color: white;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }
        
        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(0, 243, 255, 0.4);
        }
        
        .hidden { display: none !important; }
        .fade-out { animation: fadeOut 0.5s forwards; }
        
        @keyframes fadeOut {
            to { opacity: 0; visibility: hidden; }
        }
        
        .dashboard { display: none; }
        .dashboard.active { display: block; }
        
        /* Secret Gold Section Styles */
        .gold-section {
            background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(0, 0, 0, 0.8));
            border: 2px solid var(--neon-gold);
        }
        
        /* Sentiment Game Styles */
        .sentiment-card {
            transition: all 0.3s;
            cursor: pointer;
        }
        
        .sentiment-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0, 243, 255, 0.3);
        }
        
        .sentiment-card.selected {
            border-color: var(--neon-cyan);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.5);
        }
        
        .streak-flame {
            animation: flicker 1s infinite alternate;
        }
        
        @keyframes flicker {
            0% { opacity: 1; transform: scale(1); }
            100% { opacity: 0.8; transform: scale(1.1); }
        }
        
        .progress-ring {
            transform: rotate(-90deg);
        }
        
        .progress-ring-circle {
            transition: stroke-dashoffset 0.5s;
        }
        
        .ticker-wrap {
            overflow: hidden;
            white-space: nowrap;
        }
        
        .ticker {
            display: inline-block;
            animation: ticker 30s linear infinite;
        }
        
        @keyframes ticker {
            0% { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }
        
        ::-webkit-scrollbar { width: 8px; height: 8px; }
        ::-webkit-scrollbar-track { background: #0a0a0f; }
        ::-webkit-scrollbar-thumb { background: var(--neon-cyan); border-radius: 4px; }
    </style>
</head>
<body class="grid-bg">

    <!-- LOGIN SCREEN -->
    <div id="login-screen" class="login-screen">
        <div class="login-container">
            <div class="login-left">
                <div class="mb-8">
                    <h1 class="text-6xl font-black brand-font mb-2 glitch" data-text="KACCI FX">
                        <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-purple-500 to-pink-500">KACCI FX</span>
                    </h1>
                    <p class="text-xl text-gray-400 tracking-widest uppercase">Professional Trading Terminal</p>
                </div>
                
                <div class="space-y-4">
                    <div class="flex items-center gap-4 opacity-0" style="animation: slideIn 0.5s forwards 0.5s;">
                        <div class="w-12 h-12 rounded-full bg-cyan-500/20 flex items-center justify-center text-cyan-400">📊</div>
                        <div>
                            <h3 class="font-bold text-cyan-400">Market Sentiment Game</h3>
                            <p class="text-sm text-gray-400">Build consistency streaks & earn rewards</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-4 opacity-0" style="animation: slideIn 0.5s forwards 0.7s;">
                        <div class="w-12 h-12 rounded-full bg-yellow-500/20 flex items-center justify-center text-yellow-400">🥇</div>
                        <div>
                            <h3 class="font-bold text-yellow-400">Secret Gold Vault</h3>
                            <p class="text-sm text-gray-400">Real-time XAU/USD tracking</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="login-right">
                <div class="login-form">
                    <h2 class="text-3xl font-bold brand-font mb-2 text-white">Welcome Back</h2>
                    <p class="text-gray-400 mb-8">Sign in to access your terminal</p>
                    
                    <form id="login-form" onsubmit="handleLogin(event)">
                        <div class="input-group">
                            <svg class="w-5 h-5 absolute left-3 top-1/2 transform -translate-y-1/2 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
                            </svg>
                            <input type="text" id="username" placeholder="Username" required value="trader">
                        </div>
                        
                        <div class="input-group">
                            <svg class="w-5 h-5 absolute left-3 top-1/2 transform -translate-y-1/2 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path>
                            </svg>
                            <input type="password" id="password" placeholder="Password" required value="kacci2024">
                        </div>
                        
                        <button type="submit" class="login-btn">ACCESS TERMINAL</button>
                    </form>
                    
                    <div class="mt-6 text-center">
                        <button onclick="demoLogin()" class="text-cyan-400 hover:text-cyan-300 text-sm">Quick Demo Access</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- MAIN DASHBOARD -->
    <div id="dashboard" class="dashboard">
        <!-- Header -->
        <header class="fixed top-0 w-full z-50 glass-panel border-b border-cyan-500/30">
            <div class="container mx-auto px-4 py-3 flex justify-between items-center">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 bg-gradient-to-br from-cyan-500 to-purple-600 rounded-lg flex items-center justify-center font-bold text-xl brand-font animate-pulse">K</div>
                    <h1 class="text-2xl font-bold brand-font glitch" data-text="KACCI FX">
                        <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-purple-500 to-pink-500">KACCI FX</span>
                    </h1>
                </div>
                
                <div class="flex items-center gap-4">
                    <!-- Streak Counter -->
                    <div class="hidden md:flex items-center gap-2 px-3 py-1 bg-orange-500/20 border border-orange-500/50 rounded-full">
                        <span class="text-2xl streak-flame">🔥</span>
                        <div class="text-right">
                            <div class="text-xs text-orange-400 uppercase font-bold">Streak</div>
                            <div class="text-lg font-bold text-orange-400 leading-none" id="streak-count">0</div>
                        </div>
                    </div>
                    
                    <div id="clock" class="text-xl font-mono text-cyan-400 brand-font"></div>
                    
                    <!-- Navigation -->
                    <nav class="hidden md:flex gap-2">
                        <button onclick="showSection('forex')" class="px-4 py-2 rounded-lg bg-cyan-500/20 text-cyan-400 hover:bg-cyan-500/30 transition-colors text-sm font-bold">FOREX</button>
                        <button onclick="showSection('sentiment')" class="px-4 py-2 rounded-lg bg-purple-500/20 text-purple-400 hover:bg-purple-500/30 transition-colors text-sm font-bold">SENTIMENT</button>
                        <button onclick="showSection('gold')" class="px-4 py-2 rounded-lg bg-yellow-500/20 text-yellow-400 hover:bg-yellow-500/30 transition-colors text-sm font-bold border border-yellow-500/50">🥇 GOLD</button>
                    </nav>
                    
                    <button onclick="logout()" class="p-2 hover:bg-white/10 rounded-lg text-gray-400 hover:text-white">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"></path>
                        </svg>
                    </button>
                </div>
            </div>
        </header>

        <!-- Ticker -->
        <div class="fixed top-16 w-full bg-black/80 border-b border-cyan-500/20 z-40 py-2 ticker-wrap">
            <div class="ticker text-sm font-mono" id="ticker-tape"></div>
        </div>

        <!-- MAIN CONTENT -->
        <main class="container mx-auto px-4 pt-24 pb-8">
            
            <!-- SENTIMENT GAME SECTION -->
            <section id="sentiment-section" class="mb-8">
                <div class="glass-panel rounded-xl p-6 neon-border mb-6">
                    <div class="flex justify-between items-center mb-6">
                        <div>
                            <h2 class="text-2xl font-bold brand-font text-purple-400">Market Sentiment Challenge</h2>
                            <p class="text-gray-400 text-sm">Read the market. Make your call. Build your streak.</p>
                        </div>
                        <div class="flex items-center gap-4">
                            <div class="text-right">
                                <div class="text-xs text-gray-400">Daily Challenge</div>
                                <div class="text-2xl font-bold text-cyan-400" id="sentiment-score">0/3</div>
                            </div>
                            <div class="w-16 h-16 relative">
                                <svg class="progress-ring w-16 h-16">
                                    <circle class="text-gray-700" stroke-width="4" stroke="currentColor" fill="transparent" r="28" cx="32" cy="32"/>
                                    <circle id="progress-circle" class="text-cyan-400 progress-ring-circle" stroke-width="4" stroke-linecap="round" stroke="currentColor" fill="transparent" r="28" cx="32" cy="32" 
                                            stroke-dasharray="175.9" stroke-dashoffset="175.9"/>
                                </svg>
                                <div class="absolute inset-0 flex items-center justify-center text-xs font-bold" id="accuracy-display">0%</div>
                            </div>
                        </div>
                    </div>

                    <!-- Current Sentiment Display -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                        <div class="glass-panel rounded-lg p-4 text-center border border-red-500/30 bg-red-500/5">
                            <div class="text-3xl mb-2">😱</div>
                            <div class="text-red-400 font-bold">FEAR</div>
                            <div class="text-xs text-gray-400">0-39 Index</div>
                            <div class="text-2xl font-bold text-red-400 mt-2" id="fear-value">--</div>
                        </div>
                        <div class="glass-panel rounded-lg p-4 text-center border border-yellow-500/30 bg-yellow-500/5">
                            <div class="text-3xl mb-2">😑</div>
                            <div class="text-yellow-400 font-bold">NEUTRAL</div>
                            <div class="text-xs text-gray-400">40-60 Index</div>
                            <div class="text-2xl font-bold text-yellow-400 mt-2" id="neutral-value">--</div>
                        </div>
                        <div class="glass-panel rounded-lg p-4 text-center border border-green-500/30 bg-green-500/5">
                            <div class="text-3xl mb-2">🚀</div>
                            <div class="text-green-400 font-bold">GREED</div>
                            <div class="text-xs text-gray-400">61-100 Index</div>
                            <div class="text-2xl font-bold text-green-400 mt-2" id="greed-value">--</div>
                        </div>
                    </div>

                    <!-- Game Area -->
                    <div id="game-area" class="glass-panel rounded-lg p-6 bg-gradient-to-r from-purple-900/20 to-cyan-900/20 border border-purple-500/30">
                        <div class="text-center mb-4">
                            <span class="text-xs uppercase tracking-wider text-purple-400">Current Market Sentiment</span>
                            <div class="text-4xl font-black brand-font text-white my-2" id="current-sentiment">LOADING...</div>
                            <div class="text-sm text-gray-400" id="sentiment-description">--</div>
                        </div>
                        
                        <div class="grid grid-cols-3 gap-4 mt-6">
                            <button onclick="makeSentimentCall('fear')" class="sentiment-card p-4 rounded-lg bg-red-500/10 border border-red-500/30 hover:bg-red-500/20 text-center group">
                                <div class="text-2xl mb-2 group-hover:scale-110 transition-transform">📉</div>
                                <div class="text-red-400 font-bold">Will Drop</div>
                                <div class="text-xs text-gray-500">Fear Increases</div>
                            </button>
                            <button onclick="makeSentimentCall('neutral')" class="sentiment-card p-4 rounded-lg bg-yellow-500/10 border border-yellow-500/30 hover:bg-yellow-500/20 text-center group">
                                <div class="text-2xl mb-2 group-hover:scale-110 transition-transform">➡️</div>
                                <div class="text-yellow-400 font-bold">Stays Same</div>
                                <div class="text-xs text-gray-500">Neutral</div>
                            </button>
                            <button onclick="makeSentimentCall('greed')" class="sentiment-card p-4 rounded-lg bg-green-500/10 border border-green-500/30 hover:bg-green-500/20 text-center group">
                                <div class="text-2xl mb-2 group-hover:scale-110 transition-transform">📈</div>
                                <div class="text-green-400 font-bold">Will Rise</div>
                                <div class="text-xs text-gray-500">Greed Increases</div>
                            </button>
                        </div>

                        <div id="game-result" class="mt-4 text-center hidden">
                            <div class="text-2xl mb-2" id="result-emoji"></div>
                            <div class="text-lg font-bold" id="result-text"></div>
                        </div>
                    </div>

                    <!-- Consistency Stats -->
                    <div class="grid grid-cols-3 gap-4 mt-4">
                        <div class="glass-panel rounded-lg p-3 text-center">
                            <div class="text-xs text-gray-400">Current Streak</div>
                            <div class="text-2xl font-bold text-orange-400 streak-flame" id="current-streak">0 🔥</div>
                        </div>
                        <div class="glass-panel rounded-lg p-3 text-center">
                            <div class="text-xs text-gray-400">Best Streak</div>
                            <div class="text-2xl font-bold text-cyan-400" id="best-streak">0</div>
                        </div>
                        <div class="glass-panel rounded-lg p-3 text-center">
                            <div class="text-xs text-gray-400">Accuracy</div>
                            <div class="text-2xl font-bold text-green-400" id="total-accuracy">0%</div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- FOREX SECTION -->
            <section id="forex-section">
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    <div class="lg:col-span-2 space-y-6">
                        <div class="glass-panel rounded-xl p-6 neon-border">
                            <div class="flex justify-between items-center mb-4">
                                <h2 class="text-xl font-bold brand-font text-cyan-400">Major Forex Pairs</h2>
                                <button onclick="refreshForex()" class="px-3 py-1 text-xs bg-cyan-500/20 text-cyan-400 rounded hover:bg-cyan-500/30">REFRESH</button>
                            </div>
                            <div class="grid grid-cols-2 md:grid-cols-3 gap-4" id="forex-grid"></div>
                        </div>

                        <div class="glass-panel rounded-xl p-6 neon-border">
                            <h2 class="text-xl font-bold brand-font text-purple-400 mb-4">Market Movers</h2>
                            <div class="space-y-3" id="movers-list"></div>
                        </div>
                    </div>

                    <div class="space-y-6">
                        <div class="glass-panel rounded-xl p-6 neon-border border-green-500/30">
                            <h2 class="text-lg font-bold brand-font text-green-400 mb-4">Account Summary</h2>
                            <div class="space-y-3">
                                <div class="flex justify-between items-center">
                                    <span class="text-gray-400">Balance</span>
                                    <span class="text-2xl font-mono text-green-400">$50,000</span>
                                </div>
                                <div class="flex justify-between items-center">
                                    <span class="text-gray-400">Open P/L</span>
                                    <span class="text-lg font-mono text-green-400">+$2,450</span>
                                </div>
                            </div>
                        </div>

                        <div class="glass-panel rounded-xl p-6 neon-border border-yellow-500/30">
                            <h2 class="text-lg font-bold brand-font text-yellow-400 mb-4">Swing Opportunities</h2>
                            <div id="swing-opportunities" class="space-y-3"></div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- SECRET GOLD SECTION -->
            <section id="gold-section" class="hidden">
                <div class="glass-panel rounded-xl p-8 neon-gold-border gold-section mb-6">
                    <div class="flex justify-between items-center mb-6">
                        <div class="flex items-center gap-3">
                            <span class="text-4xl">🥇</span>
                            <div>
                                <h2 class="text-3xl font-black brand-font text-yellow-400">GOLD VAULT</h2>
                                <p class="text-yellow-600 text-sm">XAU/USD Real-Time Tracking</p>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="text-xs text-yellow-600 uppercase">Live Price</div>
                            <div class="text-4xl font-mono font-bold text-yellow-400" id="gold-price">--</div>
                            <div class="text-sm" id="gold-change">--</div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
                        <div class="glass-panel rounded-lg p-4 bg-yellow-500/5 border border-yellow-500/20">
                            <div class="text-xs text-yellow-600 mb-1">24h High</div>
                            <div class="text-xl font-mono text-yellow-400" id="gold-high">--</div>
                        </div>
                        <div class="glass-panel rounded-lg p-4 bg-yellow-500/5 border border-yellow-500/20">
                            <div class="text-xs text-yellow-600 mb-1">24h Low</div>
                            <div class="text-xl font-mono text-yellow-400" id="gold-low">--</div>
                        </div>
                        <div class="glass-panel rounded-lg p-4 bg-yellow-500/5 border border-yellow-500/20">
                            <div class="text-xs text-yellow-600 mb-1">24h Volume</div>
                            <div class="text-xl font-mono text-yellow-400" id="gold-volume">--</div>
                        </div>
                        <div class="glass-panel rounded-lg p-4 bg-yellow-500/5 border border-yellow-500/20">
                            <div class="text-xs text-yellow-600 mb-1">Market Cap</div>
                            <div class="text-xl font-mono text-yellow-400">$12.4T</div>
                        </div>
                    </div>

                    <canvas id="goldChart" height="300"></canvas>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="glass-panel rounded-xl p-6 neon-gold-border">
                        <h3 class="text-lg font-bold text-yellow-400 mb-4">Gold Alerts</h3>
                        <div class="space-y-3">
                            <div class="flex items-center justify-between p-3 bg-yellow-500/10 rounded-lg border border-yellow-500/30">
                                <div>
                                    <div class="text-yellow-400 font-bold">Price Target</div>
                                    <div class="text-xs text-gray-400">Alert when XAU/USD hits</div>
                                </div>
                                <div class="text-2xl font-mono text-yellow-400">$2,100</div>
                            </div>
                            <div class="flex items-center justify-between p-3 bg-yellow-500/10 rounded-lg border border-yellow-500/30">
                                <div>
                                    <div class="text-yellow-400 font-bold">Support Level</div>
                                    <div class="text-xs text-gray-400">Strong support at</div>
                                </div>
                                <div class="text-2xl font-mono text-yellow-400">$2,035</div>
                            </div>
                        </div>
                    </div>

                    <div class="glass-panel rounded-xl p-6 neon-gold-border">
                        <h3 class="text-lg font-bold text-yellow-400 mb-4">Gold Sentiment</h3>
                        <div class="flex items-center justify-center h-32">
                            <div class="text-center">
                                <div class="text-5xl mb-2">🐂</div>
                                <div class="text-xl font-bold text-green-400">Bullish</div>
                                <div class="text-sm text-gray-400">72% of traders long</div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <script>
        // Configuration
        let config = {
            volatilityThreshold: 1.0,
            refreshInterval: 5000,
            currentUser: null
        };

        // Game State
        let gameState = {
            streak: parseInt(localStorage.getItem('kacci_streak') || '0'),
            bestStreak: parseInt(localStorage.getItem('kacci_best_streak') || '0'),
            totalCalls: parseInt(localStorage.getItem('kacci_total_calls') || '0'),
            correctCalls: parseInt(localStorage.getItem('kacci_correct_calls') || '0'),
            dailyScore: 0,
            lastPlayed: localStorage.getItem('kacci_last_played') || null,
            currentSentiment: null
        };

        // State
        let forexData = {};
        let previousRates = {};
        let goldChart;
        let sentimentChart;

        // Initialize
        function initDashboard() {
            initClock();
            fetchForexData();
            fetchGoldData();
            fetchSentimentData();
            fetchMarketMovers();
            generateSwingOpportunities();
            updateStreakDisplay();
            
            setInterval(fetchForexData, config.refreshInterval);
            setInterval(fetchGoldData, 30000); // Gold updates every 30s
            setInterval(initClock, 1000);
        }

        // Clock
        function initClock() {
            const now = new Date();
            document.getElementById('clock').textContent = now.toISOString().split('T')[1].split('.')[0] + ' UTC';
        }

        // Login Handler
        function handleLogin(e) {
            e.preventDefault();
            login(document.getElementById('username').value);
        }

        function demoLogin() {
            login('DemoTrader');
        }

        function login(username) {
            config.currentUser = username;
            document.getElementById('login-screen').classList.add('fade-out');
            setTimeout(() => {
                document.getElementById('login-screen').classList.add('hidden');
                document.getElementById('dashboard').classList.add('active');
                initDashboard();
            }, 500);
        }

        function logout() {
            location.reload();
        }

        // Section Navigation
        function showSection(section) {
            document.getElementById('forex-section').classList.add('hidden');
            document.getElementById('sentiment-section').classList.add('hidden');
            document.getElementById('gold-section').classList.add('hidden');
            
            if (section === 'forex') {
                document.getElementById('forex-section').classList.remove('hidden');
            } else if (section === 'sentiment') {
                document.getElementById('sentiment-section').classList.remove('hidden');
            } else if (section === 'gold') {
                document.getElementById('gold-section').classList.remove('hidden');
                if (!goldChart) initGoldChart();
            }
        }

        // SENTIMENT GAME FUNCTIONS
        async function fetchSentimentData() {
            try {
                // Free Fear & Greed API from Alternative.me [^24^]
                const response = await fetch('https://api.alternative.me/fng/?limit=1');
                const data = await response.json();
                
                if (data.data && data.data[0]) {
                    const sentiment = data.data[0];
                    const value = parseInt(sentiment.value);
                    const classification = sentiment.value_classification;
                    
                    gameState.currentSentiment = { value, classification };
                    
                    // Update display
                    document.getElementById('current-sentiment').textContent = value;
                    document.getElementById('sentiment-description').textContent = classification;
                    
                    // Update category values
                    document.getElementById('fear-value').textContent = value < 40 ? value : '--';
                    document.getElementById('neutral-value').textContent = (value >= 40 && value <= 60) ? value : '--';
                    document.getElementById('greed-value').textContent = value > 60 ? value : '--';
                    
                    // Color coding
                    const sentimentEl = document.getElementById('current-sentiment');
                    sentimentEl.className = 'text-4xl font-black brand-font my-2 ' + 
                        (value < 40 ? 'text-red-400' : value > 60 ? 'text-green-400' : 'text-yellow-400');
                }
            } catch (error) {
                console.error('Sentiment fetch error:', error);
                // Fallback values
                document.getElementById('current-sentiment').textContent = '45';
                document.getElementById('sentiment-description').textContent = 'Neutral';
            }
        }

        function makeSentimentCall(prediction) {
            if (!gameState.currentSentiment) return;
            
            const currentValue = gameState.currentSentiment.value;
            let actual;
            if (currentValue < 40) actual = 'fear';
            else if (currentValue > 60) actual = 'greed';
            else actual = 'neutral';
            
            const correct = prediction === actual;
            
            // Update stats
            gameState.totalCalls++;
            if (correct) {
                gameState.correctCalls++;
                gameState.streak++;
                if (gameState.streak > gameState.bestStreak) {
                    gameState.bestStreak = gameState.streak;
                }
                gameState.dailyScore++;
            } else {
                gameState.streak = 0;
            }
            
            // Save to localStorage
            localStorage.setItem('kacci_streak', gameState.streak);
            localStorage.setItem('kacci_best_streak', gameState.bestStreak);
            localStorage.setItem('kacci_total_calls', gameState.totalCalls);
            localStorage.setItem('kacci_correct_calls', gameState.correctCalls);
            localStorage.setItem('kacci_last_played', new Date().toDateString());
            
            // Show result
            const resultDiv = document.getElementById('game-result');
            const resultEmoji = document.getElementById('result-emoji');
            const resultText = document.getElementById('result-text');
            
            resultDiv.classList.remove('hidden');
            if (correct) {
                resultEmoji.textContent = '🎉';
                resultText.textContent = 'Correct! Streak +1';
                resultText.className = 'text-lg font-bold text-green-400';
            } else {
                resultEmoji.textContent = '❌';
                resultText.textContent = 'Wrong! Streak reset';
                resultText.className = 'text-lg font-bold text-red-400';
            }
            
            updateStreakDisplay();
            updateProgressRing();
            
            // Disable buttons temporarily
            document.querySelectorAll('.sentiment-card').forEach(btn => {
                btn.disabled = true;
                btn.style.opacity = '0.5';
            });
            
            // Re-enable after 3 seconds
            setTimeout(() => {
                resultDiv.classList.add('hidden');
                document.querySelectorAll('.sentiment-card').forEach(btn => {
                    btn.disabled = false;
                    btn.style.opacity = '1';
                });
                fetchSentimentData(); // Get new data
            }, 3000);
        }

        function updateStreakDisplay() {
            document.getElementById('streak-count').textContent = gameState.streak;
            document.getElementById('current-streak').textContent = gameState.streak + ' 🔥';
            document.getElementById('best-streak').textContent = gameState.bestStreak;
            
            const accuracy = gameState.totalCalls > 0 ? 
                Math.round((gameState.correctCalls / gameState.totalCalls) * 100) : 0;
            document.getElementById('total-accuracy').textContent = accuracy + '%';
            document.getElementById('accuracy-display').textContent = accuracy + '%';
        }

        function updateProgressRing() {
            const circle = document.getElementById('progress-circle');
            const radius = circle.r.baseVal.value;
            const circumference = radius * 2 * Math.PI;
            const percent = Math.min(gameState.dailyScore / 3, 1);
            const offset = circumference - (percent * circumference);
            
            circle.style.strokeDashoffset = offset;
            document.getElementById('sentiment-score').textContent = gameState.dailyScore + '/3';
        }

        // GOLD FUNCTIONS
        async function fetchGoldData() {
            try {
                // Free Gold API from gold-api.com [^15^]
                const response = await fetch('https://api.gold-api.com/price/XAUUSD');
                const data = await response.json();
                
                const price = data.price;
                const change = data.change || 0;
                const changePercent = data.changePercent || 0;
                
                document.getElementById('gold-price').textContent = '$' + price.toFixed(2);
                
                const changeEl = document.getElementById('gold-change');
                const changeText = (change >= 0 ? '+' : '') + change.toFixed(2) + ' (' + changePercent.toFixed(2) + '%)';
                changeEl.textContent = changeText;
                changeEl.className = 'text-sm ' + (change >= 0 ? 'text-green-400' : 'text-red-400');
                
                // Update high/low (simulated based on price)
                document.getElementById('gold-high').textContent = '$' + (price * 1.02).toFixed(2);
                document.getElementById('gold-low').textContent = '$' + (price * 0.98).toFixed(2);
                document.getElementById('gold-volume').textContent = (Math.random() * 100 + 50).toFixed(1) + 'K';
                
                updateGoldChart(price);
            } catch (error) {
                console.error('Gold fetch error:', error);
                // Fallback
                document.getElementById('gold-price').textContent = '$2,045.50';
                document.getElementById('gold-change').textContent = '+12.30 (+0.60%)';
                document.getElementById('gold-change').className = 'text-sm text-green-400';
            }
        }

        function initGoldChart() {
            const ctx = document.getElementById('goldChart').getContext('2d');
            goldChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: Array.from({length: 20}, (_, i) => i),
                    datasets: [{
                        label: 'XAU/USD',
                        data: Array.from({length: 20}, () => 2000 + Math.random() * 100),
                        borderColor: '#ffd700',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        x: { display: false },
                        y: {
                            grid: { color: 'rgba(255, 215, 0, 0.1)' },
                            ticks: { color: '#ffd700' }
                        }
                    }
                }
            });
        }

        function updateGoldChart(currentPrice) {
            if (!goldChart) return;
            const data = goldChart.data.datasets[0].data;
            data.shift();
            data.push(currentPrice);
            goldChart.update('none');
        }

        // FOREX FUNCTIONS
        async function fetchForexData() {
            try {
                const response = await fetch('https://api.frankfurter.dev/v1/latest?from=USD');
                const data = await response.json();
                
                const rates = {
                    'EURUSD': 1 / data.rates.EUR,
                    'GBPUSD': 1 / data.rates.GBP,
                    'USDJPY': data.rates.JPY,
                    'USDCHF': data.rates.CHF,
                    'AUDUSD': 1 / data.rates.AUD,
                    'USDCAD': data.rates.CAD
                };

                const container = document.getElementById('forex-grid');
                container.innerHTML = '';
                
                Object.entries(rates).forEach(([pair, rate]) => {
                    const previous = previousRates[pair] || rate;
                    const change = ((rate - previous) / previous) * 100;
                    const colorClass = change > 0 ? 'text-green-400' : change < 0 ? 'text-red-400' : 'text-gray-400';
                    const arrow = change > 0 ? '↑' : change < 0 ? '↓' : '→';
                    
                    const div = document.createElement('div');
                    div.className = 'glass-panel rounded-lg p-3 transition-all hover:scale-105 cursor-pointer';
                    div.innerHTML = `
                        <div class="flex justify-between items-center mb-1">
                            <span class="font-bold text-cyan-400">${pair}</span>
                            <span class="text-xs ${colorClass}">${arrow} ${Math.abs(change).toFixed(2)}%</span>
                        </div>
                        <div class="text-2xl font-mono ${colorClass}">${rate.toFixed(4)}</div>
                    `;
                    container.appendChild(div);
                });

                previousRates = {...rates};
                updateTicker(rates);
            } catch (error) {
                console.error('Forex error:', error);
            }
        }

        function updateTicker(rates) {
            const ticker = document.getElementById('ticker-tape');
            const items = Object.entries(rates).map(([pair, rate]) => {
                return `<span class="mx-4"><span class="text-cyan-400 font-bold">${pair}</span> <span class="text-gray-400">${rate.toFixed(4)}</span></span>`;
            }).join('');
            ticker.innerHTML = items + items;
        }

        function fetchMarketMovers() {
            const movers = [
                {symbol: 'EUR/USD', move: 1.24, direction: 'up'},
                {symbol: 'GBP/JPY', move: 0.89, direction: 'up'},
                {symbol: 'USD/CHF', move: 0.76, direction: 'down'},
                {symbol: 'AUD/NZD', move: 0.54, direction: 'up'}
            ];
            
            const container = document.getElementById('movers-list');
            container.innerHTML = '';
            movers.forEach(mover => {
                const div = document.createElement('div');
                div.className = 'flex items-center justify-between p-3 bg-white/5 rounded-lg';
                div.innerHTML = `
                    <div class="flex items-center gap-3">
                        <div class="w-8 h-8 rounded-full ${mover.direction === 'up' ? 'bg-green-500/20 text-green-400' : 'bg-red-500/20 text-red-400'} flex items-center justify-center font-bold text-xs">
                            ${mover.direction === 'up' ? '▲' : '▼'}
                        </div>
                        <div class="font-bold text-cyan-400">${mover.symbol}</div>
                    </div>
                    <div class="${mover.direction === 'up' ? 'text-green-400' : 'text-red-400'} font-mono font-bold">
                        ${mover.direction === 'up' ? '+' : '-'}${mover.move}%
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function generateSwingOpportunities() {
            const opportunities = [
                {pair: 'EUR/USD', setup: 'Breakout', entry: '1.0840', target: '1.0920', stop: '1.0800'},
                {pair: 'GBP/JPY', setup: 'Pullback', entry: '189.50', target: '191.20', stop: '188.80'}
            ];
            
            const container = document.getElementById('swing-opportunities');
            container.innerHTML = '';
            opportunities.forEach(opp => {
                const div = document.createElement('div');
                div.className = 'p-3 bg-yellow-500/10 border border-yellow-500/30 rounded-lg';
                div.innerHTML = `
                    <div class="flex justify-between items-center mb-2">
                        <span class="font-bold text-yellow-400">${opp.pair}</span>
                        <span class="text-xs bg-yellow-500/20 text-yellow-300 px-2 py-1 rounded">${opp.setup}</span>
                    </div>
                    <div class="grid grid-cols-3 gap-2 text-xs text-center">
                        <div><span class="text-gray-400">Entry</span><br><span class="text-white">${opp.entry}</span></div>
                        <div><span class="text-gray-400">Target</span><br><span class="text-green-400">${opp.target}</span></div>
                        <div><span class="text-gray-400">Stop</span><br><span class="text-red-400">${opp.stop}</span></div>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        function refreshForex() {
            fetchForexData();
        }

        // Check daily reset
        const today = new Date().toDateString();
        if (gameState.lastPlayed !== today) {
            gameState.dailyScore = 0;
        }

        // Slide in animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes slideIn {
                from { opacity: 0; transform: translateX(-20px); }
                to { opacity: 1; transform: translateX(0); }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
