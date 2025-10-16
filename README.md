HELLO CHAT
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Worldwide Chat</title>
<style>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
}
.chat-container {
    width: 400px;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
    display: flex;
    flex-direction: column;
    overflow: hidden;
}
header {
    background-color: #0077cc;
    color: white;
    text-align: center;
    padding: 15px;
    font-size: 18px;
}
.chat-box {
    flex: 1;
    padding: 10px;
    overflow-y: auto;
    border-bottom: 1px solid #ccc;
    display: flex;
    flex-direction: column;
}
.chat-box div {
    margin: 5px 0;
    padding: 8px 12px;
    border-radius: 20px;
    max-width: 80%;
}
.user-msg { background-color: #0077cc; color: white; align-self: flex-end; }
.bot-msg { background-color: #e5e5e5; color: black; align-self: flex-start; }
input {
    border: none; padding: 10px; flex: 1; border-top: 1px solid #ccc; outline: none;
}
button {
    border: none; padding: 10px 15px; background-color: #0077cc; color: white; cursor: pointer;
}
button:hover { background-color: #005fa3; }
.chat-container input, .chat-container button { width: 50%; }
</style>
</head>
<body>
<div class="chat-container">
    <header id="chatHeader">Worldwide Chat</header>
    <div class="chat-box" id="chatBox"></div>
    <input type="text" id="chatInput" placeholder="Type a message..." />
    <button onclick="sendMessage()">Send</button>
</div>

<!-- Firebase JS SDK -->
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

<script>
// --- Firebase config (apna Firebase config paste karo) ---
const firebaseConfig = {
  apiKey: "API_KEY",
  authDomain: "PROJECT_ID.firebaseapp.com",
  databaseURL: "https://PROJECT_ID-default-rtdb.firebaseio.com",
  projectId: "PROJECT_ID",
  storageBucket: "PROJECT_ID.appspot.com",
  messagingSenderId: "SENDER_ID",
  appId: "APP_ID"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.database();
const chatBox = document.getElementById('chatBox');
const chatInput = document.getElementById('chatInput');

const userName = "Khan"; // Change your name

// Listen for new messages
db.ref("messages").on("child_added", (snapshot) => {
    const data = snapshot.val();
    const msgDiv = document.createElement('div');
    msgDiv.className = data.user === userName ? 'user-msg' : 'bot-msg';
    msgDiv.textContent = `${data.user}: ${data.text}`;
    chatBox.appendChild(msgDiv);
    chatBox.scrollTop = chatBox.scrollHeight;
});

// Send message
function sendMessage() {
    const text = chatInput.value.trim();
    if(text === "") return;
    db.ref("messages").push({ user: userName, text: text });
    chatInput.value = "";
}
</script>
</body>
</html>
