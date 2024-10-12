---
title: Web socket and fast api
date: 2024-10-12 01:01:01 +0700
categories: [web socket]
tags: [web socket fastapi]     # TAG names should always be lowercase
---

## 1. Define web socket
![Web Socket Definition](/assets/2024-10-12-web-socket-fastapi/fastapi-websockets-1.jpg)

Web Socket là protocol cho phép two-way communication giữa client (ví dụ web browser) và server thông qua single TCP connection.

Benefit of Web Socket:
1. Low latency: Messages are sent and received instantly.
2. Reduced server load: No need for constant polling.
3. Bidirectional communication: Both client and server can initiate data transfer.
4. Efficient for real-time applications: Ideal for chat apps, live updates, and notifications.

## 2. Sample code
![Web socket sample demo](/assets/2024-10-12-web-socket-fastapi/sample-demo-01.excalidraw.png)

### 2.1. Server
server.py
``` python
from fastapi import FastAPI, WebSocket
from connection_manager import SocketConnectionManager

app = FastAPI()

connection_manager = SocketConnectionManager()

@app.get("/")
async def root():
    return {"message" : "Web socket server"}

@app.websocket("/websocket")
async def websocket_endpoint(websocket: WebSocket):
    await connection_manager.connect(websocket= websocket)
    try:
        while True:
            data = await websocket.receive_text()
            await connection_manager.send_message(message= f"Server recieved {data}", websocket= websocket)
    except:
        connection_manager.disconnect(websocket= websocket)
        print("Web socket disconnected")
```

### 2.2. Socket Manager

connection_manager.py

``` python
from fastapi import WebSocket

class SocketConnectionManager():
    def __init__(self):
        self.active_connections = []

    async def  connect(self, websocket: WebSocket):
        await websocket.accept()
        self.active_connections.append(websocket)

    async def send_message(self, message: str, websocket: WebSocket):
        await websocket.send_text(message)

    async def disconnect(self, websocket: WebSocket):
        self.active_connections.remove(websocket)
```

### 2.3. Client

client.html

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Web Socket with FastAPI demo</h1>

    <form action="" onsubmit="sendMessage(event)">
        <input type="text" id="text_message" autocomplete="off">
        <button type="submit">Send</button>
    </form>

    <ol id="message_list"></ol>

    <script>
        var ws = new WebSocket(`ws://localhost:80/websocket`);
        console.log("Connected")
        ws.onmessage = function (event) {
            var messages = document.getElementById('message_list')
            var message = document.createElement('li')
            var content = document.createTextNode(event.data)
            message.appendChild(content)
            messages.appendChild(message)
        };
        console.log("Send Mesage")
        function sendMessage(event) {
            var input = document.getElementById("text_message")
            ws.send(input.value)
            input.value = ''
            event.preventDefault()
        }
    </script>
</body>
</html>
```

### 2.4. Run demo
command line

``` powershell
pip install fastapi
pip install "uvicorn[standard]"
uvicorn server:app --host 0.0.0.0 --port 80
```

## 3. References
https://medium.com/@nmjoshi/getting-started-websocket-with-fastapi-b41d244a2799
https://unfoldai.com/fastapi-and-websockets/