<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Discours du Clan X-TMP</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            background-image: 
                radial-gradient(circle at 20% 80%, rgba(229, 62, 62, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(221, 107, 32, 0.1) 0%, transparent 50%),
                url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200' viewBox='0 0 200 200'%3E%3Cg fill='none' stroke='%23e53e3e' stroke-width='2' opacity='0.1'%3E%3Ctext x='100' y='100' text-anchor='middle' dominant-baseline='middle' font-size='24' font-weight='bold'%3ETMP%3C/text%3E%3Ccircle cx='100' cy='100' r='80'/%3E%3Cpath d='M60 60 L140 140 M140 60 L60 140'/%3E%3C/g%3E%3C/svg%3E");
            background-size: 100% 100%, 100% 100%, 300px 300px;
            background-position: center, center, center;
            background-repeat: no-repeat, no-repeat, repeat;
            min-height: 100vh;
            color: #fff;
        }

        .container {
            height: 100vh;
            display: flex;
            flex-direction: column;
            max-width: 100%;
        }

        .header {
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            color: white;
            padding: 15px 20px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }

        .header h1 {
            font-size: 1.8em;
            margin-bottom: 5px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            font-weight: bold;
        }

        .user-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(255, 255, 255, 0.1);
            padding: 10px;
            border-radius: 10px;
            margin-top: 10px;
            font-size: 0.9em;
        }

        .online-users {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .user-badge {
            background: rgba(255, 255, 255, 0.2);
            padding: 5px 12px;
            border-radius: 20px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #48bb78;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .main-content {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        .sidebar {
            width: 280px;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-right: 1px solid rgba(255, 255, 255, 0.1);
            padding: 15px;
            overflow-y: auto;
        }

        .sidebar h3 {
            color: #e53e3e;
            margin-bottom: 15px;
            font-size: 1.1em;
            font-weight: bold;
        }

        .user-list {
            list-style: none;
        }

        .user-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 5px;
            transition: all 0.3s;
            cursor: pointer;
            background: rgba(255, 255, 255, 0.02);
        }

        .user-item:hover {
            background: rgba(229, 62, 62, 0.1);
            transform: translateX(5px);
        }

        .avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 0.9em;
        }

        .chat-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: rgba(255, 255, 255, 0.02);
            backdrop-filter: blur(5px);
            min-height: 0; /* Important pour le scroll */
        }

        .messages-container {
            flex: 1;
            overflow-y: auto;
            overflow-x: hidden;
            padding: 25px;
            display: flex;
            flex-direction: column;
            gap: 18px;
            max-height: calc(100vh - 180px); /* Limite la hauteur - augmentée */
            scroll-behavior: smooth; /* Défilement fluide */
        }

        /* Amélioration du scrollbar */
        .messages-container::-webkit-scrollbar {
            width: 6px;
        }

        .messages-container::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 3px;
        }

        .messages-container::-webkit-scrollbar-thumb {
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            border-radius: 3px;
        }

        .messages-container::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(45deg, #dd3333, #cc5a1a);
        }

        .message {
            display: flex;
            animation: slideIn 0.3s ease-out;
            flex-shrink: 0; /* Empêche la compression des messages */
        }

        .message.new-message {
            animation: messageArrival 0.6s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes messageArrival {
            0% {
                opacity: 0;
                transform: translateY(20px) scale(0.9);
                box-shadow: 0 0 0 0 rgba(229, 62, 62, 0.7);
            }
            30% {
                opacity: 1;
                transform: translateY(-5px) scale(1.02);
                box-shadow: 0 0 15px 5px rgba(229, 62, 62, 0.3);
            }
            60% {
                transform: translateY(2px) scale(1.01);
                box-shadow: 0 0 10px 3px rgba(229, 62, 62, 0.2);
            }
            100% {
                opacity: 1;
                transform: translateY(0) scale(1);
                box-shadow: 0 0 0 0 rgba(229, 62, 62, 0);
            }
        }

        .message-content.flash {
            animation: messageFlash 0.6s ease-out;
        }

        @keyframes messageFlash {
            0% { background: rgba(229, 62, 62, 0.1); }
            50% { background: rgba(229, 62, 62, 0.3); }
            100% { background: rgba(255, 255, 255, 0.1); }
        }

        .message.own .message-content.flash {
            animation: ownMessageFlash 0.6s ease-out;
        }

        @keyframes ownMessageFlash {
            0% { 
                background: linear-gradient(45deg, #e53e3e, #dd6b20);
                transform: scale(1.05);
                box-shadow: 0 0 20px rgba(229, 62, 62, 0.6);
            }
            50% { 
                background: linear-gradient(45deg, #ff4d4d, #e67330);
                transform: scale(1.02);
                box-shadow: 0 0 15px rgba(229, 62, 62, 0.4);
            }
            100% { 
                background: linear-gradient(45deg, #e53e3e, #dd6b20);
                transform: scale(1);
                box-shadow: none;
            }
        }

        .message.own {
            justify-content: flex-end;
        }

        .message-content {
            max-width: 80%;
            padding: 16px 20px;
            border-radius: 20px;
            position: relative;
            word-wrap: break-word;
            word-break: break-word; /* Assure la césure des mots longs */
            min-width: 120px; /* Taille minimale */
        }

        .message.own .message-content {
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            color: white;
            border-bottom-right-radius: 5px;
        }

        .message:not(.own) .message-content {
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            border-bottom-left-radius: 5px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .message-header {
            font-size: 0.9em;
            font-weight: bold;
            opacity: 0.9;
            margin-bottom: 8px;
            color: #e53e3e;
        }

        .message.own .message-header {
            color: rgba(255, 255, 255, 0.9);
        }

        .message-text {
            line-height: 1.5;
            font-size: 1.1em;
            font-weight: 500;
        }

        .message-time {
            font-size: 0.8em;
            opacity: 0.7;
            margin-top: 8px;
            text-align: right;
        }

        .input-area {
            padding: 20px 25px;
            background: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            flex-shrink: 0; /* Empêche la zone de saisie de se compresser */
        }

        .input-container {
            display: flex;
            gap: 15px;
            align-items: center;
            max-width: 100%;
        }

        .message-input {
            flex: 1;
            padding: 15px 20px;
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 25px;
            font-size: 1.05em;
            outline: none;
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            transition: all 0.3s;
        }

        .message-input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .message-input:focus {
            border-color: #e53e3e;
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 0 0 3px rgba(229, 62, 62, 0.1);
        }

        .send-btn {
            padding: 15px 25px;
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            font-size: 1em;
        }

        .send-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(229, 62, 62, 0.4);
        }

        .send-btn:active {
            transform: translateY(0);
        }

        .login-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .login-form {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            max-width: 400px;
            width: 90%;
            border: 2px solid rgba(229, 62, 62, 0.3);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
        }

        .login-form h2 {
            color: #e53e3e;
            margin-bottom: 20px;
            font-size: 1.8em;
        }

        .login-form p {
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 25px;
        }

        .login-input {
            width: 100%;
            padding: 15px;
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 1em;
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            outline: none;
            transition: all 0.3s;
        }

        .login-input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .login-input:focus {
            border-color: #e53e3e;
            box-shadow: 0 0 0 3px rgba(229, 62, 62, 0.1);
        }

        .login-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, #e53e3e, #dd6b20);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }

        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(229, 62, 62, 0.3);
        }

        .typing-indicator {
            display: none;
            padding: 10px 20px;
            font-style: italic;
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.85em;
            flex-shrink: 0;
        }

        .typing-dots::after {
            content: '';
            animation: typing 1.5s infinite;
        }

        @keyframes typing {
            0% { content: ''; }
            25% { content: '.'; }
            50% { content: '..'; }
            75% { content: '...'; }
            100% { content: ''; }
        }

        .system-message {
            text-align: center;
            background: rgba(229, 62, 62, 0.1) !important;
            color: #e53e3e !important;
            font-style: italic;
            border: 1px solid rgba(229, 62, 62, 0.3);
            margin: 10px 0;
        }

        .music-controls {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.7);
            border-radius: 25px;
            padding: 10px 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 999;
            border: 1px solid rgba(229, 62, 62, 0.3);
        }

        .music-btn {
            background: none;
            border: none;
            color: #fff;
            cursor: pointer;
            font-size: 1.2em;
            padding: 5px;
            border-radius: 50%;
            transition: all 0.3s;
        }

        .music-btn:hover {
            background: rgba(229, 62, 62, 0.2);
            transform: scale(1.1);
        }

        .volume-slider {
            width: 80px;
            height: 4px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 2px;
            outline: none;
            cursor: pointer;
        }

        .volume-slider::-webkit-slider-thumb {
            appearance: none;
            width: 12px;
            height: 12px;
            background: #e53e3e;
            border-radius: 50%;
            cursor: pointer;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .sidebar {
                width: 250px;
            }
            
            .header h1 {
                font-size: 1.5em;
            }
            
            .message-content {
                max-width: 90%;
                padding: 14px 18px;
            }

            .message-text {
                font-size: 1.05em;
            }

            .messages-container {
                padding: 20px;
                gap: 15px;
                max-height: calc(100vh - 200px);
            }

            .music-controls {
                top: 10px;
                right: 10px;
                padding: 8px 12px;
            }

            .volume-slider {
                width: 60px;
            }
        }

        @media (max-width: 600px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: 180px;
                border-right: none;
                border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            }
            
            .user-list {
                display: flex;
                gap: 10px;
                overflow-x: auto;
                padding-bottom: 10px;
            }
            
            .user-item {
                min-width: 120px;
                margin-bottom: 0;
            }

            .messages-container {
                max-height: calc(100vh - 320px);
                padding: 15px;
                gap: 12px;
            }

            .message-content {
                max-width: 95%;
                padding: 12px 16px;
            }

            .message-text {
                font-size: 1em;
            }

            .input-area {
                padding: 15px 20px;
            }

            .message-input {
                padding: 12px 16px;
                font-size: 1em;
            }

            .send-btn {
                padding: 12px 20px;
                font-size: 0.95em;
            }
        }
    </style>
</head>
<body>
    <!-- Contrôles musique -->
    <div class="music-controls" id="musicControls">
        <button class="music-btn" id="musicToggle" title="Activer/Désactiver la musique">🎵</button>
        <input type="range" class="volume-slider" id="volumeSlider" min="0" max="100" value="30" title="Volume">
    </div>

    <!-- Audio pour la musique d'ambiance -->
    <audio id="backgroundMusic" loop>
        <source src="https://www.soundjay.com/misc/sounds/bell-ringing-05.wav" type="audio/wav">
        <!-- Fallback: utilisation d'un son de notification simple -->
    </audio>

    <div class="login-overlay" id="loginOverlay">
        <div class="login-form">
            <h2>🎯 Discours du Clan X-TMP</h2>
            <p>Rejoignez la discussion du clan</p>
            <input type="text" class="login-input" id="usernameInput" placeholder="Votre pseudonyme..." maxlength="15">
            <button class="login-btn" onclick="login()">Rejoindre le clan</button>
        </div>
    </div>

    <div class="container">
        <div class="header">
            <h1>🎯 Discours du Clan X-TMP</h1>
            <div class="user-info">
                <div class="online-users">
                    <span>👥 Membres actifs:</span>
                    <div id="userCount" class="user-badge">
                        <div class="status-dot"></div>
                        <span id="countText">0 membre</span>
                    </div>
                </div>
                <div class="user-badge">
                    <span>👤 <span id="currentUser">Vous</span></span>
                </div>
            </div>
        </div>

        <div class="main-content">
            <div class="sidebar">
                <h3>👥 Membres en ligne</h3>
                <ul class="user-list" id="userList">
                </ul>
            </div>

            <div class="chat-area">
                <div class="messages-container" id="messagesContainer">
                    <div class="message">
                        <div class="message-content system-message">
                            <div class="message-text">💬 Bienvenue dans le chat du Clan X-TMP ! Les messages s'affichent pour tous les membres connectés.</div>
                        </div>
                    </div>
                </div>

                <div class="typing-indicator" id="typingIndicator">
                    <span class="typing-dots">Un membre écrit</span>
                </div>

                <div class="input-area">
                    <div class="input-container">
                        <input type="text" class="message-input" id="messageInput" placeholder="Écrivez votre message au clan..." maxlength="500">
                        <button class="send-btn" onclick="sendMessage()">📤 Envoyer</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        let currentUsername = '';
        let onlineUsers = [];
        let allMess
