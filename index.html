<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StreamStudio WebRTC</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    
    <style>
        body { 
            font-family: 'Inter', sans-serif; 
            margin: 0;
            padding: 0;
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #1f1f23; }
        ::-webkit-scrollbar-thumb { background: #555; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #777; }

        .chat-message { animation: fadeIn 0.3s ease-out; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .pulse-record { animation: pulse-red 2s infinite; }
        @keyframes pulse-red {
            0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(239, 68, 68, 0); }
            100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
        }

        /* Video container handling */
        .video-wrapper {
            position: relative;
            width: 100%;
            height: 100%;
            background: #000;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 0.5rem;
        }

        /* Remote Video (Friend) - Large view */
        #remoteVideo {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 0.5rem;
            z-index: 5; /* Below PIP */
        }
        
        /* Local Video (You) - Picture-in-Picture (PIP) */
        #localVideoPip {
            position: absolute;
            bottom: 20px; 
            right: 20px;
            width: 200px; 
            height: 120px;
            border: 4px solid #a855f7;
            border-radius: 8px;
            z-index: 10;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
            object-fit: cover;
            transform: scaleX(-1); /* Flip local video horizontally for natural viewing */
        }
        
        /* Remote Placeholder */
        .remote-placeholder {
            filter: grayscale(100%);
            opacity: 0.5;
        }
    </style>
</head>
<body class="bg-[#0e0e10] text-white overflow-hidden">

    <div class="h-screen flex flex-col"> 
    
        <!-- Top Navbar -->
        <header class="h-14 bg-[#18181b] border-b border-[#2d2d30] flex items-center justify-between px-4 shrink-0">
            <div class="flex items-center gap-2">
                <i class="fas fa-video text-purple-500 text-xl"></i>
                <h1 class="font-bold text-lg tracking-tight">Stream<span class="text-purple-500">Studio</span></h1>
            </div>
            
            <div class="flex items-center gap-6 bg-[#00000040] px-4 py-1 rounded-full border border-[#ffffff10]">
                <div class="flex items-center gap-2" id="live-indicator" style="opacity: 0.3;">
                    <div class="w-3 h-3 rounded-full bg-red-500"></div>
                    <span class="font-semibold text-sm text-red-500 uppercase">Офлайн</span>
                </div>
                <div class="h-4 w-[1px] bg-gray-600"></div>
                <div class="flex items-center gap-2 text-gray-300">
                    <i class="fas fa-eye text-xs"></i>
                    <span class="text-sm font-mono" id="viewer-count">1</span>
                </div>
                <div class="flex items-center gap-2 text-gray-300">
                    <i class="fas fa-clock text-xs"></i>
                    <span class="text-sm font-mono" id="stream-timer">00:00:00</span>
                </div>
            </div>

            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-purple-500 to-pink-500 flex items-center justify-center font-bold text-sm">
                    <span id="user-initials">В</span>
                </div>
                <span class="text-xs text-gray-400" id="user-id-display">Загрузка...</span>
            </div>
        </header>

        <!-- Main Content -->
        <main class="flex-1 flex overflow-hidden">
            
            <!-- Left Side: Stream Preview & Controls -->
            <section class="flex-1 flex flex-col p-4 gap-4 min-w-0">
                
                <!-- Video Area (Main Screen for Remote, PIP for Local) -->
                <div class="flex-1 video-wrapper border border-[#2d2d30] shadow-2xl relative group">
                    
                    <!-- Remote Video (Friend) - Large -->
                    <video id="remoteVideo" autoplay playsinline class="remote-placeholder" poster="https://placehold.co/1280x720/1f2937/ffffff?text=Ожидание+собеседника"></video>
                    
                    <!-- Local Video (You) - PIP -->
                    <video id="localVideoPip" autoplay muted playsinline></video>

                    <!-- Status Overlay -->
                    <div id="connection-status-overlay" class="absolute inset-0 flex flex-col items-center justify-center z-20 bg-black bg-opacity-70 text-center p-8">
                        <div id="initial-action-prompt">
                            <i class="fas fa-satellite-dish text-6xl text-purple-400 mb-4"></i>
                            <h2 class="text-2xl font-bold mb-2">Начните совместный эфир</h2>
                            <p class="text-gray-300 mb-6 max-w-sm">
                                Чтобы позвонить другу, вам нужно создать комнату (получить код) или присоединиться к существующей комнате по коду.
                            </p>
                            
                            <!-- Join/Create Controls -->
                            <div class="flex flex-col gap-3 max-w-md mx-auto">
                                <input type="text" id="room-code-input" placeholder="Введите код комнаты (6 цифр)" maxlength="6" class="p-3 rounded-lg bg-[#2d2d30] text-white text-center text-xl font-mono tracking-widest outline-none border border-gray-600 focus:border-purple-500 transition" oninput="this.value = this.value.replace(/[^0-9]/g, '')">

                                <div class="flex gap-4">
                                    <button onclick="joinCallFromInput()" id="btn-join-call" class="flex-1 px-6 py-3 rounded-full bg-purple-600 hover:bg-purple-700 font-bold transition shadow-lg shadow-purple-900/20 flex items-center justify-center gap-2 disabled:opacity-50" disabled>
                                        <i class="fas fa-sign-in-alt"></i> Присоединиться
                                    </button>
                                    <button onclick="startCall()" id="btn-create-call" class="flex-1 px-6 py-3 rounded-full bg-yellow-600 hover:bg-yellow-700 font-bold transition shadow-lg shadow-yellow-900/20 flex items-center justify-center gap-2 disabled:opacity-50" disabled>
                                        <i class="fas fa-plus"></i> Создать комнату
                                    </button>
                                </div>
                            </div>
                            <p class="text-xs text-gray-500 mt-4">Сначала разрешите доступ к камере/микрофону.</p>

                        </div>
                        
                        <div id="signaling-progress" class="hidden">
                            <div class="text-center">
                                <i class="fas fa-link text-5xl text-yellow-500 mb-4 animate-pulse"></i>
                                <h2 class="text-xl font-bold mb-2" id="progress-title">Создание комнаты...</h2>
                                <p class="text-gray-300 mb-4" id="progress-message">Ожидайте автоматического соединения или отправьте код другу.</p>
                                
                                <!-- Share Code UI -->
                                <div id="share-code-box" class="mt-4 w-full max-w-lg mx-auto">
                                    <label class="block text-sm font-medium text-gray-400 mb-2 text-left">Код вашей комнаты (сообщите другу):</label>
                                    <div class="flex">
                                        <input id="share-code-input" type="text" readonly class="flex-1 p-3 rounded-lg bg-[#2d2d30] text-center text-3xl font-mono text-yellow-300 outline-none border border-yellow-500 tracking-widest">
                                    </div>
                                    <p class="text-xs text-gray-400 mt-2">Ваш друг должен ввести этот код в поле "Присоединиться", чтобы начать звонок.</p>
                                </div>
                            </div>
                        </div>
                    </div>


                    <!-- Placeholder when no camera -->
                    <div id="no-signal" class="absolute inset-0 flex flex-col items-center justify-center z-30 bg-[#0e0e10] hidden">
                        <i class="fas fa-video-slash text-6xl text-gray-600 mb-4"></i>
                        <p class="text-gray-400">Камера отключена или недоступна</p>
                        <p class="text-sm text-gray-500 mt-1">Для работы нужен доступ к камере.</p>
                        <button onclick="initMedia()" class="mt-4 px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded font-medium transition">
                            Разрешить доступ
                        </button>
                        <div id="media-error-display" class="mt-4 text-red-400 text-sm hidden"></div>
                    </div>
                </div>

                <!-- Control Bar -->
                <div class="h-28 bg-[#18181b] rounded-xl border border-[#2d2d30] flex items-center justify-between px-6 shrink-0">
                    
                    <div class="flex items-center gap-2">
                        <div class="text-xs text-gray-400 uppercase font-semibold mb-1 absolute -mt-16 ml-1">Источники</div>
                        <button onclick="toggleCamera()" id="btn-cam" class="w-12 h-12 rounded-lg bg-[#2d2d30] hover:bg-[#3d3d40] flex items-center justify-center transition text-white" disabled>
                            <i class="fas fa-video"></i>
                        </button>
                        <button onclick="toggleMic()" id="btn-mic" class="w-12 h-12 rounded-lg bg-[#2d2d30] hover:bg-[#3d3d40] flex items-center justify-center transition text-white" disabled>
                            <i class="fas fa-microphone"></i>
                        </button>
                    </div>

                    <!-- Title and Description Generator Feature -->
                    <div class="flex flex-col items-center">
                        <div class="text-xs text-gray-400 uppercase font-semibold mb-1 absolute -mt-16">Название и Описание</div>
                        <div class="flex items-center gap-2">
                            <input type="text" id="stream-title" placeholder="Название вашей трансляции..." class="bg-transparent text-center border-b border-gray-600 focus:border-purple-500 outline-none w-64 pb-1 text-sm font-medium placeholder-gray-500 transition" value="Наша общая трансляция">
                            <button onclick="generateStreamDescription(this)" id="btn-desc-gen" class="text-purple-400 hover:text-purple-300 text-sm transition" title="Сгенерировать описание стрима">
                                ✨ Описание
                            </button>
                        </div>
                        <textarea id="stream-description" rows="2" placeholder="Опишите свой стрим (до 150 символов)..." class="mt-2 w-full max-w-sm bg-[#2d2d30] border border-gray-600 rounded p-1 text-xs resize-none placeholder-gray-400 focus:border-purple-500 outline-none transition"></textarea>
                    </div>

                    <div>
                        <button onclick="toggleStreamState()" id="btn-stream" class="px-6 py-3 rounded-lg bg-red-600 hover:bg-red-700 font-bold tracking-wide transition shadow-lg shadow-red-900/20 flex items-center gap-2 disabled:opacity-50" disabled>
                            <div class="w-2 h-2 rounded-full bg-white animate-pulse hidden" id="rec-dot"></div>
                            <span id="stream-text">Начать эфир</span>
                        </button>
                    </div>
                </div>
            </section>

            <!-- Right Side: Chat (Restored) -->
            <aside class="w-80 bg-[#18181b] border-l border-[#2d2d30] flex flex-col shrink-0 hidden md:flex">
                <div class="h-12 border-b border-[#2d2d30] flex items-center justify-center gap-2">
                    <h2 class="font-semibold text-sm uppercase tracking-wider text-gray-300">Чат трансляции</h2>
                </div>
                
                <!-- Chat Messages Area -->
                <div id="chat-container" class="flex-1 overflow-y-auto p-4 space-y-3 relative">
                    <div class="text-center text-gray-500 text-sm mt-10" id="initial-chat-message">
                        <i class="fas fa-comments text-4xl mb-2 opacity-50"></i>
                        <p id="chat-status-text">Ожидание соединения с Firebase...</p>
                    </div>
                </div>

                <!-- Chat Input -->
                <div class="p-4 border-t border-[#2d2d30] bg-[#18181b]">
                    <form onsubmit="handleUserMessage(event)" class="relative">
                        <input type="text" id="chat-input" placeholder="Отправить сообщение..." class="w-full bg-[#0e0e10] border border-[#2d2d30] rounded-lg py-3 pl-4 pr-20 text-sm focus:outline-none focus:border-purple-500 transition text-gray-200" disabled>
                        
                        <!-- TTS Announcement Feature -->
                        <button type="button" onclick="handleTTSAnnouncement(this)" id="btn-tts" class="absolute right-10 top-2 h-8 w-8 flex items-center justify-center text-green-500 hover:text-green-400 transition" title="Объявить сообщение голосом (TTS)">
                            <i class="fas fa-volume-up"></i>
                        </button>

                        <button type="submit" class="absolute right-2 top-2 h-8 w-8 flex items-center justify-center text-purple-500 hover:text-purple-400" title="Отправить в чат" disabled>
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </form>
                    <div class="flex justify-between items-center mt-2 px-1">
                        <div class="text-xs text-gray-500 font-bold">1500 баллов</div>
                        <button class="text-gray-400 hover:text-white"><i class="fas fa-smile"></i></button>
                    </div>
                </div>
            </aside>
        </main>
    </div>


    <script type="module">
        // === FIREBASE IMPORTS ===
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, onSnapshot, updateDoc, deleteDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        
        // setLogLevel('debug'); // Uncomment for detailed debug logs

        // === GEMINI API CONFIGURATION (for Chat and TTS) ===
        const apiKey = "";
        const textApiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
        const ttsApiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`;

        // === GLOBAL VARIABLES & FIREBASE INIT ===
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');

        let app;
        let db;
        let auth;
        let userId = 'loading';
        let isAuthReady = false;

        let mediaStream = null;
        let pc = null; // RTCPeerConnection
        let dataChannel = null; // RTCDataChannel for chat
        let timerInterval;
        let seconds = 0;
        let isConnected = false; // WebRTC connection status
        let currentRoomId = null;

        // WebRTC Configuration
        const iceServers = {
            iceServers: [
                { urls: 'stun:stun.l.google.com:19302' },
                { urls: 'stun:stun1.l.google.com:19302' }
            ]
        };

        // DOM Elements
        const localVideoPip = document.getElementById('localVideoPip');
        const remoteVideo = document.getElementById('remoteVideo');
        const noSignal = document.getElementById('no-signal');
        const mediaErrorDisplay = document.getElementById('media-error-display');
        const chatContainer = document.getElementById('chat-container');
        const chatStatusText = document.getElementById('chat-status-text');
        const timerEl = document.getElementById('stream-timer');
        const viewerEl = document.getElementById('viewer-count');
        const btnCreateCall = document.getElementById('btn-create-call');
        const btnJoinCall = document.getElementById('btn-join-call');
        const roomCodeInput = document.getElementById('room-code-input');
        const initialActionPrompt = document.getElementById('initial-action-prompt');
        const signalingProgress = document.getElementById('signaling-progress');
        const progressTitle = document.getElementById('progress-title');
        const progressMessage = document.getElementById('progress-message');
        const shareCodeBox = document.getElementById('share-code-box');
        const shareCodeInput = document.getElementById('share-code-input');
        const connectionStatusOverlay = document.getElementById('connection-status-overlay');
        const chatInput = document.getElementById('chat-input');
        const chatSendButton = document.querySelector('.fa-paper-plane').parentElement; // Corrected selector

        
        // === UTILITIES ===

        function generateRandomCode() {
            // Generates a 6-digit numeric code
            return Math.floor(100000 + Math.random() * 900000).toString();
        }
        
        function getRoomDocRef(roomId) {
            // Using the public path for collaborative data
            return doc(db, `artifacts/${appId}/public/data/rooms`, roomId);
        }

        function updateUIOnRoomLoad(id) {
            currentRoomId = id;
            
            initialActionPrompt.classList.add('hidden');
            signalingProgress.classList.remove('hidden');
            shareCodeBox.classList.remove('hidden');
            shareCodeInput.value = id;
            
            btnCreateCall.disabled = true;
            btnJoinCall.disabled = true;
            document.getElementById('btn-stream').disabled = false;
        }

        async function fetchWithRetry(url, options, maxRetries = 5) {
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (!response.ok) {
                        if (response.status === 429 || response.status >= 500) {
                            throw new Error(`Server error: ${response.statusText}`);
                        }
                        throw new Error(`HTTP error! status: ${response.status}`);
                    }
                    return response;
                } catch (error) {
                    if (i < maxRetries - 1) {
                        const delay = Math.pow(2, i) * 1000 + Math.random() * 1000;
                        await new Promise(resolve => setTimeout(resolve, delay));
                    } else {
                        console.error("Fetch failed after max retries:", error);
                        throw error;
                    }
                }
            }
        }
        
        function addSystemMessage(text, isError = false) {
            const initialChatMsg = document.getElementById('initial-chat-message');
            if (initialChatMsg && chatContainer.contains(initialChatMsg)) {
                 initialChatMsg.remove();
            }
            const div = document.createElement('div');
            div.className = `text-xs italic text-center my-2 ${isError ? 'text-red-400' : 'text-gray-500'}`;
            div.innerText = text;
            chatContainer.appendChild(div);
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }
        
        function displayMediaError(message) {
            mediaErrorDisplay.innerText = message;
            mediaErrorDisplay.classList.remove('hidden');
        }

        function base64ToArrayBuffer(base64) {
            const binary_string = window.atob(base64);
            const len = binary_string.length;
            const bytes = new Uint8Array(len);
            for (let i = 0; i < len; i++) {
                bytes[i] = binary_string.charCodeAt(i);
            }
            return bytes.buffer;
        }
        
        function writeString(view, offset, string) {
            for (let i = 0; i < string.length; i++) {
                view.setUint8(offset + i, string.charCodeAt(i));
            }
        }
        function pcmToWav(pcm16, sampleRate) {
            const numChannels = 1;
            const bitsPerSample = 16;
            const bytesPerSample = bitsPerSample / 8;
            const blockAlign = numChannels * bytesPerSample;
            const byteRate = sampleRate * blockAlign;
            const dataSize = pcm16.length * bytesPerSample;

            const buffer = new ArrayBuffer(44 + dataSize);
            const view = new DataView(buffer);

            writeString(view, 0, 'RIFF');
            view.setUint32(4, 36 + dataSize, true); 
            writeString(view, 8, 'WAVE');

            writeString(view, 12, 'fmt ');
            view.setUint32(16, 16, true); 
            view.setUint16(20, 1, true); 
            view.setUint16(22, numChannels, true);
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, byteRate, true);
            view.setUint16(32, blockAlign, true);
            view.setUint16(34, bitsPerSample, true);

            writeString(view, 36, 'data');
            view.setUint32(40, dataSize, true);

            for (let i = 0; i < pcm16.length; i++) {
                view.setInt16(44 + i * bytesPerSample, pcm16[i], true);
            }

            return new Blob([buffer], { type: 'audio/wav' });
        }


        // === MEDIA CONTROLS ===

        async function initMedia() {
            if (mediaStream) return true;

            try {
                mediaStream = await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
                localVideoPip.srcObject = mediaStream;

                noSignal.classList.add('hidden');
                connectionStatusOverlay.classList.remove('hidden'); // Show initial action prompt

                // Enable media and call buttons
                document.getElementById('btn-cam').disabled = false;
                document.getElementById('btn-mic').disabled = false;
                btnCreateCall.disabled = false;
                btnJoinCall.disabled = false;


                addSystemMessage("Шаг 1/3: Камера и микрофон подключены. Теперь вы можете создать комнату или присоединиться.");
                return true;

            } catch (err) {
                console.error("Error accessing media:", err);
                let message = "";
                if (err.name === "NotAllowedError" || err.name === "SecurityError") {
                    message = "Доступ к камере/микрофону заблокирован. Проверьте разрешения браузера.";
                } else if (err.name === "NotFoundError") {
                    message = "Камера не найдена.";
                } else {
                    message = `Ошибка доступа: ${err.message || 'Неизвестная ошибка'}`;
                }
                
                displayMediaError(message);
                noSignal.classList.remove('hidden'); // Show the 'no signal' UI
                connectionStatusOverlay.classList.add('hidden'); // Hide overlay if camera fails

                addSystemMessage(`Ошибка доступа: ${message}`, true);
                return false;
            }
        }

        function toggleCamera() {
            if (mediaStream) {
                const videoTrack = mediaStream.getVideoTracks()[0];
                videoTrack.enabled = !videoTrack.enabled;
                const btn = document.getElementById('btn-cam');
                btn.classList.toggle('bg-red-500', !videoTrack.enabled);
                btn.classList.toggle('bg-[#2d2d30]', videoTrack.enabled);
            }
        }

        function toggleMic() {
            if (mediaStream) {
                const audioTrack = mediaStream.getAudioTracks()[0];
                audioTrack.enabled = !audioTrack.enabled;
                const btn = document.getElementById('btn-mic');
                btn.classList.toggle('bg-red-500', !audioTrack.enabled);
                btn.classList.toggle('bg-[#2d2d30]', audioTrack.enabled);
                const icon = btn.querySelector('i');
                icon.className = audioTrack.enabled ? 'fas fa-microphone' : 'fas fa-microphone-slash';
            }
        }


        // === WebRTC SIGNALING & DATADCHANNEL LOGIC (Firestore Based) ===

        function setupDataChannelHandlers(dc) {
            dataChannel = dc;
            // Enable chat input only when the channel is open
            dc.onopen = () => {
                addSystemMessage("Шаг 3/3: DataChannel: Канал чата открыт! Соединение WebRTC завершено.");
                viewerEl.innerText = "2";
                chatInput.disabled = false;
                chatSendButton.disabled = false;
            };
            dc.onmessage = (event) => {
                try {
                    const data = JSON.parse(event.data);
                    if (data.type === 'chat') {
                        addChatMessage("Собеседник", data.message, "#eab308");
                    }
                } catch (e) {
                    console.error("Error parsing data channel message:", e);
                }
            };
            dc.onclose = () => {
                addSystemMessage("WebRTC: Соединение закрыто. DataChannel отключен.", true);
                dataChannel = null;
                viewerEl.innerText = "1";
                chatInput.disabled = true;
                chatSendButton.disabled = true;
            };
            dc.onerror = (error) => {
                console.error("DataChannel Error:", error);
                addSystemMessage("Ошибка DataChannel: Проблема с каналом чата.", true);
            };
        }

        function createPeerConnection(isCreator) {
            if (pc) return;

            pc = new RTCPeerConnection(iceServers);

            // 1. Setup local stream tracks
            if (mediaStream) {
                mediaStream.getTracks().forEach(track => pc.addTrack(track, mediaStream));
            } else {
                addSystemMessage("Ошибка: Медиапоток недоступен для WebRTC.", true);
                return;
            }

            // 2. Setup remote stream
            pc.ontrack = (event) => {
                if (remoteVideo.srcObject !== event.streams[0]) {
                    remoteVideo.srcObject = event.streams[0];
                    remoteVideo.classList.remove('remote-placeholder');
                    isConnected = true;
                    connectionStatusOverlay.classList.add('hidden'); // Hide overlay on successful connection
                    addSystemMessage("WebRTC: Видеопоток получен. Соединение успешно установлено!");
                }
            };

            // 3. Setup Data Channel
            if (isCreator) {
                // Creator creates the channel
                const channel = pc.createDataChannel("chat-channel");
                setupDataChannelHandlers(channel);
                addSystemMessage("Шаг 2/3: Создан RTCPeerConnection и DataChannel. Ожидание Answer...");
            } else {
                // Joiner listens for the remote channel
                pc.ondatachannel = (event) => {
                    addSystemMessage("Шаг 2/3: Создан RTCPeerConnection. Получен удаленный DataChannel. Настройка чата...");
                    setupDataChannelHandlers(event.channel);
                };
            }
            
            // 4. Handle ICE candidates and send them to Firestore
            pc.onicecandidate = async (event) => {
                if (event.candidate) {
                    await addIceCandidateToFirestore(currentRoomId, event.candidate.toJSON());
                }
            };

            pc.oniceconnectionstatechange = () => {
                if (pc.iceConnectionState === 'failed' || pc.iceConnectionState === 'disconnected' || pc.iceConnectionState === 'closed') {
                    addSystemMessage(`WebRTC: Соединение прервано. Состояние: ${pc.iceConnectionState}.`, true);
                    isConnected = false;
                    remoteVideo.classList.add('remote-placeholder');
                    remoteVideo.srcObject = null;
                    viewerEl.innerText = "1";
                    
                    // Re-enable controls if connection closes
                    if (currentRoomId) {
                        currentRoomId = null;
                        btnCreateCall.disabled = false;
                        btnJoinCall.disabled = false;
                        initialActionPrompt.classList.remove('hidden');
                        signalingProgress.classList.add('hidden');
                        shareCodeBox.classList.add('hidden');
                        document.getElementById('btn-stream').disabled = true;
                    }
                }
            };
        }

        async function addIceCandidateToFirestore(roomId, candidate) {
             if (!db || !roomId) return;
             const roomRef = getRoomDocRef(roomId);
             try {
                 // Fetch current data to ensure non-destructive update of the array
                 const roomData = (await getDoc(roomRef)).data();
                 const currentCandidates = roomData?.iceCandidates || [];
                 
                 await updateDoc(roomRef, {
                    iceCandidates: [...currentCandidates, candidate]
                 });
             } catch (e) {
                 // This is expected if the document is being created simultaneously
                 console.warn("Could not add ICE candidate:", e);
             }
        }
        
        async function getRoomData(roomId) {
            const docSnap = await getDoc(getRoomDocRef(roomId));
            return docSnap.exists() ? docSnap.data() : null;
        }

        async function setupFirestoreSignaling(roomId, isCreator) {
            if (!isAuthReady) return;
            
            const roomRef = getRoomDocRef(roomId);

            if (isCreator) {
                progressTitle.textContent = "Комната создана! Сообщите код другу.";
                progressMessage.textContent = "Ожидание, пока друг зайдет и отправит Answer...";
                
                // Initial creation (ensure it exists and marks self as creator)
                await setDoc(roomRef, {
                    creatorId: userId,
                    joinerId: null,
                    offer: null,
                    answer: null,
                    iceCandidates: []
                }, { merge: true });
                
                createPeerConnection(true);

                const offer = await pc.createOffer();
                await pc.setLocalDescription(offer);
                
                // Save the Offer to Firestore
                await updateDoc(roomRef, {
                    offer: { sdp: pc.localDescription.sdp, type: pc.localDescription.type }
                });
                addSystemMessage("WebRTC Offer отправлен через Firestore.");
                
            } else {
                // Joiner must check if room exists
                const initialRoomData = await getRoomData(roomId);
                if (!initialRoomData || !initialRoomData.creatorId) {
                    progressTitle.textContent = "Ошибка: Комната не найдена.";
                    progressMessage.textContent = "Пожалуйста, проверьте код и попробуйте снова.";
                    addSystemMessage("Комната не найдена. Проверьте код.", true);
                    
                    // Restore UI
                    currentRoomId = null;
                    initialActionPrompt.classList.remove('hidden');
                    signalingProgress.classList.add('hidden');
                    shareCodeBox.classList.add('hidden');
                    btnCreateCall.disabled = false;
                    btnJoinCall.disabled = false;
                    
                    if (pc) pc.close();
                    return;
                }

                progressTitle.textContent = "Соединение с комнатой...";
                progressMessage.textContent = "Получение Offer и создание Answer...";
                createPeerConnection(false);
            }
            
            // Start listening for changes (Offer, Answer, ICE Candidates)
            onSnapshot(roomRef, async (docSnap) => {
                if (!docSnap.exists()) {
                    if (pc) pc.close();
                    progressTitle.textContent = "Соединение разорвано.";
                    progressMessage.textContent = "Комната удалена ее создателем.";
                    addSystemMessage("Комната удалена. Разрываю WebRTC.", true);
                    
                    // Restore UI
                    currentRoomId = null;
                    initialActionPrompt.classList.remove('hidden');
                    signalingProgress.classList.add('hidden');
                    shareCodeBox.classList.add('hidden');
                    btnCreateCall.disabled = false;
                    btnJoinCall.disabled = false;
                    return;
                }
                
                const data = docSnap.data();

                // 1. Handle Remote Description (Offer/Answer)
                if (isCreator && data.answer && pc.remoteDescription?.type !== 'answer') {
                    // Creator receives Answer
                    progressTitle.textContent = "Получен Answer!";
                    progressMessage.textContent = "Установка соединения...";
                    await pc.setRemoteDescription(new RTCSessionDescription(data.answer));
                    addSystemMessage("WebRTC Answer получен и применен. Ждем ICE кандидатов.");
                    
                } else if (!isCreator && data.offer && pc.remoteDescription?.type !== 'offer') {
                    // Joiner receives Offer
                    progressTitle.textContent = "Получен Offer!";
                    progressMessage.textContent = "Создание и отправка Answer...";
                    await pc.setRemoteDescription(new RTCSessionDescription(data.offer));
                    
                    // Joiner creates Answer and saves it
                    const answer = await pc.createAnswer();
                    await pc.setLocalDescription(answer);

                    await setDoc(roomRef, {
                        joinerId: userId,
                        answer: { sdp: pc.localDescription.sdp, type: pc.localDescription.type }
                    }, { merge: true });
                    addSystemMessage("WebRTC Answer создан и отправлен через Firestore. Ждем ICE кандидатов.");
                    viewerEl.innerText = "2";
                }
                
                // 2. Handle ICE Candidates
                if (data.iceCandidates && data.iceCandidates.length > 0) {
                    // Process all candidates
                    for (const candidate of data.iceCandidates) {
                        try {
                            if (pc.remoteDescription) { 
                                await pc.addIceCandidate(new RTCIceCandidate(candidate));
                            }
                        } catch (e) {
                            console.error("Error adding remote ICE candidate:", e);
                        }
                    }
                    // Clear candidates after processing to avoid reprocessing
                    await updateDoc(roomRef, { iceCandidates: [] });
                }
            });
        }


        // === PUBLIC ACTIONS (Called from UI) ===

        window.startCall = async function() {
            if (!isAuthReady || currentRoomId) {
                addSystemMessage("Пожалуйста, подождите, идет инициализация или звонок уже начат.", true);
                return;
            }

            const mediaOk = await initMedia();
            if (!mediaOk) return;

            const newRoomId = generateRandomCode(); // Use a new random code
            updateUIOnRoomLoad(newRoomId);
            
            await setupFirestoreSignaling(newRoomId, true);
        }
        
        window.joinCallFromInput = async function() {
            const roomId = roomCodeInput.value.trim();
            if (roomId.length !== 6) {
                addSystemMessage("Ошибка: Код комнаты должен состоять из 6 цифр.", true);
                return;
            }
            if (!isAuthReady || currentRoomId) {
                addSystemMessage("Пожалуйста, подождите, идет инициализация или звонок уже начат.", true);
                return;
            }

            const mediaOk = await initMedia();
            if (!mediaOk) return;

            // Check if room exists before starting signaling
            const roomData = await getRoomData(roomId);
            if (!roomData) {
                addSystemMessage(`Комната с кодом ${roomId} не найдена. Проверьте код.`, true);
                return;
            }

            updateUIOnRoomLoad(roomId);
            await setupFirestoreSignaling(roomId, false);
        }

        // === STREAMING/RECORDING LOGIC (Simplified, just for UI) ===
        
        let isStreaming = false;
        
        window.toggleStreamState = function() {
             if (isStreaming) {
                stopStream();
            } else {
                startStream();
            }
        }

        function startStream() {
            if (isStreaming) return;
            isStreaming = true;
            
            // UI Updates
            const btnStream = document.getElementById('btn-stream');
            const streamText = document.getElementById('stream-text');
            const liveIndicator = document.getElementById('live-indicator');
            const liveText = liveIndicator.querySelector('span');
            const recDot = document.getElementById('rec-dot');

            btnStream.classList.replace('bg-red-600', 'bg-gray-700');
            btnStream.classList.replace('hover:bg-red-700', 'hover:bg-gray-600');
            streamText.innerText = "Закончить";
            recDot.classList.remove('hidden');
            liveIndicator.style.opacity = "1";
            liveText.innerText = "В ЭФИРЕ";
            liveText.classList.add('pulse-record');

            // Logic
            startTimer();
            addSystemMessage("Симуляция стрима запущена.");
        }

        function stopStream() {
            isStreaming = false;
            
            // UI Updates
            const btnStream = document.getElementById('btn-stream');
            const streamText = document.getElementById('stream-text');
            const liveIndicator = document.getElementById('live-indicator');
            const liveText = liveIndicator.querySelector('span');
            const recDot = document.getElementById('rec-dot');

            btnStream.classList.replace('bg-gray-700', 'bg-red-600');
            btnStream.classList.replace('hover:bg-gray-600', 'hover:bg-red-700');
            streamText.innerText = "Начать эфир";
            liveIndicator.style.opacity = "0.3";
            liveText.innerText = "ОФЛАЙН";
            liveText.classList.remove('pulse-record');
            recDot.classList.add('hidden');

            // Logic
            stopTimer();
            addSystemMessage("Симуляция стрима завершена.");
        }


        // === SIMULATION LOGIC (Only Timer remains) ===

        function startTimer() {
            seconds = 0;
            timerEl.innerText = "00:00:00";
            timerInterval = setInterval(() => {
                seconds++;
                const h = Math.floor(seconds / 3600).toString().padStart(2, '0');
                const m = Math.floor((seconds % 3600) / 60).toString().padStart(2, '0');
                const s = (seconds % 60).toString().padStart(2, '0');
                timerEl.innerText = `${h}:${m}:${s}`;
            }, 1000);
        }

        function stopTimer() {
            clearInterval(timerInterval);
        }

        // === CHAT & GEMINI INTEGRATION ===

        window.handleUserMessage = function(e) {
            e.preventDefault();
            const input = document.getElementById('chat-input');
            const text = input.value.trim();
            if (text) {
                // Send message over data channel if connected
                if (dataChannel && dataChannel.readyState === 'open') {
                    const messagePayload = {
                        type: 'chat',
                        message: text
                    };
                    dataChannel.send(JSON.stringify(messagePayload));
                    addChatMessage("Вы (Стример)", text, "#a855f7", true); // Display locally immediately
                    addSystemMessage("Сообщение отправлено по WebRTC DataChannel.");
                } else {
                    // Send locally only if there is no active connection
                    addChatMessage("Вы (Стример)", text, "#a855f7", true);
                    addSystemMessage("Сообщение отправлено ЛОКАЛЬНО (WebRTC DataChannel не активен).", true);
                }
                input.value = "";
            }
        }

        function addChatMessage(name, text, color, isOwner = false) {
            const initialChatMsg = document.getElementById('initial-chat-message');
            if (initialChatMsg && chatContainer.contains(initialChatMsg)) { 
                initialChatMsg.remove();
            }

            const div = document.createElement('div');
            div.className = "chat-message text-sm break-words flex flex-wrap items-baseline";
            
            const badge = isOwner ? `<span class="bg-purple-600 text-white text-[10px] px-1 rounded mr-1">BROADCASTER</span>` : '';

            const escapedText = text.replace(/'/g, "\\'").replace(/"/g, '\\"');
            const escapedName = name.replace(/'/g, "\\'").replace(/"/g, '\\"');
            
            const replyButton = isOwner ? '' : `
                <button onclick="generateStreamerResponse('${escapedName}', '${escapedText}', this)" 
                        class="ml-2 text-purple-400 hover:text-purple-300 text-xs font-semibold whitespace-nowrap disabled:opacity-50 transition" title="Сгенерировать ответ с помощью Gemini">
                    ✨ Ответить
                </button>`;

            div.innerHTML = `
                <div class="flex items-baseline">
                    <span class="font-bold cursor-pointer hover:underline" style="color: ${color}">${name}</span>:
                    ${badge}<span class="text-gray-300">${text}</span>
                    ${replyButton}
                </div>
            `;
            
            chatContainer.appendChild(div);
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }

        window.generateStreamerResponse = async function(viewerName, messageText, buttonEl) {
            buttonEl.disabled = true;
            const originalText = buttonEl.innerHTML;
            buttonEl.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Думаю...';
            
            const streamTitle = document.getElementById('stream-title').value.trim() || "моя сегодняшняя трансляция";

            const systemPrompt = `Ты - дружелюбный, харизматичный и активный стример. Твоя задача - дать короткий, остроумный и позитивный ответ на комментарий зрителя. Ссылка на текущую тему стрима: "${streamTitle}". Ответ должен быть на русском языке. Будь лаконичным, максимум одно предложение.`;

            const userQuery = `Зритель ${viewerName} написал: "${messageText}". Сгенерируй ответ.`;
            
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
            };

            try {
                const response = await fetchWithRetry(textApiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const text = result.candidates?.[0]?.content?.parts?.[0]?.text;

                if (text) {
                    addChatMessage("Вы (Стример)", text, "#a855f7", true);
                    addSystemMessage("Ответ сгенерирован Gemini.");
                } else {
                    addSystemMessage("Ошибка: Не удалось сгенерировать ответ.");
                }
            } catch (error) {
                console.error("Gemini API Error:", error);
                addSystemMessage("Ошибка API: Не удалось связаться с Gemini.", true);
            } finally {
                buttonEl.disabled = false;
                buttonEl.innerHTML = originalText;
            }
        }

        window.generateStreamDescription = async function(buttonEl) {
            buttonEl.disabled = true;
            const originalText = buttonEl.innerHTML;
            buttonEl.innerHTML = '<i class="fas fa-spinner fa-spin"></i>';
            
            const streamTitle = document.getElementById('stream-title').value.trim();
            const descriptionEl = document.getElementById('stream-description');

            if (!streamTitle) {
                addSystemMessage("Ошибка: Введите название трансляции для генерации описания.", true);
                buttonEl.disabled = false;
                buttonEl.innerHTML = originalText;
                return;
            }

            const systemPrompt = `Ты - маркетолог стриминговой платформы. Твоя задача - создать привлекательное, короткое (максимум 150 символов) описание для стрима на основе его названия. Используй смайлики и призывы к действию. Ответ должен быть на русском языке и содержать ТОЛЬКО сгенерированное описание.`;

            const userQuery = `Название стрима: "${streamTitle}". Сгенерируй описание.`;
            
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
            };

            try {
                const response = await fetchWithRetry(textApiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const text = result.candidates?.[0]?.content?.parts?.[0]?.text;

                if (text) {
                    const finalDescription = text.trim().substring(0, 150);
                    descriptionEl.value = finalDescription;
                    addSystemMessage("Описание стрима сгенерировано Gemini!");
                } else {
                    addSystemMessage("Ошибка: Не удалось сгенерировать описание.", true);
                }
            } catch (error) {
                console.error("Gemini API Error:", error);
                addSystemMessage("Ошибка API: Не удалось связаться с Gemini.", true);
            } finally {
                buttonEl.disabled = false;
                buttonEl.innerHTML = originalText;
            }
        }

        window.handleTTSAnnouncement = function(buttonEl) {
            const input = document.getElementById('chat-input');
            const text = input.value.trim();
            if (text) {
                generateAndPlayTTS(text, buttonEl);
                input.value = "";
            } else {
                addSystemMessage("Ошибка TTS: Введите текст для озвучивания.", true);
            }
        }
        
        async function generateAndPlayTTS(text, buttonEl) {
            if (!text.trim()) { addSystemMessage("Ошибка TTS: Введите текст для озвучивания.", true); return; }
            buttonEl.disabled = true;
            const originalIcon = buttonEl.innerHTML;
            buttonEl.innerHTML = '<i class="fas fa-circle-notch fa-spin"></i>';

            try {
                const payload = {
                    contents: [{ parts: [{ text: text }] }],
                    generationConfig: { responseModalities: ["AUDIO"], speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: "Charon" } } } },
                };

                const response = await fetchWithRetry(ttsApiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) { throw new Error(`HTTP error! status: ${response.status}`); }

                const result = await response.json();
                const part = result?.candidates?.[0]?.content?.parts?.[0];
                const audioData = part?.inlineData?.data;
                const mimeType = part?.inlineData?.mimeType;

                if (audioData && mimeType && mimeType.startsWith("audio/")) {
                    const sampleRateMatch = mimeType.match(/rate=(\d+)/);
                    const sampleRate = sampleRateMatch ? parseInt(sampleRateMatch[1], 10) : 16000;
                    const pcmData = base64ToArrayBuffer(audioData);
                    const pcm16 = new Int16Array(pcmData);
                    const wavBlob = pcmToWav(pcm16, sampleRate);
                    const audioUrl = URL.createObjectURL(wavBlob);

                    const audio = new Audio(audioUrl);
                    audio.play();
                    
                    audio.onended = () => {
                        buttonEl.disabled = false;
                        buttonEl.innerHTML = originalIcon;
                        URL.revokeObjectURL(audioUrl);
                    };
                    
                    addSystemMessage(`TTS: Объявлено: "${text}"`);
                } else {
                    addSystemMessage("Ошибка TTS: Не удалось получить аудиоданные.", true);
                }

            } catch (error) {
                console.error("TTS API Error:", error);
                addSystemMessage("Ошибка API: Не удалось сгенерировать голос. Проверьте консоль.", true);
            } finally {
                buttonEl.disabled = false;
                buttonEl.innerHTML = originalIcon;
            }
        }


        // === INITIALIZATION & FIREBASE SETUP ===
        
        async function initFirebase() {
            try {
                app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);
                
                const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : undefined;

                if (initialAuthToken) {
                    await signInWithCustomToken(auth, initialAuthToken);
                } else {
                    await signInAnonymously(auth);
                }
                
                onAuthStateChanged(auth, (user) => {
                    if (user) {
                        userId = user.uid;
                        isAuthReady = true;
                        
                        document.getElementById('user-id-display').textContent = userId;
                        document.getElementById('user-initials').textContent = userId.substring(0, 2).toUpperCase();
                        
                        chatStatusText.textContent = "Firebase подключен. Вы готовы к WebRTC.";
                        
                        // Try to init media early to unlock buttons
                        initMedia();

                    } else {
                        console.error("User not authenticated.");
                        chatStatusText.textContent = "Ошибка аутентификации.";
                    }
                });

            } catch (error) {
                console.error("Firebase Initialization Error:", error);
                chatStatusText.textContent = `Ошибка Firebase: ${error.code}`;
            }
        }
        
        // Ensure no alerts are used.
        (function patchAlerts() {
            window.alert = (message) => {
                console.warn("ALERT BLOCKED:", message);
                addSystemMessage(`Системное предупреждение: ${message}`, true);
            };
        })();

        // Start initialization sequence
        window.onload = () => {
            initFirebase();
            // Expose helper functions globally for onclick attributes
            window.initMedia = initMedia;
            window.toggleCamera = toggleCamera;
            window.toggleMic = toggleMic;
        };

    </script>
</body>
</html>
