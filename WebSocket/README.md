# WebSocket
The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.

## Interfaces
### WebSocket
The primary interface for connecting to a WebSocket server and then sending and receiving data on the connection.
### CloseEvent
The event sent by the WebSocket object when the connection closes.
### MessageEvent
The event sent by the WebSocket object when a message is received from the server.

## Examples

#### Creating a WebSocket object
In order to communicate using the WebSocket protocol, you need to create a WebSocket object; this will automatically attempt to open the connection to the server.

The WebSocket constructor accepts one required and one optional parameter:
```js
webSocket = new WebSocket(url, protocols);
```
``url``
The URL to which to connect; this should be the URL to which the WebSocket server will respond. This should use the URL scheme wss://, although some software may allow you to use the insecure ws:// for local connections.
``protocols`` Optional
Either a single protocol string or an array of protocol strings. These strings are used to indicate sub-protocols, so that a single server can implement multiple WebSocket sub-protocols (for example, you might want one server to be able to handle different types of interactions depending on the specified protocol). If you don't specify a protocol string, an empty string is assumed.

- If you want to open a connection and are flexible about the protocols you support, you can specify an array of protocols:
```js
var exampleSocket = new WebSocket("wss://www.example.com/socketserver", ["protocolOne", "protocolTwo])
```

#### Sending data to the server
Once you've opened your connection, you can begin transmitting data to the server. To do this, simply call the WebSocket object's send() method for each message you want to send:
```js
exampleSocket.send("Here's some text that the server is urgently awaiting!");
``` 
You can send data as a string, Blob, or ArrayBuffer.

As establishing a connection is asynchronous and prone to failure there is no guarantee that calling the send() method immediately after creating a WebSocket object will be successful. We can at least be sure that attempting to send data only takes place once a connection is established by defining an onopen event handler to do the work:
```js
exampleSocket.onopen = function (event) {
  exampleSocket.send("Here's some text that the server is urgently awaiting!"); 
};
```

##### Using JSON to transmit objects
One handy thing you can do is use JSON to send reasonably complex data to the server. For example, a chat program can interact with a server using a protocol implemented using packets of JSON-encapsulated data:
```js
// Send text to all users through the server
function sendText() {
  // Construct a msg object containing the data the server needs to process the message from the chat client.
  var msg = {
    type: "message",
    text: document.getElementById("text").value,
    id:   clientID,
    date: Date.now()
  };

  // Send the msg object as a JSON-formatted string.
  exampleSocket.send(JSON.stringify(msg));
  
  // Blank the text input element, ready to receive the next line of text from the user.
  document.getElementById("text").value = "";
}
```
#### Receiving messages from the server
WebSockets is an event-driven API; when messages are received, a message event is sent to the WebSocket object. To handle it, add an event listener for the message event, or use the onmessage event handler. To begin listening for incoming data, you can do something like this:
```js
exampleSocket.onmessage = function (event) {
  console.log(event.data);
}
```
Receiving and interpreting JSON objects
Let's consider the chat client application first alluded to in Using JSON to transmit objects. There are assorted types of data packets the client might receive, such as:

- Login handshake
- Message text
- User list updates

The code that interprets these incoming messages might look like this:
```js
exampleSocket.onmessage = function(event) {
  var f = document.getElementById("chatbox").contentDocument;
  var text = "";
  var msg = JSON.parse(event.data);
  var time = new Date(msg.date);
  var timeStr = time.toLocaleTimeString();
  
  switch(msg.type) {
    case "id":
      clientID = msg.id;
      setUsername();
      break;
    case "username":
      text = "<b>User <em>" + msg.name + "</em> signed in at " + timeStr + "</b><br>";
      break;
    case "message":
      text = "(" + timeStr + ") <b>" + msg.name + "</b>: " + msg.text + "<br>";
      break;
    case "rejectusername":
      text = "<b>Your username has been set to <em>" + msg.name + "</em> because the name you chose is in use.</b><br>"
      break;
    case "userlist":
      var ul = "";
      for (i=0; i < msg.users.length; i++) {
        ul += msg.users[i] + "<br>";
      }
      document.getElementById("userlistbox").innerHTML = ul;
      break;
  }
  
  if (text.length) {
    f.write(text);
    document.getElementById("chatbox").contentWindow.scrollByPages(1);
  }
};
```
Here we use JSON.parse() to convert the JSON object back into the original object, then examine and act upon its contents.

**Text data format**
Text received over a WebSocket connection is in UTF-8 format.

Closing the connection
When you've finished using the WebSocket connection, call the WebSocket method close():
```js
exampleSocket.close();
```
It may be helpful to examine the socket's bufferedAmount attribute before attempting to close the connection to determine if any data has yet to be transmitted on the network. If this value isn't 0, there's pending data still, so you may wish to wait before closing the connection.
