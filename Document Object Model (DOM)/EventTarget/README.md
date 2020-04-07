# EventTarget
<b>EventTarget</b> is a DOM interface implemented by objects that can receive events and may have listeners for them.

<a href="./../Element/README.md" target="_self">Element</a>, <a href="./../Document/README.md" target="_self">Document</a>, and <a href="./../Window/README.md" target="_self">Window</a> are the most common event targets, but other objects can be event targets, too. For example XMLHttpRequest, AudioNode, AudioContext, and others.

The root of the DOM hierarchy is EventTarget, that is inherited by Node, and other DOM nodes inherit from it.

<img width="522" alt="Captura de Pantalla 2020-04-07 a la(s) 09 03 33" src="https://user-images.githubusercontent.com/20034230/78605171-2eeb3d80-78af-11ea-9501-ec4853e392c4.png">

The DOM interfaces are:

**Node** – serves as a base for DOM nodes. It provides the core tree functionality: parentNode, nextSibling, childNodes and so on (they are getters). There are concrete node classes that inherit from it, namely: Text for text nodes, Element for element nodes and more exotic ones like Comment for comment nodes.

**Element** – is a base interface for DOM elements. It provides element-level navigation like nextElementSibling, children and searching methods like getElementsByTagName, querySelector. A browser supports not only HTML, but also XML and SVG. The Element class serves as a base for more specific classes: SVGElement, XMLElement and HTMLElement.

**HTMLElement** – is finally the basic interface for all HTML elements. It is inherited by various HTML elements:

- **HTMLInputElement** – the interface for ```<input>``` elements,
- **HTMLBodyElement** – the interface for ```<body>``` elements,
- **HTMLAnchorElement** – the interface for ```<a>``` elements

Let’s consider the DOM object for an ```<input>``` element. It belongs to HTMLInputElement class. It gets properties and methods as a superposition of:

- **HTMLInputElement** – provides input-specific properties.
- **HTMLElement** – provides common HTML element methods (and getters/setters).
- **Element** – provides generic element methods.
- **Node** – provides common DOM node properties.
- **EventTarget** – gives the support for events (to be covered).

## Constructor
EventTarget()
Creates a new EventTarget object instance.

## Methods

### EventTarget.addEventListener()
Sets up a function that will be called whenever the specified event is delivered to the target. Common targets are <a href="./../Element/README.md" target="_self">Element</a>, <a href="./../Document/README.md" target="_self">Document</a>, and <a href="./../Window/README.md" target="_self">Window</a>, but the target may be any object that supports events (such as XMLHttpRequest).

```js
target.addEventListener(type, listener [, options]);
target.addEventListener(type, listener [, useCapture]);
target.addEventListener(type, listener [, useCapture, wantsUntrusted  ]); // Gecko/Mozilla only
```

#### Parameters
##### type
A case-sensitive string representing the event type to listen for.
##### listener
The object which receives a notification (an object that implements the Event interface) when an event of the specified type occurs.
##### options | Optional
An options object specifies characteristics about the event listener. The available options are:

##### useCapture | Optional
A Boolean indicating whether events of this type will be dispatched to the registered listener before being dispatched to any EventTarget beneath it in the DOM tree. Events that are bubbling upward through the tree will not trigger a listener designated to use capture. Event bubbling and capturing are two ways of propagating events which occur in an element that is nested within another element, when both elements have registered a handle for that event. The event propagation mode determines the order in which elements receive the event. See DOM Level 3 Events and JavaScript Event order for a detailed explanation. If not specified, useCapture defaults to false.
##### wantsUntrusted 
A Firefox (Gecko)-specific parameter. If true, the listener receives synthetic events dispatched by web content (the default is false for browser chrome and true for regular web pages). This parameter is useful for code found in add-ons, as well as the browser itself.

#### Return value
undefined

### EventTarget.removeEventListener()
Rmoves from the EventTarget an event listener previously registered with EventTarget.addEventListener().
```js
target.removeEventListener(type, listener[, options]);
target.removeEventListener(type, listener[, useCapture]);
```
#### Parameters
##### type
A string which specifies the type of event for which to remove an event listener.
##### listener
The EventListener function of the event handler to remove from the event target.
##### options | Optional
An options object that specifies characteristics about the event listener. The available options are:
capture: A Boolean that indicates that events of this type will be dispatched to the registered listener before being dispatched to any EventTarget beneath it in the DOM tree.
 mozSystemGroup: Available only in code running in XBL or in Firefox' chrome, it is a Boolean defining if the listener is added to the system group.
##### useCapture | Optional
Specifies whether the EventListener to be removed is registered as a capturing listener or not. If this parameter is absent, a default value of false is assumed.

#### Return value
undefined.

### EventTarget.dispatchEvent()
Dispatches an event at the specified EventTarget (synchronously), invoking the affected EventListeners in the appropriate order.

```js 
cancelled = !target.dispatchEvent(event)
```
#### Parameter
##### event
is the Event object to be dispatched.
##### target
is used to initialize the Event.target and determine which event listeners to invoke.
#### Return Value
The return value is false if event is cancelable and at least one of the event handlers which handled this event called Event.preventDefault(). Otherwise it returns true.

## Example
We are going to create our own event target (Dog) that extends EventTarget interface.

```js
class Dog extends EventTarget {
  constructor(mySecretBarks) {
    super();
    this._secretBarks = mySecretBarks;
  }

  get secretBarks() {
    return this._secretBarks;
  }
};

let myDog = new Dog(1);
let value = myDog.secretBarks;
console.log(value); // == 1

// assign a 'bark' event listener to myDog that changes _secretBarks from barkCount event param.
const myDogBarklistener = myDog.addEventListener("bark", function(e) {
  this._secretBarks = e.detail;
});


// create a 'bark' CustomEvent with an associated value
let barkEvent = new CustomEvent("bark", {
  detail: 11
});

// dispatch a barkEvent on myDog
myDog.dispatchEvent(barkEvent);
let newValue = myDog.secretBarks;
console.log(newValue); // == 11

// remove the bark listener function from myDog EventTarget
myDog.removeEventListener(myDogBarklistener);

```
You can run the code <a href="https://jsfiddle.net/h17ysrub/4/">here</a>.

 You can create your own EventTarget (e.g. Dog) and make that target listen to an Event (e.g. bark) you assign with addEventListener.
 
 You can dispatch an event to the EventTarget (in this case: myDog) with dispatchEvent.

 After you acomplished the needed tasks, you remove the event listener (e.g. bark) with removeEventListener (A common practice to avoid memory leak)
 
