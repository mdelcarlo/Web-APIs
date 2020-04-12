# MediaQueryList

A MediaQueryList object stores information on a media query applied to a document, with support for both immediate and event-driven matching against the state of the document. You can create a MediaQueryList by calling matchMedia() on the window object. The resulting object handles sending notifications to listeners when the media query state changes (i.e. when the media query test starts or stops evaluating to true).

## Properties
The new version of the MediaQueryList interface inherits properties from its parent interface, EventTarget.

#### MediaQueryList.matches | Read only
A Boolean that returns true if the document currently matches the media query list, or false if not.
#### MediaQueryList.media | Read only
A DOMString representing a serialized media query
Methods
The new version of the MediaQueryList interface inherits methods from its parent interface, EventTarget.

#### MediaQueryList.addListener()
Adds a listener to the MediaQueryListener that will run a custom callback function in response to the media query status changing. This is basically an alias for EventTarget.addEventListener(), for backwards compatibility purposes.
#### MediaQueryList.removeListener()
Removes a listener from the MediaQueryListener. This is basically an alias for EventTarget.removeEventListener(), for backwards compatibility purposes.
## Events
The following events are delivered to MediaQueryList objects:

#### change
Sent to the MediaQueryList when the result of running the media query against the document changes. For example, if the media query is (min-width: 400px), the change event is fired any time the width of the document's viewport changes to be less than 400 pixels or greater than that.
Also available using the onchange event handler property.
## Examples
Create a MediaQueryList and then sets up a listener to detect when the media query status changes, running a custom function when it does to change the appearence of the page.

```js
var para = document.querySelector('p');

var mql = window.matchMedia('(max-width: 600px)');

function screenTest(e) {
  if (e.matches) {
    /* the viewport is 600 pixels wide or less */
    para.textContent = 'This is a narrow screen — less than 600px wide.';
    document.body.style.backgroundColor = 'red';
  } else {
    /* the viewport is more than than 600 pixels wide */
    para.textContent = 'This is a wide screen — more than 600px wide.';
    document.body.style.backgroundColor = 'blue';
  }
}

mql.addListener(screenTest);
```