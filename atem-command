<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ATEM 1 M/E Trainer - SNES Edition</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
    <style>
        :root {
            --program-color: #e6482e; /* SNES Red */
            --preview-color: #3fdb67; /* SNES Green */
            --key-color: #4d90f1;     /* SNES Blue */
            --active-light: #ffffff; 
            --base-gray-light: #c6c6c6; /* Light UI Gray */
            --base-gray-dark: #7b7b7b;  /* Dark UI Gray */
            --panel-color: #9d9d9d;    /* Main panel gray */
            --dark-border: #1c1c1c;    /* Black border */
            --light-border: #efefef;   /* White highlight */
            --bg-dark: #2d2b47;        /* Dark purple bg */
            --bg-light: #3c3c54;       /* Lighter purple bg */
        }

        body {
            background-color: var(--bg-dark);
            background-image: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAQAAAAECAYAAACp8Z5+AAAAAXNSR0IArs4c6QAAABJJREFUCB1jZEAD/o/w/5OhvAMA/moC/wI2GcgAAAAASUVORK5CYII=');
            image-rendering: pixelated;
            color: var(--active-light);
            font-family: 'Press Start 2P', monospace;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        /* --- UI STYLES --- */
        .game-ui {
            width: 80%;
            background-color: var(--panel-color);
            border: 4px solid var(--dark-border);
            border-top-color: var(--light-border);
            border-left-color: var(--light-border);
            padding: 10px 20px;
            margin-bottom: 15px;
            position: relative;
        }
        .game-info {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            margin-bottom: 10px;
        }
        .game-info h2 {
            margin: 0;
            font-size: 1em; 
            color: var(--dark-border);
        }
        .prompt-box {
            background-color: #000;
            width: 100%;
            padding: 12px;
            min-height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            border: 2px solid var(--dark-border);
        }
        #prompt-text {
            margin: 0;
            font-size: 0.8em;
            font-style: normal;
            color: var(--preview-color);
            transition: all 0.2s ease;
            letter-spacing: 1px;
            line-height: 1.5;
        }
       
        @keyframes shake {
            10%, 90% { transform: translate3d(-1px, 0, 0); }
            20%, 80% { transform: translate3d(2px, 0, 0); }
            30%, 50%, 70% { transform: translate3d(-4px, 0, 0); }
            40%, 60% { transform: translate3d(4px, 0, 0); }
        }

        #score-display.flash {
            animation: score-flash 0.5s ease;
        }
        @keyframes score-flash {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); color: var(--preview-color); }
            100% { transform: scale(1); }
        }
        
        #confetti-container {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; overflow: hidden; z-index: 9999;
        }

        .confetti {
            position: absolute; width: 6px; height: 6px;
            background-color: #f00; opacity: 1;
        }

        #feedback-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2em;
            color: var(--preview-color);
            opacity: 0;
            margin: 0;
            pointer-events: none;
            z-index: 100;
            text-shadow: 3px 3px var(--dark-border);
            white-space: nowrap;
        }
        #feedback-text.show {
            animation: feedback-anim 1.2s ease-out forwards;
        }
        @keyframes feedback-anim {
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 1; }
            20%, 60% { transform: translate(-50%, -50%) scale(1.1); }
            40%, 80% { transform: translate(-50%, -50%) scale(1); }
            100% { transform: translate(-50%, -50%) scale(1.5); opacity: 0; }
        }
        
        .monitor-flash {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: white;
            opacity: 0;
            pointer-events: none;
        }
        .monitor-flash.flash {
            animation: flash-anim 0.4s ease-out;
        }
        @keyframes flash-anim {
            0% { opacity: 0.7; }
            100% { opacity: 0; }
        }


        .progress-container {
            width: 100%;
            margin-top: 10px;
            display: flex;
            align-items: center;
            font-size: 0.6em;
            color: var(--dark-border);
        }
        .progress-label {
            padding: 0 10px;
            white-space: nowrap;
        }
        .progress-bar-outline {
            flex-grow: 1;
            height: 20px;
            border: 2px solid var(--dark-border);
            border-top-color: var(--base-gray-dark);
            border-left-color: var(--base-gray-dark);
            background-color: #000;
            padding: 2px;
        }
        .progress-bar-fill {
            height: 100%;
            width: 0%;
            background-color: var(--preview-color);
            transition: width 0.5s ease-out;
        }

        .monitors {
            display: flex;
            justify-content: center;
            width: 80%;
            margin-bottom: 20px;
        }

        .monitor {
            background-color: #000;
            border: 4px solid var(--dark-border);
            border-top-color: var(--light-border);
            border-left-color: var(--light-border);
            width: 45%;
            height: 25vh;
            margin: 0 10px;
            display: flex;
            flex-direction: column;
            overflow: hidden;
            position: relative;
        }

        .monitor-label {
            background-color: var(--dark-gray);
            color: var(--light-border);
            text-align: center;
            padding: 5px;
            font-size: 0.8em;
            flex-shrink: 0;
        }

        .monitor-content {
            width: 100%; height: 100%; display: flex; align-items: center;
            justify-content: center; position: relative;
        }
        
        .monitor-content > div { width: 100%; height: 100%; }
        .monitor-content svg {
            width: 100%; height: 100%; object-fit: contain;
            shape-rendering: crispEdges;
        }
        
        .key-overlay {
            position: absolute; width: 100%; height: 100%;
            top: 0; left: 0; opacity: 0;
            transition: opacity 0.2s step-end; pointer-events: none;
        }
        .key-overlay.visible { opacity: 1; }
        
        #preview-label { color: var(--preview-color); }
        #program-label { color: var(--program-color); }

        .atem-switcher {
            background-color: var(--panel-color);
            padding: 15px;
            display: grid;
            grid-template-columns: 3fr 1fr;
            grid-gap: 20px;
            width: 80%;
            border: 4px solid var(--dark-border);
            border-top-color: var(--light-border);
            border-left-color: var(--light-border);
        }

        .bus-row { margin-bottom: 15px; }
        .bus-label { margin-bottom: 8px; font-size: 0.8em; color: var(--dark-border); }
        .buttons { display: flex; justify-content: space-between; }

        .btn {
            background-color: var(--base-gray-light);
            border-style: solid;
            border-width: 2px;
            border-color: var(--light-border) var(--dark-border) var(--dark-border) var(--light-border);
            color: var(--dark-border);
            padding: 10px 5px; font-size: 9px;
            font-family: 'Press Start 2P', monospace; cursor: pointer;
            flex-grow: 1; margin: 0 2px; text-align: center;
            -webkit-user-select: none; user-select: none;
        }

        .btn:active {
            border-color: var(--dark-border) var(--light-border) var(--light-border) var(--dark-border);
        }
        
        .key-bus .btn.active { background-color: var(--key-color); color: var(--active-light); text-shadow: 1px 1px var(--dark-border); }
        .program-bus .btn.active { background-color: var(--program-color); color: var(--active-light); text-shadow: 1px 1px var(--dark-border);}
        .preview-bus .btn.active, .keyer-btn.active { background-color: var(--preview-color); color: var(--dark-border); }

        .side-controls { display: flex; flex-direction: column; }
        .key-buttons { display: grid; grid-template-columns: repeat(5, 1fr); gap: 5px; margin-bottom: 10px; }
        .side-controls .btn.active { background-color: var(--light-border); color: var(--dark-border); }
        .side-controls .on-btn.active { background-color: var(--program-color); color: var(--active-light); text-shadow: 1px 1px var(--dark-border); }
        .side-controls .background-btn.active { background-color: var(--program-color); color: var(--active-light); text-shadow: 1px 1px var(--dark-border); }
        .side-controls .dsk-btn.active { background-color: var(--program-color); color: var(--active-light); text-shadow: 1px 1px var(--dark-border); }


        .transition-controls { display: flex; justify-content: space-around; margin-top: auto; }
        .momentary-btn { padding: 15px 10px; font-size: 14px; }
        .cut-btn { background-color: var(--program-color); }
        .auto-btn { background-color: var(--preview-color); }

        .dsk-controls {
            margin-top: 10px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 5px;
        }
        .dsk-btn {
            width: 100%; padding: 10px; font-size: 1em;
        }
        
    </style>
</head>
<body>

    <!-- Generated SVG Images -->
    <div id="image-sources" style="display: none;">
        <!-- Video Sources -->
        <svg id="img-cam-1" viewBox="0 0 100 80" fill="none" stroke="#fff" stroke-width="3"><path d="M10 20 H60 V70 H10 Z M60 30 L85 15 V75 L60 60" stroke-linejoin="round"/><circle cx="35" cy="45" r="12" stroke-width="2"/><text x="45" y="30" font-size="12" fill="#fff" font-family="sans-serif">1</text></svg>
        <svg id="img-cam-2" viewBox="0 0 100 80" fill="none" stroke="#fff" stroke-width="3"><path d="M10 20 H60 V70 H10 Z M60 30 L85 15 V75 L60 60" stroke-linejoin="round"/><circle cx="35" cy="45" r="12" stroke-width="2"/><text x="45" y="30" font-size="12" fill="#fff" font-family="sans-serif">2</text></svg>
        <svg id="img-cam-3" viewBox="0 0 100 80" fill="none" stroke="#fff" stroke-width="3"><path d="M10 20 H60 V70 H10 Z M60 30 L85 15 V75 L60 60" stroke-linejoin="round"/><circle cx="35" cy="45" r="12" stroke-width="2"/><text x="45" y="30" font-size="12" fill="#fff" font-family="sans-serif">3</text></svg>
        <svg id="img-class-pc" viewBox="0 0 100 80" fill="none" stroke="#fff" stroke-width="3"><rect x="10" y="10" width="80" height="55" rx="5"/><path d="M30 65 H70 L75 75 H25 Z"/><text x="50" y="45" font-size="24" fill="#fff" text-anchor="middle" font-family="sans-serif">A+</text></svg>
        <svg id="img-control-pc" viewBox="0 0 100 80" fill="none" stroke="#fff" stroke-width="3"><rect x="10" y="10" width="80" height="55" rx="5"/><path d="M30 65 H70 L75 75 H25 Z"/><circle cx="50" cy="38" r="12" stroke-width="2"/><path d="M50 16 L50 24 M50 52 L50 60 M30 38 L38 38 M62 38 L70 38" stroke-width="4"/></svg>
        <svg id="img-mp-1" viewBox="0 0 100 80" fill="#fff"><path d="M40 30 L65 45 L40 60 Z"/><text x="70" y="52" font-size="12" fill="#fff" font-family="sans-serif">1</text></svg>
        <svg id="img-mp-2" viewBox="0 0 100 80" fill="#fff"><path d="M40 30 L65 45 L40 60 Z"/><text x="70" y="52" font-size="12" fill="#fff" font-family="sans-serif">2</text></svg>
        <div id="img-color" style="width: 100%; height: 100%; background-color: #2980b9;"></div>
        <svg id="img-bars" viewBox="0 0 7 6"><rect fill="#C0C0C0" width="1" height="4"/><rect fill="#C0C000" x="1" width="1" height="4"/><rect fill="#00C0C0" x="2" width="1" height="4"/><rect fill="#00C000" x="3" width="1" height="4"/><rect fill="#C000C0" x="4" width="1" height="4"/><rect fill="#C00000" x="5" width="1" height="4"/><rect fill="#0000C0" x="6" width="1" height="4"/><rect fill="#0000C0" y="4" width="1" height="2"/><rect fill="#000000" x="1" y="4" width="1" height="2"/><rect fill="#C000C0" x="2" y="4" width="1" height="2"/><rect fill="#000000" x="3" y="4" width="1" height="2"/><rect fill="#00C0C0" x="4" y="4" width="1" height="2"/><rect fill="#000000" x="5" y="4" width="1" height="2"/><rect fill="#C0C0C0" x="6" y="4" width="1" height="2"/></svg>
        <div id="img-black" style="width: 100%; height: 100%; background-color: #000;"></div>

        <!-- Key Graphics -->
        <svg id="key-graphic-1" viewBox="0 0 200 40"><rect x="0" y="10" width="200" height="20" fill="rgba(0,50,150,0.8)" /><text x="100" y="26" font-size="12" fill="#fff" text-anchor="middle" font-family="sans-serif">JANE DOE - HOST</text></svg>
        <svg id="key-graphic-2" viewBox="0 0 100 100"><circle cx="80" cy="20" r="15" fill="rgba(200,0,0,0.9)" /><text x="80" y="25" font-size="14" fill="#fff" text-anchor="middle" font-family="sans-serif" font-weight="bold">LIVE</text></svg>
        <svg id="key-graphic-3" viewBox="0 0 100 40"><rect x="10" y="10" width="80" height="20" fill="rgba(200,100,0,0.9)" /><text x="50" y="25" font-size="14" fill="#fff" text-anchor="middle" font-family="sans-serif">REPLAY</text></svg>
        <svg id="key-graphic-4" viewBox="0 0 100 100"><rect x="10" y="60" width="80" height="20" fill="rgba(0,100,50,0.9)" /><text x="50" y="75" font-size="10" fill="#fff" text-anchor="middle" font-family="sans-serif">MEGA CORP</text></svg>
    </div>

    <div id="confetti-container"></div>

    <!-- Game UI -->
    <div class="game-ui">
        <h2 id="feedback-text"></h2>
        <div class="game-info">
             <h2>SCORE: <span id="score-display">0</span></h2>
        </div>
        <div class="prompt-box" id="prompt-box">
            <p id="prompt-text">Press DSK2 to begin!</p>
        </div>
        <div class="progress-container">
            <div class="progress-label">Live in 3,2,1...</div>
            <div class="progress-bar-outline">
                <div class="progress-bar-fill" id="progress-bar"></div>
            </div>
            <div class="progress-label">Roll Credits!</div>
        </div>
    </div>

    <div class="monitors">
        <div class="monitor">
            <div class="monitor-label" id="preview-label">Preview</div>
            <div class="monitor-content" id="preview-screen">
                <div id="preview-source-container"></div>
                <div class="monitor-flash"></div>
            </div>
        </div>
        <div class="monitor">
            <div class="monitor-label" id="program-label">Program</div>
            <div class="monitor-content" id="program-screen">
                <div id="program-source-container"></div>
                <div id="key-1-container" class="key-overlay"></div>
                <div id="key-2-container" class="key-overlay"></div>
                <div id="key-3-container" class="key-overlay"></div>
                <div id="key-4-container" class="key-overlay"></div>
                <div class="monitor-flash"></div>
            </div>
        </div>
    </div>

    <div class="atem-switcher">
        <div class="bus-section">
            <div class="bus-row key-bus">
                <div class="bus-label">Key Bus</div>
                <div class="buttons">
                    <button class="btn">CAM 1</button><button class="btn">CAM 2</button><button class="btn">CAM 3</button><button class="btn">CLASS PC</button><button class="btn">CONTROL PC</button><button class="btn">MEDIA PLAYER 1</button><button class="btn">MEDIA PLAYER 2</button><button class="btn">COLOR</button><button class="btn">BARS</button><button class="btn">BLACK</button>
                </div>
            </div>
            <div class="bus-row program-bus">
                <div class="bus-label">Program Bus</div>
                <div class="buttons">
                    <button class="btn" data-source-id="img-cam-1">CAM 1</button><button class="btn" data-source-id="img-cam-2">CAM 2</button><button class="btn" data-source-id="img-cam-3">CAM 3</button><button class="btn" data-source-id="img-class-pc">CLASS PC</button><button class="btn" data-source-id="img-control-pc">CONTROL PC</button><button class="btn" data-source-id="img-mp-1">MEDIA PLAYER 1</button><button class="btn" data-source-id="img-mp-2">MEDIA PLAYER 2</button><button class="btn" data-source-id="img-color">COLOR</button><button class="btn" data-source-id="img-bars">BARS</button><button class="btn" data-source-id="img-black">BLACK</button>
                </div>
            </div>
             <div class="bus-row preview-bus">
                <div class="bus-label">Preview Bus</div>
                <div class="buttons">
                    <button class="btn" data-source-id="img-cam-1">CAM 1</button><button class="btn" data-source-id="img-cam-2">CAM 2</button><button class="btn" data-source-id="img-cam-3">CAM 3</button><button class="btn" data-source-id="img-class-pc">CLASS PC</button><button class="btn" data-source-id="img-control-pc">CONTROL PC</button><button class="btn" data-source-id="img-mp-1">MEDIA PLAYER 1</button><button class="btn" data-source-id="img-mp-2">MEDIA PLAYER 2</button><button class="btn" data-source-id="img-color">COLOR</button><button class="btn" data-source-id="img-bars">BARS</button><button class="btn" data-source-id="img-black">BLACK</button>
                </div>
            </div>
        </div>
        <div class="side-controls">
            <div class="key-buttons">
                <button class="btn">MACRO</button><button class="btn on-btn" data-key-id="1">ON</button><button class="btn on-btn" data-key-id="2">ON</button><button class="btn on-btn" data-key-id="3">ON</button><button class="btn on-btn" data-key-id="4">ON</button>
                <button class="btn background-btn">BACKGROUND</button><button class="btn keyer-btn" data-key-id="1">KEY 1</button><button class="btn keyer-btn" data-key-id="2">KEY 2</button><button class="btn keyer-btn" data-key-id="3">KEY 3</button><button class="btn keyer-btn" data-key-id="4">KEY 4</button>
            </div>
            <div class="transition-controls">
                <button class="btn momentary-btn cut-btn">CUT</button>
                <button class="btn momentary-btn auto-btn">AUTO</button>
            </div>
            <div class="dsk-controls">
                <button class="btn dsk-btn" id="dsk1-btn">DSK1</button>
                <button class="btn dsk-btn" id="dsk2-btn">DSK2</button>
            </div>
        </div>
    </div>

    <script>
        // --- DOM ELEMENTS ---
        const programScreen = document.getElementById('program-screen');
        const previewScreen = document.getElementById('preview-screen');
        const programSourceContainer = document.getElementById('program-source-container');
        const previewSourceContainer = document.getElementById('preview-source-container');
        const imageSources = document.getElementById('image-sources');
        const scoreDisplay = document.getElementById('score-display');
        const promptText = document.getElementById('prompt-text');
        const promptBox = document.getElementById('prompt-box');
        const dsk2Button = document.getElementById('dsk2-btn');
        const confettiContainer = document.getElementById('confetti-container');
        const feedbackText = document.getElementById('feedback-text');
        const progressBar = document.getElementById('progress-bar');

        // --- GAME STATE ---
        let score = 0;
        const GOAL_SCORE = 2500;
        let currentPrompt = null;
        let gameStarted = false;
        let availablePrompts = [];
        const keyerGraphics = {
            1: 'key-graphic-1', 2: 'key-graphic-2',
            3: 'key-graphic-3', 4: 'key-graphic-4'
        };
        const activeKeys = new Set();
        const armedKeys = new Set();
        const successMessages = ["PERFECT!", "NICE SWITCH!", "GREAT!", "EXCELLENT!", "AWESOME!"];
        
        const customSounds = {
            correct: '',
            click: '', // Placeholder for custom click sound
        };

        // --- COMBINED PROMPT DEFINITIONS ---
        const gamePrompts = [
            { text: "Show me Camera 1, clean.", targetSource: "img-cam-1", targetKeys: {} },
            { text: "I need the Class PC on Program.", targetSource: "img-class-pc", targetKeys: {} },
            { text: "Put Media Player 1 on the air.", targetSource: "img-mp-1", targetKeys: {} },
            { text: "Give me the wide shot on Cam 2.", targetSource: "img-cam-2", targetKeys: {} },
            { text: "Let's see the Control PC feed.", targetSource: "img-control-pc", targetKeys: {} },
            { text: "Take it to black.", targetSource: "img-black", targetKeys: {} },
            { text: "I want Camera 1 with the host's lower third (Key 1).", targetSource: "img-cam-1", targetKeys: { 1: 'on' } },
            { text: "Show me Camera 2 with the LIVE bug (Key 2).", targetSource: "img-cam-2", targetKeys: { 2: 'on' } },
            { text: "Put the Class PC up, and add the Sponsor logo (Key 4).", targetSource: "img-class-pc", targetKeys: { 4: 'on' } },
            { text: "I need Camera 1 with the Replay graphic (Key 3) and the Sponsor logo (Key 4).", targetSource: "img-cam-1", targetKeys: { 3: 'on', 4: 'on' } },
            { text: "Let's see Camera 2 with the lower third (Key 1) and the LIVE bug (Key 2).", targetSource: "img-cam-2", targetKeys: { 1: 'on', 2: 'on' } }
        ];

        // --- AUDIO ---
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function playSound(type) {
            if (type === 'click' && customSounds.click) { new Audio(customSounds.click).play(); return; }
            if (type === 'correct' && customSounds.correct) { new Audio(customSounds.correct).play(); return; }
             
             const oscillator = audioCtx.createOscillator(); const gainNode = audioCtx.createGain(); oscillator.connect(gainNode); gainNode.connect(audioCtx.destination); gainNode.gain.setValueAtTime(0, audioCtx.currentTime); gainNode.gain.linearRampToValueAtTime(0.3, audioCtx.currentTime + 0.01);
             if (type === 'correct') { oscillator.type = 'sine'; oscillator.frequency.setValueAtTime(880.0, audioCtx.currentTime); }
             else if (type === 'click') { oscillator.type = 'triangle'; oscillator.frequency.setValueAtTime(1500, audioCtx.currentTime); gainNode.gain.linearRampToValueAtTime(0.1, audioCtx.currentTime + 0.01); }
             else { oscillator.type = 'square'; oscillator.frequency.setValueAtTime(110.0, audioCtx.currentTime); }
             oscillator.start(audioCtx.currentTime);
             const duration = (type === 'click') ? 0.05 : 0.1;
             gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + duration);
             oscillator.stop(audioCtx.currentTime + duration);
        }

        // --- PIZZAZ FUNCTIONS ---
        function triggerConfetti() {
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.classList.add('confetti');
                const colors = ['#d6495f', '#75c179', '#6ec5d9', '#f2f0f3'];
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                
                confetti.style.left = `${window.innerWidth / 2}px`;
                confetti.style.top = `${window.innerHeight / 2}px`;

                const animationName = `confetti-fall-${i}`;
                const xEnd = Math.random() * 400 - 200;
                const yEnd = Math.random() * 200 + 100;

                const keyframes = `@keyframes ${animationName} {
                    0% { transform: translate(0, 0) rotateZ(0); opacity: 1; }
                    30% { transform: translate(${xEnd * 0.5}px, -${yEnd}px) rotateZ(180deg); opacity: 1; }
                    100% { transform: translate(${xEnd}px, 100vh) rotateZ(360deg); opacity: 0; }
                }`;
                
                let dynamicStyleSheet = document.getElementById('dynamic-styles');
                if (!dynamicStyleSheet) {
                    dynamicStyleSheet = document.createElement('style');
                    dynamicStyleSheet.id = 'dynamic-styles';
                    document.head.appendChild(dynamicStyleSheet);
                }
                dynamicStyleSheet.sheet.insertRule(keyframes, dynamicStyleSheet.sheet.cssRules.length);
                
                confetti.style.animation = `${animationName} ${1.5 + Math.random()}s ease-out forwards`;
                confettiContainer.appendChild(confetti);

                setTimeout(() => confetti.remove(), 2500);
            }
        }


        // --- GAME LOGIC ---
        function startGame() {
            score = 0;
            updateScoreboard();
            availablePrompts = [...gamePrompts];
            displayNewPrompt();
            gameStarted = true;
        }

        function endGame() {
            gameStarted = false;
            currentPrompt = null;
            promptText.textContent = `Round ended. Press DSK2 to start a new class.`;
        }

        function updateScoreboard() { 
            scoreDisplay.textContent = score; 
            scoreDisplay.classList.add('flash');
            setTimeout(() => scoreDisplay.classList.remove('flash'), 500);
            const progress = Math.min((score / GOAL_SCORE) * 100, 100);
            progressBar.style.width = `${progress}%`;
        }

        function isPromptValid(p) {
            const currentProgramSource = document.querySelector('.program-bus .btn.active')?.dataset.sourceId;
            const targetOnKeys = new Set();
            for (const keyIdStr in p.targetKeys) {
                if (p.targetKeys[keyIdStr] === 'on') {
                    targetOnKeys.add(parseInt(keyIdStr));
                }
            }
            const programSourceMatches = p.targetSource === currentProgramSource;
            const keysMatch = activeKeys.size === targetOnKeys.size && [...activeKeys].every(key => targetOnKeys.has(key));
            return !(programSourceMatches && keysMatch);
        }

        function displayNewPrompt() {
             if (score >= GOAL_SCORE) {
                promptText.textContent = "Well done! The professor was happy with the production! Press DSK2 to start the next class.";
                gameStarted = false;
                dsk2Button.classList.add('active');
                currentPrompt = null;
                return;
            }

            if (availablePrompts.length === 0) {
                 promptText.textContent = `Training Complete! Final Score: ${score}. Press DSK2 to play again.`;
                 gameStarted = false;
                 dsk2Button.classList.add('active');
                 currentPrompt = null;
                 return;
            }

            let potentialPrompts = availablePrompts.filter(isPromptValid);

            if (potentialPrompts.length === 0) {
                promptText.textContent = `All tasks complete! Final Score: ${score}. Press DSK2 to play again.`;
                 gameStarted = false;
                 dsk2Button.classList.add('active');
                 currentPrompt = null;
                return;
            }
            
            const promptIndex = Math.floor(Math.random() * potentialPrompts.length);
            currentPrompt = potentialPrompts[promptIndex];
            
            availablePrompts = availablePrompts.filter(p => p !== currentPrompt);
            promptText.textContent = currentPrompt.text;
        }

        function evaluateProgramState() {
            if (!gameStarted || !currentPrompt) return;

            const actualProgramSource = document.querySelector('.program-bus .btn.active')?.dataset.sourceId;
            const actualOnKeys = new Set(activeKeys);

            const requiredSource = currentPrompt.targetSource;
            const requiredOnKeys = new Set();
            for (const keyIdStr in currentPrompt.targetKeys) {
                if (currentPrompt.targetKeys[keyIdStr] === 'on') {
                    requiredOnKeys.add(parseInt(keyIdStr));
                }
            }

            const sourceMatches = actualProgramSource === requiredSource;
            const keysMatch = actualOnKeys.size === requiredOnKeys.size && [...actualOnKeys].every(key => requiredOnKeys.has(key));

            if (sourceMatches && keysMatch) {
                handleCorrectAnswer();
            }
        }

        function handleCorrectAnswer() {
             playSound('correct');
             triggerConfetti();
             document.querySelector('#program-screen').parentElement.querySelector('.monitor-flash').classList.add('flash');

             const keyElements = Object.keys(currentPrompt.targetKeys).length;
             const pointsEarned = (1 + keyElements) * 150;
             score += pointsEarned;
             updateScoreboard();

             const randomSuccessMessage = successMessages[Math.floor(Math.random() * successMessages.length)];
             feedbackText.textContent = randomSuccessMessage;
             feedbackText.classList.add('show');
             
             promptText.style.opacity = 0;
             currentPrompt = null; 

             setTimeout(() => {
                feedbackText.classList.remove('show');
                promptText.style.opacity = 1;
                document.querySelector('#program-screen').parentElement.querySelector('.monitor-flash').classList.remove('flash');
                displayNewPrompt();
             }, 1200);
        }
        
        // --- TRANSITION LOGIC ---
        function performTransition() {
            if (!gameStarted) return;

            const activePreviewButton = document.querySelector('.preview-bus .btn.active');
            const activeProgramButton = document.querySelector('.program-bus .btn.active');
            
            if (activePreviewButton) {
                const targetProgramButton = document.querySelector(`.program-bus .btn[data-source-id="${activePreviewButton.dataset.sourceId}"]`);
                if(targetProgramButton) targetProgramButton.dispatchEvent(new MouseEvent('click'));
            }
            if (activeProgramButton) {
                const targetPreviewButton = document.querySelector(`.preview-bus .btn[data-source-id="${activeProgramButton.dataset.sourceId}"]`);
                if(targetPreviewButton) targetPreviewButton.dispatchEvent(new MouseEvent('click'));
            }

            armedKeys.forEach(keyId => {
                const onButton = document.querySelector(`.on-btn[data-key-id="${keyId}"]`);
                if(onButton) onButton.dispatchEvent(new MouseEvent('click'));
            });
            
            evaluateProgramState();

            document.querySelectorAll('.keyer-btn.active').forEach(btn => btn.classList.remove('active'));
            armedKeys.clear();
        }

        // --- SWITCHER LOGIC ---
        function setupExclusiveBusRow(busSelector, screenContainer) {
            const bus = document.querySelector(busSelector);
            if (!bus) return;
            const buttons = bus.querySelectorAll('.btn');
            buttons.forEach(button => {
                button.addEventListener('click', () => {
                    if (button.classList.contains('active')) return;
                    buttons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    const sourceId = button.dataset.sourceId;
                    if (screenContainer && sourceId) {
                        const sourceElement = imageSources.querySelector(`#${sourceId}`);
                        if (sourceElement) screenContainer.innerHTML = sourceElement.outerHTML;
                    }
                    if(bus.classList.contains('program-bus')) evaluateProgramState();
                });
            });
        }
        
        function setupKeyOnButtons() {
            const onButtons = document.querySelectorAll('.on-btn');
            onButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const keyId = parseInt(button.dataset.keyId);
                    button.classList.toggle('active');
                    const keyOverlay = document.getElementById(`key-${keyId}-container`);
                    const graphicSourceId = keyerGraphics[keyId];
                    if (button.classList.contains('active')) {
                        activeKeys.add(keyId);
                        if(keyOverlay && graphicSourceId) keyOverlay.innerHTML = imageSources.querySelector(`#${graphicSourceId}`).outerHTML;
                        keyOverlay.classList.add('visible');
                    } else {
                        activeKeys.delete(keyId);
                        keyOverlay.classList.remove('visible');
                    }
                    evaluateProgramState();
                });
            });
        }
        
        function setupKeyerButtons() {
            const keyerButtons = document.querySelectorAll('.keyer-btn');
            keyerButtons.forEach(button => {
                button.addEventListener('click', () => {
                    button.classList.toggle('active');
                    const keyId = parseInt(button.dataset.keyId);
                    if(button.classList.contains('active')) {
                        armedKeys.add(keyId);
                    } else {
                        armedKeys.delete(keyId);
                    }
                });
            });
        }

        // --- INITIALIZATION ---
        setupExclusiveBusRow('.program-bus', programSourceContainer);
        setupExclusiveBusRow('.preview-bus', previewSourceContainer);
        setupKeyOnButtons();
        setupKeyerButtons();
        
        document.querySelectorAll('.btn').forEach(button => {
             button.addEventListener('mousedown', () => playSound('click'));
        });

        document.querySelectorAll('.key-buttons .btn:not(.on-btn):not(.keyer-btn):not(.background-btn), .key-bus .btn, #dsk1-btn').forEach(button => {
            button.addEventListener('click', () => button.classList.toggle('active'));
        });
        
        const cutButton = document.querySelector('.cut-btn');
        const autoButton = document.querySelector('.auto-btn');
        cutButton.addEventListener('click', performTransition);
        autoButton.addEventListener('click', performTransition);
        
        dsk2Button.addEventListener('click', () => {
            dsk2Button.classList.toggle('active');
            if(gameStarted) {
                endGame();
            } else {
                startGame();
            }
        });

        function setInitialState() {
            gameStarted = false; 
            document.querySelector('.program-bus .btn[data-source-id="img-black"]')?.dispatchEvent(new MouseEvent('click'));
            document.querySelector('.preview-bus .btn[data-source-id="img-cam-1"]')?.dispatchEvent(new MouseEvent('click'));
            document.querySelector('.background-btn').classList.add('active');
            dsk2Button.classList.add('active');
            gameStarted = false; 
            promptText.textContent = "Press DSK2 to begin your training!";
            updateScoreboard();
        }

        setInitialState();

    </script>
</body>
</html>
