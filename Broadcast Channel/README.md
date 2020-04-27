# Broadcast Channel
The Broadcast Channel API allows basic communication between browsing contexts (that is, windows, tabs, frames, or iframes) and workers on the same origin.

<img width="692" alt="Captura de Pantalla 2020-04-27 a la(s) 22 46 11" src="https://user-images.githubusercontent.com/20034230/80363910-0c11df00-88d9-11ea-891d-a06c30b554e2.png">


By creating a BroadcastChannel object, you can receive any messages that are posted to it. You don't have to maintain a reference to the frames or workers you wish to communicate with: they can “subscribe” to a particular channel by constructing their own BroadcastChannel with the same name, and have bi-directional communication between all of them.


## Broadcast Channel interface
Creating or joining a channel
A client joins a broadcast channel by creating a BroadcastChannel object. Its constructor takes one single parameter: the name of the channel. If it is the first to connect to that broadcast channel name, the underlying channel is created.

```js
const bc = new BroadcastChannel('test_channel');
```
Sending a message
It is enough to call the postMessage() method on the created BroadcastChannel object, which takes any object as an argument. An example string message:

```js
bc.postMessage('This is a test message.');
```
Any kind of object can be sent, not just a DOMString.

The API doesn't associate any semantics to messages, so it is up to the code to know what kind of messages to expect and what to do with them.

### Receiving a message
When a message is posted, a message event is dispatched to each BroadcastChannel object connected to this channel. A function can be run for this event with the onmessage event handler:

```js
bc.onmessage = function (ev) { console.log(ev); }
```
### Disconnecting a channel
To leave a channel, call the close() method on the object. This disconnects the object from the underlying channel, allowing garbage collection.

```js
bc.close();
```
