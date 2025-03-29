Code Documentation - socketIoController.js
The purpose of this code file is to handle socket.io connections and emit messages to connected clients.
Import
The code imports the connectDB function from the `../config/connectDB` file. This function establishes a connection to the database.
Function: `sendMessageAdmin(io)`
This function is responsible for handling the socket.io connections and emitting messages to connected clients.
Parameters
•	io: The socket.io instance passed as a parameter to the function.
Usage
To use this function, pass the socket.io instance as an argument when calling `sendMessageAdmin(io)`.

    
Function Logic
```js
const sendMessageAdmin = (io) => {
    io.on('connection', (socket) => {
        socket.on('data-server', (msg) => {
            io.emit('data-server', msg);
        });
        socket.on('data-server_2', (msg) => {
            io.emit('data-server_2', msg);
        });
        socket.on('data-server-5', (msg) => {
            io.emit('data-server-5', msg);
        });
        socket.on('data-server-3', (msg) => {
            io.emit('data-server-3', msg);
        });
        // socket.on("disconnect", () => {
        // console.log('a user disconnect ' + socket.id);
        // });
    });
} 
    
```
The provided code defines a function named sendMessageAdmin that takes io as a parameter. 

1.	Inside this function, it sets up event listeners for different socket events using the io.on method. When a specific event is received, the function emits the same event with the associated message using io.emit.
2.	Overall, this code is designed to relay incoming messages received on specific socket events to all connected clients using Socket.IO.
    	

