<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="chat-container">
        <h2>Hi! How can I help you?</h2>
        <div id="chatbox"></div>
        <input type="text" id="userInput" placeholder="Type your question...">
        <button onclick="sendMessage()">Send</button>
        
        <input type="file" id="fileUpload">
        <button onclick="uploadFile()">Upload</button>
    </div>
    
    <script src="script.js"></script>
</body>
</html>

/* styles.css */
.chat-container {
    width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    text-align: center;
}

#chatbox {
    height: 200px;
    border: 1px solid #ccc;
    overflow-y: scroll;
    margin-bottom: 10px;
}

/* script.js */
function sendMessage() {
    let userInput = document.getElementById("userInput").value;
    let chatbox = document.getElementById("chatbox");
    
    let userMessage = document.createElement("p");
    userMessage.innerText = "User: " + userInput;
    chatbox.appendChild(userMessage);
    
    fetch('/chat', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({ message: userInput })
    })
    .then(response => response.json())
    .then(data => {
        let botMessage = document.createElement("p");
        botMessage.innerText = "Chatbot: " + data.reply;
        chatbox.appendChild(botMessage);
    });
}

function uploadFile() {
    let file = document.getElementById("fileUpload").files[0];
    let formData = new FormData();
    formData.append("file", file);
    
    fetch('/upload', {
        method: 'POST',
        body: formData
    })
    .then(response => response.text())
    .then(data => alert("File uploaded successfully!"));
}

/* server.py */
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/chat', methods=['POST'])
def chat():
    user_message = request.json['message']
    bot_reply = "Here is a response to: " + user_message  # Placeholder response
    return jsonify({"reply": bot_reply})

@app.route('/upload', methods=['POST'])
def upload():
    file = request.files['file']
    file.save("uploads/" + file.filename)
    return "File uploaded successfully"

if __name__ == '__main__':
    app.run(debug=True)
