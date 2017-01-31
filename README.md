# Socket Presentation

### What is a WebSocket?

> WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection.

_What does this mean?_

WebSockets allow for 2 way, simultaneous communication

* Think of a telephone, where both parties can talk at the same time without interruption

WebSockets are different than traditional HTTP because the WebSocket specification defines an API for establishing "socket" connections between the web browser and a server. In other words:

> There is an persistent connection between the client and the server and both parties can start sending data at any time.

### Why is this dope?

This is dope because it makes it easy to create apps with event based communication in real-time.

### Socket.io

It's a wrapper for WebSockets, with a fallback for polling when WebSockets aren't supported.


### Sources 

[HTML5 Rocks](https://www.html5rocks.com/en/tutorials/websockets/basics/)