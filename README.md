![Screenshot 2023-06-11 143255](https://github.com/pranotidhangar/Real-Chat.github.io/assets/131478879/10ae0187-9dad-4cff-8e62-75a330078f6a)
![Screenshot 2023-06-11 142930](https://github.com/pranotidhangar/Real-Chat.github.io/assets/131478879/f003ac22-0350-4544-98a2-37b83111cdfc)
![Screenshot 2023-04-23 194943](https://github.com/pranotidhangar/Real-Chat.github.io/assets/131478879/1152a8ea-1232-41e0-876b-9f67867ceb0f)
# Real-Chat## Real-Time Chat Application Documentation

### Introduction
This documentation provides a guide for developing a real-time chat application using Node.js and Socket.IO. Socket.IO is a JavaScript library that enables real-time bidirectional communication between the server and the clients. This application will allow multiple users to join chat rooms and exchange messages instantly.

### Prerequisites
To follow this documentation, make sure you have the following prerequisites installed:

- Node.js (https://nodejs.org)
- NPM (Node Package Manager, comes with Node.js installation)

### Setup
1. Create a new directory for your project.
2. Open a terminal or command prompt and navigate to the project directory.
3. Initialize a new Node.js project by running the following command:
   ```
   npm init -y
   ```
4. Install the required dependencies (Node.js and Socket.IO) by running the following command:
   ```
   npm install express socket.io
   ```

### Server Setup
1. Create a new file called `server.js` in the project directory.
2. Open `server.js` and require the necessary modules:
   ```javascript
   const express = require('express');
   const app = express();
   const http = require('http').createServer(app);
   const io = require('socket.io')(http);
   ```
3. Create an HTTP server using Express and Socket.IO:
   ```javascript
   const port = 3000; // Change the port number if required

   http.listen(port, () => {
     console.log(`Server is running on http://localhost:${port}`);
   });
   ```
4. Implement Socket.IO event handlers for handling client connections and disconnections:
   ```javascript
   io.on('connection', (socket) => {
     console.log('A user connected');

     socket.on('disconnect', () => {
       console.log('A user disconnected');
     });
   });
   ```

### Client Setup
1. Create a new HTML file called `index.html` in the project directory.
2. Open `index.html` and add the necessary HTML structure:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
     <title>Real-Time Chat Application</title>
   </head>
   <body>
     <h1>Real-Time Chat Application</h1>
     <div id="messages"></div>
     <form id="message-form">
       <input id="message-input" type="text" placeholder="Type your message" />
       <button type="submit">Send</button>
     </form>

     <script src="/socket.io/socket.io.js"></script>
     <script src="client.js"></script>
   </body>
   </html>
   ```
3. Create a new JavaScript file called `client.js` in the project directory.
4. Open `client.js` and add the following code to establish a connection with the server:
   ```javascript
   const socket = io();

   socket.on('connect', () => {
     console.log('Connected to the server');
   });
   ```
5. Implement code to handle the message form submission and emit a "chat message" event:
   ```javascript
   const messageForm = document.getElementById('message-form');
   const messageInput = document.getElementById('message-input');

   messageForm.addEventListener('submit', (e) => {
     e.preventDefault();
     const message = messageInput.value;
     if (message.trim() !== '') {
       socket.emit('chat message', message);
       messageInput.value = '';
     }
   });
   ```
6. Add code to handle incoming chat messages from the server and display them in the UI:
   ```javascript
   const messagesContainer = document.getElementById('messages');

   socket.on('chat message', (message) => {
    

 const messageElement = document.createElement('div');
     messageElement.textContent = message;
     messagesContainer.appendChild(messageElement);
   });
   ```

### Broadcasting Chat Messages
To enable broadcasting of chat messages to all connected clients, modify the server-side event handler as follows:

```javascript
io.on('connection', (socket) => {
  console.log('A user connected');

  socket.on('disconnect', () => {
    console.log('A user disconnected');
  });

  socket.on('chat message', (message) => {
    io.emit('chat message', message);
  });
});
```

### Running the Application
1. Start the server by running the following command in the project directory:
   ```
   node server.js
   ```
2. Open a web browser and navigate to `http://localhost:3000` (or the appropriate port number).
3. Open multiple browser tabs or windows and join the chat room.
4. Start sending messages, and they should appear instantly on all connected clients.

### Conclusion
Congratulations! You have successfully developed a real-time chat application using Node.js and Socket.IO. This documentation provided a basic implementation, and you can further enhance the application by adding features like user authentication, private messaging, chat room management, and more. Socket.IO offers a wide range of functionalities, so feel free to explore the Socket.IO documentation (https://socket.io/docs/) to learn more.**
