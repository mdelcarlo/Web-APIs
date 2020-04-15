# Web Workers
Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.

## Usage
A worker is an object created using a constructor (e.g. Worker()) that runs a named JavaScript file — this file contains the code that will run in the worker thread; workers run in another global context that is different from the current window. This context is represented by either a DedicatedWorkerGlobalScope object (in the case of dedicated workers - workers that are utilized by a single script), or a SharedWorkerGlobalScope (in the case of shared workers - workers that are shared between multiple scripts).

You can run whatever code you like inside the worker thread, with some exceptions. For example, you can't directly manipulate the DOM from inside a worker, or use some default methods and properties of the window object. But you can use a large number of items available under window, including WebSockets, and data storage mechanisms like IndexedDB.  See Functions and classes available to workers for more details.

Data is sent between workers and the main thread via a system of messages — both sides send their messages using the postMessage() method, and respond to messages via the onmessage event handler (the message is contained within the Message event's data property). The data is copied rather than shared.

Workers may in turn spawn new workers, as long as those workers are hosted within the same origin as the parent page.  In addition, workers may use XMLHttpRequest for network I/O, with the exception that the responseXML and channel attributes on XMLHttpRequest always return null.

In addition to dedicated workers, there are other types of worker:

- **Shared workers** are workers that can be utilized by multiple scripts running in different windows, IFrames, etc., as long as they are in the same domain as the worker. They are a little more complex than dedicated workers — scripts must communicate via an active port. See SharedWorker for more details.
- **ServiceWorkers** essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among other things, to enable the creation of effective offline experiences, intercept network requests and take appropriate action based on whether the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.
- **Chrome Workers** are a Firefox-only type of worker that you can use if you are developing add-ons and want to use workers in extensions and have access to js-ctypes in your worker. See ChromeWorker for more details. 
- **Audio Workers** provide the ability for direct scripted audio processing to be done inside a web worker context.

## Examples

#### Multiply in a dedicated web worker

The main script comunicates with the worker script through mesagges.

##### main.js script

```js
const first = document.querySelector('#number1');
const second = document.querySelector('#number2');

const result = document.querySelector('.result');

if (window.Worker) {
	const myWorker = new Worker("worker.js");

	first.onchange = function() {
	  myWorker.postMessage([first.value, second.value]);
	  console.log('Message posted to worker');
	}

	second.onchange = function() {
	  myWorker.postMessage([first.value, second.value]);
	  console.log('Message posted to worker');
	}

	myWorker.onmessage = function(e) {
		result.textContent = e.data;
		console.log('Message received from worker');
	}
} else {
	console.log('Your browser doesn\'t support web workers.')
}
```

##### worker.js script

```js
onmessage = function(e) {
  console.log('Worker: Message received from main script');
  let result = e.data[0] * e.data[1];
  if (isNaN(result)) {
    postMessage('Please write two numbers');
  } else {
    let workerResult = 'Result: ' + result;
    console.log('Worker: Posting message back to main script');
    postMessage(workerResult);
  }
}
```

#### Multiply and square in a shared web worker

##### square.js

```js
var squareNumber = document.querySelector('#number3');

var result2 = document.querySelector('.result2');

if (!!window.SharedWorker) {
  var myWorker = new SharedWorker("worker.js");

  squareNumber.onchange = function() {
    myWorker.port.postMessage([squareNumber.value, squareNumber.value]);
    console.log('Message posted to worker');
  }

  myWorker.port.onmessage = function(e) {
    result2.textContent = e.data;
    console.log('Message received from worker');
  }
}
```

##### multiply.js
```js
var first = document.querySelector('#number1');
var second = document.querySelector('#number2');

var result1 = document.querySelector('.result1');

if (!!window.SharedWorker) {
  var myWorker = new SharedWorker("worker.js");

  first.onchange = function() {
    myWorker.port.postMessage([first.value, second.value]);
    console.log('Message posted to worker');
  }

  second.onchange = function() {
    myWorker.port.postMessage([first.value, second.value]);
    console.log('Message posted to worker');
  }

  myWorker.port.onmessage = function(e) {
    result1.textContent = e.data;
    console.log('Message received from worker');
    console.log(e.lastEventId);
  }
}
```

##### worker.js

```js
onconnect = function(e) {
  var port = e.ports[0];

  port.onmessage = function(e) {
    var workerResult = 'Result: ' + (e.data[0] * e.data[1]);
    port.postMessage(workerResult);
  }

}
```