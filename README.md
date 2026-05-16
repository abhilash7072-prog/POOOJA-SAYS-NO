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
            background
