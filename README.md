# Socket Presentation

### What is a WebSocket?

> WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection.

_What does this mean?_

WebSockets allow for two way, simultaneous communication between the client and the server

* Think of a telephone, where both parties can talk at the same time without interruption

WebSockets are different than traditional ways of communicating between the server and the browser because the WebSocket specification defines an API for establishing "socket" connections between the two. In other words:

> There is an persistent connection between the client and the server and both parties can start sending data at any time.

In the past workarounds have been used in lieu of this formal protocol. One such workaround was "polling", where a connection is made to the server like AJAX does but that connection is kept alive for a certain amount of time and needs to be refreshed periodically.


### Why is this dope?

This is dope because it makes it easy to create apps with event based communication in real-time. From Stack Overflow user `Moka`:

> The main advantage of WebSockets server-side, is that it is not an HTTP request (after handshake), but a proper message based communication protocol. This enables you to achieve huge performance and architecture advantages. For example, in node.js, you can share the same memory for different socket connections, so they can each access shared variables. Therefore, you don't need to use a database as an exchange point in the middle (like with AJAX or Long Polling with a language like PHP). You can store data in RAM, or even republish between sockets straight away.

### Socket.io

It's a wrapper for WebSockets, with a fallback for polling when WebSockets aren't supported.

### How to get started

You can clone [this repo](https://github.com/skiprox/websockets-getting-started).

This includes the server side `index.js`, and the client side `public/js/app.js` (with `app.built.js` being the browserify'd version). Here's an overview of what is in each:

* `index.js`
	* Server side code. Runs `express`, uses Node's `http` to create a server, and uses `socket.io` to listen and send events.
	* Listens and emits events very similarly to `EventEmitter`.
	* `io` used to listen to and emit events to/from all nodes, and `socket` for one specific socket.
	
Example:

```
io.on('connection', function(socket) {
	userCount++;
	io.emit('add user', {
		users: userCount
	});
	socket.on('click', function(data) {
		io.emit('click registered', {
			x: data.xPos,
			y: data.yPos
		});
	});
	socket.on('disconnect', function(data) {
		userCount--;
		io.emit('drop user', {
			users: userCount
		});
	})
});
```

* `public/js/app.js`
	* Client side code. Includes `socket.io` on the page, creates a new `socket` by initiating `io`, `var socket = io();`
	* Because this is one client that is directly communicating with the server, you just need to emit and listen for events with `socket`.
	
Example:

```
var socket = io();
document.body.addEventListener('click', function(e) {
	socket.emit('click', {
		xPos: e.pageX,
		yPos: e.pageY
	});
});
socket.on('click registered', function(data) {
	console.log('we have clicks', data.x, data.y);
});
```

### Next Steps

Check out [this repo](https://github.com/skiprox/shared-canvas) for an example of drawing, and [this repo](https://github.com/skiprox/palmetto-boyz) for an example of a chat app.

Live examples:

* [Drawing](http://little-slugs.herokuapp.com/)
* [Chat](http://palmetto-boyz.herokuapp.com/)


### Sources 

[HTML5 Rocks](https://www.html5rocks.com/en/tutorials/websockets/basics/)

[This Stack Overflow QA](http://stackoverflow.com/questions/10028770/in-what-situations-would-ajax-long-short-polling-be-preferred-over-html5-websock)