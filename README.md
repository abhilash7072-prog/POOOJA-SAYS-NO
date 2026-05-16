<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Incoming Transmission... 🌸</title>
    <style>
        :root {
            --primary: #ff6b8b;
            --primary-light: #ffa3b1;
            --accent: #4dadf7;
            --bg: #fff0f3;
            --terminal-bg: #2d3436;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
        }

        body {
            font-family: 'Courier New', Courier, monospace;
            background: linear-gradient(135deg, #ffe3e8 0%, #ffccd5 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Floating Hearts Background */
        .hearts-bg {
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }

        .heart-particle {
            position: absolute;
            color: rgba(255, 107, 139, 0.2);
            font-size: 20px;
            animation: floatUp 6s linear infinite;
        }

        @keyframes floatUp {
            0% { transform: translateY(105vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        /* Main Arcade Console */
        .arcade-box {
            background: #fff;
            border: 4px solid #000;
            border-radius: 24px;
            padding: 30px;
            width: 90%;
            max-width: 480px;
            box-shadow: 8px 8px 0px #000;
            z-index: 2;
            position: relative;
            transform: rotate(-1deg);
            animation: gentleFloat 4s ease-in-out infinite alternate;
        }

        @keyframes gentleFloat {
            0% { transform: translateY(0) rotate(-1deg); }
            100% { transform: translateY(-10px) rotate(1deg); }
        }

        /* Screen Wrapper */
        .screen {
            background: var(--terminal-bg);
            border: 3px solid #000;
            border-radius: 12px;
            padding: 25px 15px;
            min-height: 220px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: #fff;
            margin-bottom: 25px;
            box-shadow: inset 0 0 20px rgba(0,0,0,0.8);
            position: relative;
            overflow: hidden;
        }

        .screen::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            z-index: 2;
            background-size: 100% 3px, 6px 100%;
            pointer-events: none;
        }

        .emoji-hub {
            font-size: 4.5rem;
            margin-bottom: 15px;
            filter: drop-shadow(0 4px 8px rgba(0,0,0,0.3));
        }

        .text-display {
            font-size: 1.25rem;
            font-weight: bold;
            line-height: 1.5;
            color: #51cf66; /* Retro Green terminal text */
            text-shadow: 0 0 5px rgba(81, 207, 102, 0.5);
        }

        /* Japan Ticket Aesthetic */
        .ticket {
            background: #fff;
            color: #000;
            border: 2px dashed var(--primary);
            border-radius: 10px;
            padding: 15px;
            margin-top: 10px;
            font-family: Arial, sans-serif;
            box-shadow: 4px 4px 0px #000;
            width: 100%;
            transform: scale(0);
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        @keyframes popIn {
            100% { transform: scale(1); }
        }

        /* Buttons Styling (Chunky Game-Boy Aesthetic) */
        .controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            min-height: 70px;
        }

        .btn {
            padding: 14px 28px;
            font-size: 1.1rem;
            font-weight: 900;
            font-family: 'Courier New', Courier, monospace;
            border: 3px solid #000;
            border-radius: 12px;
            cursor: pointer;
            position: relative;
            box-shadow: 4px 4px 0px #000;
            transition: all 0.1s ease;
        }

        .btn:active {
            transform: translate(3px, 3px);
            box-shadow: 1px 1px 0px #000;
        }

        .btn-yes {
            background: var(--primary);
            color: #fff;
        }

        .btn-no {
            background: #e9ecef;
            color: #000;
            position: absolute;
            transition: left 0.12s linear, top 0.12s linear, transform 0.2s ease;
        }
    </style>
</head>
<body>

    <div class="hearts-bg" id="heartsBg"></div>

    <div class="arcade-box">
        <div class="screen">
            <div class="emoji-hub" id="displayEmoji">💌</div>
            <div class="text-display" id="displayText">SYSTEM: Execute love_request.exe?<br>> Would you like to be my gf?</div>
        </div>
        
        <div class="controls" id="controlPanel">
            <button class="btn btn-yes" id="yesBtn" onclick="handleYes()">YES</button>
            <button class="btn btn-no" id="noBtn">NO</button>
        </div>
    </div>

    <script>
        let step = 1;
        let noScale = 1;
        const textElement = document.getElementById('displayText');
        const emojiElement = document.getElementById('displayEmoji');
        const controlPanel = document.getElementById('controlPanel');
        const noBtn = document.getElementById('noBtn');

        // Create Background Hearts
        function spawnHearts() {
            const container = document.getElementById('heartsBg');
            for (let i = 0; i < 20; i++) {
                let heart = document.createElement('div');
                heart.className = 'heart-particle';
                heart.innerHTML = '🌸';
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.animationDelay = Math.random() * 5 + 's';
                heart.style.fontSize = (Math.random() * 20 + 15) + 'px';
                container.appendChild(heart);
            }
        }
        spawnHearts();

        // Runaway Engine + Shrink Strategy
        function flee() {
            // Get random bounds keeping it safe inside the inner viewport padding
            const x = Math.random() * (window.innerWidth - noBtn.offsetWidth - 60) + 30;
            const y = Math.random() * (window.innerHeight - noBtn.offsetHeight - 60) + 30;
            
            noBtn.style.position = 'fixed';
            noBtn.style.left = x + 'px';
            noBtn.style.top = y + 'px';

            // Shrink it every time she tries to touch it so it gets progressively harder
            if(noScale > 0.3) {
                noScale -= 0.1;
                noBtn.style.transform = `scale(${noScale})`;
            }
        }

        // Event hooks for evasive maneuvers
        noBtn.addEventListener('mouseenter', flee);
        noBtn.addEventListener('click', flee);
        noBtn.addEventListener('touchstart', (e) => { e.preventDefault(); flee(); });

        // Progression Engine
        function handleYes() {
            if (step === 1) {
                // Click 2 Processing
                step = 2;
                emojiElement.innerHTML = "✨🦉✨";
                textElement.style.color = "#ff8787"; // Change terminal font color to soft pink
                textElement.innerHTML = "CRITICAL ACCESS GRANTED:<br>> Processing reward script...";
                
                // Hide the "No" button entirely while ticket renders
                noBtn.style.display = 'none';
                
                // Change Yes text to fire stage 3
                const yesBtn = document.getElementById('yesBtn');
                yesBtn.innerHTML = "CLAIM REWARD 💾";

            } else if (step === 2) {
                // Click 3: Reveal Japan Trip Voucher
                step = 3;
                emojiElement.innerHTML = "✈️🌸🇯🇵";
                textElement.innerHTML = `
                    <div class="ticket">
                        <div style="font-size:0.8rem; letter-spacing:2px; color:#aaa;">BOARDING PASS</div>
                        <div style="font-size:1.4rem; font-weight:bold; color:var(--primary)">TOKYO & BEYOND</div>
                        <hr style="border:none; border-top:1px dashed #ccc; margin:8px 0;">
                        <div style="text-align:left; font-size:0.9rem; line-height:1.4;">
                            • <strong>DURATION:</strong> 5 Magical Days<br>
                            • <strong>VALID:</strong> Any day after June 15
                        </div>
                    </div>
                `;
                
                // Transition action for next prompt
                const yesBtn = document.getElementById('yesBtn');
                yesBtn.innerHTML = "CONTINUE SYSTEM CHECK ⚙️";

            } else if (step === 3) {
                // Click 4: Love confirmation challenge
                step = 4;
                emojiElement.innerHTML = "🔮💖";
                textElement.style.color = "#4dadf7"; // Neon Blue terminal phase
                textElement.innerHTML = "FINAL HARDWARE TEST:<br>> Do you love me?";
                
                // Revive the RUNAWAY NO button at original size
                noScale = 1;
                noBtn.style.position = 'absolute';
                noBtn.style.left = 'auto';
                noBtn.style.top = 'auto';
                noBtn.style.transform = 'scale(1)';
                noBtn.style.display = 'block';

                const yesBtn = document.getElementById('yesBtn');
                yesBtn.innerHTML = "YES, UNCONDITIONALLY";

            } else if (step === 4) {
                // Click 5: Ending Complete!
                step = 5;
                emojiElement.innerHTML = "👑💝🏡";
                textElement.style.color = "#51cf66"; // Success Green
                textElement.innerHTML = "SYSTEM NOMINAL.<br><br>Connection Established.<br>Destination Locked: Japan 🌸<br>I love you too!";
                
                // Wipe controls out completely
                controlPanel.innerHTML = "";
            }
        }
    </script>
</body>
</html>
