<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>P2P Video & Chat Room</title>
    <!-- Include PeerJS library for easy WebRTC handling -->
    <script src="https://unpkg.com/peerjs@1.5.2/dist/peerjs.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; background: #0f172a; color: #f8fafc; margin: 0; padding: 20px; display: flex; flex-direction: column; align-items: center; }
        h2 { margin-bottom: 10px; }
        .room-info { background: #1e293b; padding: 10px 20px; border-radius: 8px; margin-bottom: 20px; display: flex; gap: 10px; align-items: center; }
        input, button { padding: 8px 12px; border-radius: 4px; border: 1px solid #475569; background: #334155; color: white; }
        button { background: #3b82f6; cursor: pointer; border: none; font-weight: bold; }
        button:hover { background: #2563eb; }
        .main-container { display: flex; gap: 20px; width: 100%; max-width: 1000px; flex-wrap: wrap; justify-content: center; }
        .video-box { position: relative; background: #1e293b; border-radius: 8px; overflow: hidden; width: 450px; height: 340px; display: flex; align-items: center; justify-content: center; }
        video { width: 100%; height: 100%; object-fit: cover; }
        .label { position: absolute; bottom: 10px; left: 10px; background: rgba(0,0,0,0.6); padding: 4px 8px; border-radius: 4px; font-size: 12px; }
        .chat-box { background: #1e293b; border-radius: 8px; width: 100%; max-width: 1000px; padding: 15px; margin-top: 20px; display: flex; flex-direction: column; height: 150px; }
        #chat-messages { flex-grow: 1; overflow-y: auto; background: #0f172a; padding: 10px; border-radius: 4px; margin-bottom: 10px; font-size: 14px; }
        .chat-input-area { display: flex; gap: 10px; }
        .chat-input-area input { flex-grow: 1; }
    </style>
</head>
<body>

    <h2>Secure P2P Video & Chat</h2>
    
    <div class="room-info">
        <span>Your Share Link:</span>
        <input type="text" id="share-link" readonly style="width: 300px;">
        <button onclick="copyLink()">Copy Link</button>
    </div>

    <div class="main-container">
        <div class="video-box">
            <video id="local-video" autoplay muted playsinline></video>
            <div class="label">You</div>
        </div>
        <div class="video-box">
            <video id="remote-video" autoplay playsinline></video>
            <div class="label">Partner</div>
        </div>
    </div>

    <div class="chat-box">
        <div id="chat-messages"></div>
        <div class="chat-input-area">
            <input type="text" id="message-input" placeholder="Type a message..." onkeypress="handleKeyPress(event)">
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>

    <script>
        const urlParams = new URLSearchParams(window.location.search);
        const roomId = urlParams.get('room');

        let peer;
        let myStream;
        let conn;
        let currentCall;

        const localVideo = document.getElementById('local-video');
        const remoteVideo = document.getElementById('remote-video');
        const chatMessages = document.getElementById('chat-messages');
        const messageInput = document.getElementById('message-input');
        const shareLinkInput = document.getElementById('share-link');

        // 1. Get user media (Camera & Mic)
        navigator.mediaDevices.getUserMedia({ video: true, audio: true })
            .then(stream => {
                myStream = stream;
                localVideo.srcObject = stream;
                initPeer();
            })
            .catch(err => {
                alert('Could not access camera/microphone. Check permissions.');
                console.error(err);
            });

        function initPeer() {
            // If there is a room ID in URL, connect as peer. Otherwise, create a new ID.
            peer = new Peer(); 

            peer.on('open', (id) => {
                let currentId = roomId ? roomId : id;
                if (!roomId) {
                    // Update URL with the generated room/peer ID without reloading
                    const newUrl = `${window.location.origin}${window.location.pathname}?room=${id}`;
                    window.history.pushState({path: newUrl}, '', newUrl);
                }
                shareLinkInput.value = window.location.href;

                if (roomId) {
                    // Automatically connect to the host if opening a share link
                    connectToPeer(roomId);
                }
            });

            // Handle incoming calls (When someone opens your link and calls you)
            peer.on('call', (call) => {
                currentCall = call;
                call.answer(myStream); // Answer with our camera stream
                call.on('stream', (remoteStream) => {
                    remoteVideo.srcObject = remoteStream;
                });
            });

            // Handle incoming data connections (Text Chat)
            peer.on('connection', (connection) => {
                conn = connection;
                setupDataConnection();
            });
        }

        function connectToPeer(targetId) {
            // Initiate data connection for chat
            conn = peer.connect(targetId);
            setupDataConnection();

            // Initiate media call for video/audio
            const call = peer.call(targetId, myStream);
            currentCall = call;
            call.on('stream', (remoteStream) => {
                remoteVideo.srcObject = remoteStream;
            });
        }

        function setupDataConnection() {
            conn.on('data', (data) => {
                appendMessage('Partner', data);
            });
        }

        function sendMessage() {
            const msg = messageInput.value.trim();
            if (!msg || !conn) return;
            conn.send(msg);
            appendMessage('You', msg);
            messageInput.value = '';
        }

        function handleKeyPress(e) {
            if (e.key === 'Enter') sendMessage();
        }

        function appendMessage(sender, text) {
            const div = document.createElement('div');
            div.innerHTML = `<strong>${sender}:</strong> ${text}`;
            chatMessages.appendChild(div);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function copyLink() {
            shareLinkInput.select();
            navigator.clipboard.writeText(shareLinkInput.value);
            alert('Share link copied to clipboard!');
        }
    </script>
</body>
</html>
