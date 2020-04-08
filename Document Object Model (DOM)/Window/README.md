# Window

The Window interface represents a window containing a DOM document; the document property points to the DOM document loaded in that window. A window for a given document can be obtained using the document.defaultView property.

A global variable, window, representing the window in which the script is running, is exposed to JavaScript code.

The Window interface is home to a variety of functions, namespaces, objects, and constructors which are not necessarily directly associated with the concept of a user interface window. However, the Window interface is a suitable place to include these items that need to be globally available. Many of these are documented in the JavaScript Reference and the DOM Reference.

In a tabbed browser, each tab is represented by its own Window object; the global window seen by JavaScript code running within a given tab always represents the tab in which the code is running. That said, even in a tabbed browser, some properties and methods still apply to the overall window that contains the tab, such as resizeTo() and innerHeight. Generally, anything that can't reasonably pertain to a tab pertains to the window instead.

---

## Properties
This interface inherits properties from the EventTarget interface and implements properties from the #### WindowOrWorkerGlobalScope and WindowEventHandlers mixins.

e listed in a separate section below.

#### Window.closed  Read only
This property indicates whether the current window is closed or not.
#### Window.console Read only
Returns a reference to the console object which provides access to the browser's debugging console.
#### Window.controllers  Read only
Returns the XUL controller objects for the current chrome window.
#### Window.customElements Read only
returns a reference to the CustomElementRegistry object, which can be used to register new custom elements and get information about previously registered custom elements.
#### Window.crypto Read only
Returns the browser crypto object.
#### Window.devicePixelRatio  Read only
Returns the ratio between physical pixels and device independent pixels in the current display.
#### Window.dialogArguments Read only
Gets the arguments passed to the window (if it's a dialog box) at the time window.showModalDialog() was called. This is an nsIArray.
#### Window.document Read only
Returns a reference to the document that the window contains.
#### Window.DOMMatrix Read only 
Returns a reference to a DOMMatrix object, which represents 4x4 matrices, suitable for 2D and 3D operations.
#### Window.DOMMatrixReadOnly Read only 
Returns a reference to a DOMMatrixReadOnly object, which represents 4x4 matrices, suitable for 2D and 3D operations.
#### Window.DOMPoint Read only 
Returns a reference to a DOMPoint object, which represents a 2D or 3D point in a coordinate system.
#### Window.DOMPointReadOnly Read only 
Returns a reference to a DOMPointReadOnly object, which represents a 2D or 3D point in a coordinate system.
#### Window.DOMQuad Read only 
Returns a reference to a DOMQuad object, which provides represents a quadrilaterial object, that is one having four corners and four sides.
#### Window.DOMRect Read only 
Returns a reference to a DOMRect object, which represents a rectangle.
#### Window.DOMRectReadOnly Read only 
Returns a reference to a DOMRectReadOnly object, which represents a rectangle.
#### Window.event Read only
Returns the current event, which is the event currently being handled by the JavaScript code's context, or undefined if no event is currently being handled. The Event object passed directly to event handlers should be used instead whenever possible.
#### Window.frameElement Read only
Returns the element in which the window is embedded, or null if the window is not embedded.
#### Window.frames Read only
Returns an array of the subframes in the current window.
#### Window.fullScreen
This property indicates whether the window is displayed in full screen or not.
#### Window.history Read only
Returns a reference to the history object.
#### Window.innerHeight Read only
Gets the height of the content area of the browser window including, if rendered, the horizontal scrollbar.
#### Window.innerWidth Read only
Gets the width of the content area of the browser window including, if rendered, the vertical scrollbar.
#### Window.isSecureContext  Read only
Indicates whether a context is capable of using features that require secure contexts.
#### Window.length Read only
Returns the number of frames in the window. See also window.frames.
#### Window.location
Gets/sets the location, or current URL, of the window object.
#### Window.locationbar Read only
Returns the locationbar object, whose visibility can be toggled in the window.
#### Window.localStorage Read only
Returns a reference to the local storage object used to store data that may only be accessed by the origin that created it.
#### Window.menubar Read only
Returns the menubar object, whose visibility can be toggled in the window.
#### Window.messageManager
Returns the message manager object for this window.
#### Window.mozInnerScreenX Read only 
Returns the horizontal (X) coordinate of the top-left corner of the window's viewport, in screen coordinates. This value is reported in CSS pixels. See mozScreenPixelsPerCSSPixel in nsIDOMWindowUtils for a conversion factor to adapt to screen pixels if needed.
#### Window.mozInnerScreenY Read only 
Returns the vertical (Y) coordinate of the top-left corner of the window's viewport, in screen coordinates. This value is reported in CSS pixels. See mozScreenPixelsPerCSSPixel for a conversion factor to adapt to screen pixels if needed.
#### Window.name
Gets/sets the name of the window.
#### Window.navigator Read only
Returns a reference to the navigator object.
#### Window.opener
Returns a reference to the window that opened this current window.
#### Window.orientation   Read only
Returns the orientation in degrees (in 90 degree increments) of the viewport relative to the device's natural orientation.
#### Window.outerHeight Read only
Gets the height of the outside of the browser window.
#### Window.outerWidth Read only
Gets the width of the outside of the browser window.
#### Window.pageXOffset Read only
An alias for window.scrollX.
#### Window.pageYOffset Read only
An alias for window.scrollY
#### Window.parent Read only
Returns a reference to the parent of the current window or subframe.
#### Window.performance Read only
Returns a Performance object, which includes the timing and navigation attributes, each of which is an object providing performance-related data. See also Using Navigation Timing for additional information and examples.
#### Window.personalbar Read only
Returns the personalbar object, whose visibility can be toggled in the window.
#### Window.screen Read only
Returns a reference to the screen object associated with the window.
#### Window.screenX and #### Window.screenLeft Read only
Both properties return the horizontal distance from the left border of the user's browser viewport to the left side of the screen.
#### Window.screenY and #### Window.screenTop Read only
Both properties return the vertical distance from the top border of the user's browser viewport to the top side of the screen.
#### Window.scrollbars Read only
Returns the scrollbars object, whose visibility can be toggled in the window.
#### Window.scrollMaxX  Read only
The maximum offset that the window can be scrolled to horizontally, that is the document width minus the viewport width.
#### Window.scrollMaxY  Read only
The maximum offset that the window can be scrolled to vertically (i.e., the document height minus the viewport height).
#### Window.scrollX Read only
Returns the number of pixels that the document has already been scrolled horizontally.
#### Window.scrollY Read only
Returns the number of pixels that the document has already been scrolled vertically.
#### Window.self Read only
Returns an object reference to the window object itself.
#### Window.sessionStorage
Returns a reference to the session storage object used to store data that may only be accessed by the origin that created it.
#### Window.sidebar  Read only
Returns a reference to the window object of the sidebar.
#### Window.speechSynthesis Read only
Returns a SpeechSynthesis object, which is the entry point into using Web Speech API speech synthesis functionality.
#### Window.status
Gets/sets the text in the statusbar at the bottom of the browser.
#### Window.statusbar Read only
Returns the statusbar object, whose visibility can be toggled in the window.
#### Window.toolbar Read only
Returns the toolbar object, whose visibility can be toggled in the window.
#### Window.top Read only
Returns a reference to the topmost window in the window hierarchy. This property is read only.
#### Window.visualViewport Read only
Returns a VisualViewport object which represents the visual viewport for a given window.
#### Window.window Read only
Returns a reference to the current window.
window[0], window[1], etc.
Returns a reference to the window object in the frames. See Window.frames for more details.
Properties implemented from elsewhere
#### WindowOrWorkerGlobalScope.caches Read only
Returns the CacheStorage object associated with the current context. This object enables functionality such as storing assets for offline use, and generating custom responses to requests.
#### WindowOrWorkerGlobalScope.indexedDB Read only
Provides a mechanism for applications to asynchronously access capabilities of indexed databases; returns an IDBFactory object.
#### WindowOrWorkerGlobalScope.isSecureContext Read only
Returns a boolean indicating whether the current context is secure (true) or not (false).
#### WindowOrWorkerGlobalScope.origin Read only
Returns the global object's origin, serialized as a string. (This does not yet appear to be implemented in any browser.)

---

## Methods
This interface inherits methods from the EventTarget interface and implements methods from #### #### WindowOrWorkerGlobalScope and EventTarget.

#### Window.alertt()
Displays an alert dialog.
#### Window.blur()
Sets focus away from the window.
#### Window.cancelAnimationFrame() 
Enables you to cancel a callback previously scheduled with #### Window.requestAnimationFrame.
#### Window.cancelIdleCallback() 
Enables you to cancel a callback previously scheduled with #### Window.requestIdleCallback.
#### Window.clearImmediate()
Cancels the repeated execution set using setImmediate.
#### Window.close()
Closes the current window.
#### Window.confirm()
Displays a dialog with a message that the user needs to respond to.
#### Window.dump() 
Writes a message to the console.
#### Window.find()
Searches for a given string in a window.
#### Window.focus()
Sets focus on the current window.
#### Window.getComputedStyle()
Gets computed style for the specified element. Computed style indicates the computed values of all CSS properties of the element.
#### Window.getDefaultComputedStyle() 
Gets default computed style for the specified element, ignoring author stylesheets.
#### Window.getSelection()
Returns the selection object representing the selected item(s).
#### Window.matchMedia()
Returns a MediaQueryList object representing the specified media query string.
#### Window.maximize()
FIXME: NeedsContents
#### Window.minimize() (top-level XUL windows only)
Minimizes the window.
#### Window.moveBy()
Moves the current window by a specified amount.
#### Window.moveTo()
Moves the window to the specified coordinates.
#### Window.open()
Opens a new window.
#### Window.postMessage()
Provides a secure means for one window to send a string of data to another window, which need not be within the same domain as the first.
#### Window.print()
Opens the Print Dialog to print the current document.
#### Window.prompt()
Returns the text entered by the user in a prompt dialog.
#### Window.requestAnimationFrame()
Tells the browser that an animation is in progress, requesting that the browser schedule a repaint of the window for the next animation frame.
#### Window.requestIdleCallback() 
Enables the scheduling of tasks during a browser's idle periods.
#### Window.resizeBy()
Resizes the current window by a certain amount.
#### Window.resizeTo()
Dynamically resizes window.
#### Window.scroll()
Scrolls the window to a particular place in the document.
#### Window.scrollBy()
Scrolls the document in the window by the given amount.
#### Window.scrollByLines() 
Scrolls the document by the given number of lines.
#### Window.scrollByPages() 
Scrolls the current document by the specified number of pages.
#### Window.scrollTo()
Scrolls to a particular set of coordinates in the document.
#### Window.setCursor()  (top-level XUL windows only)
Changes the cursor for the current window
#### Window.setImmediate()
Executes a function after the browser has finished other heavy tasks
#### Window.setResizable() 
Toggles a user's ability to resize a window.
#### Window.sizeToContent() 
Sizes the window according to its content.
#### Window.stop()
This method stops window loading.
#### Window.updateCommands() 
Updates the state of commands of the current chrome window (UI).
Methods implemented from elsewhere
#### EventTarget.addEventListener()
Register an event handler to a specific event type on the window.
#### EventTarget.dispatchEvent()
Used to trigger an event.
#### WindowOrWorkerGlobalScope.atob()
Decodes a string of data which has been encoded using base-64 encoding.
#### WindowOrWorkerGlobalScope.btoa()
Creates a base-64 encoded ASCII string from a string of binary data.
#### WindowOrWorkerGlobalScope.clearInterval()
Cancels the repeated execution set using #### WindowOrWorkerGlobalScope.setInterval().
#### WindowOrWorkerGlobalScope.clearTimeout()
Cancels the delayed execution set using #### WindowOrWorkerGlobalScope.setTimeout().
#### WindowOrWorkerGlobalScope.createImageBitmap()
Accepts a variety of different image sources, and returns a Promise which resolves to an ImageBitmap. Optionally the source is cropped to the rectangle of pixels originating at (sx, sy) with width sw, and height sh.
#### WindowOrWorkerGlobalScope.fetch()
Starts the process of fetching a resource from the network.
#### EventTarget.removeEventListener
Removes an event listener from the window.
#### WindowOrWorkerGlobalScope.setInterval()
Schedules a function to execute every time a given number of milliseconds elapses.
#### WindowOrWorkerGlobalScope.setTimeout()
Schedules a function to execute in a given amount of time.

## Examples

#### Change the URL of a window from a popup
The following example demonstrates how a popup window can change the URL of the window that opened it. Before attempting to change the URL, it checks that the current window has an opener using the window.opener property and that the opener isn't closed:

```js
// Check that an opener exists and is not closed
if (window.opener && !window.opener.closed) {
  window.opener.location.href = 'http://www.mozilla.org';
}
```

#### Correcting resolution in a ```<canvas>```

 ```<canvas>``` can appear too blurry on retina screens.  Use window.devicePixelRatio to determine how much extra pixel density should be added to allow for a sharper image.

```html
 <canvas id="canvas"></canvas>
```
 ```js
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');

// Set display size (css pixels).
var size = 200;
canvas.style.width = size + "px";
canvas.style.height = size + "px";

// Set actual size in memory (scaled to account for extra pixel density).
var scale = window.devicePixelRatio; // Change to 1 on retina screens to see blurry canvas.
canvas.width = size * scale;
canvas.height = size * scale;

// Normalize coordinate system to use css pixels.
ctx.scale(scale, scale);

ctx.fillStyle = "#bada55";
ctx.fillRect(10, 10, 300, 300);
ctx.fillStyle = "#ffffff";
ctx.font = '18px Arial';
ctx.textAlign = 'center';
ctx.textBaseline = 'middle';

var x = size / 2;
var y = size / 2;

var textString = "I love MDN";
ctx.fillText(textString, x, y);
 ```

 #### Moving forward and backward
To move backward through history:

```js
window.history.back();

// or

window.history.go(-1)
```
This acts exactly as if the user clicked on the Back button in their browser toolbar.

Similarly, you can move forward (as if the user clicked the Forward button), like this:

```js
window.history.forward()

// or

window.history.go(1)
```

#### Navigate to a new page
Whenever a new value is assigned to the location object, a document will be loaded using the URL as if location.assign() had been called with the modified URL. Note that security settings, like CORS, may prevent this to effectively happen.

```js
location.assign("https://github.com/mdelcarlo"); // or
location = "https://github.com/mdelcarlo";
```
#### Force reloading the current page from the server
```js
location.reload(true);
```

#### Send a string of data to the server by modifying the search property
```js
function sendData (data) {
  location.search = data;
}
```
The current URL with "?Some%20data" appended is sent to the server (if no action is taken by the server, the current document is reloaded with the modified search string).

#### Using local storage

The following snippet accesses the current domain's local Storage object and adds a data item to it using Storage.setItem().
```js
localStorage.setItem('myCat', 'Tom');
```
The syntax for reading the localStorage item is as follows:
```js
var cat = localStorage.getItem('myCat');
```
The syntax for removing the localStorage item is as follows:

```js
localStorage.removeItem('myCat');
```
The syntax for removing all the localStorage items is as follows:

```js
localStorage.clear();
```

 #### Browser detect and return a string
 ```js

// The order matters here, and this may report false positives for unlisted browsers.
function getBrowser(){
    let sBrowser;
    const sUsrAg = navigator.userAgent;

    if (sUsrAg.indexOf("Firefox") > -1) {
        sBrowser = "Mozilla Firefox";
    // "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:61.0) Gecko/20100101 Firefox/61.0"
    } else if (sUsrAg.indexOf("SamsungBrowser") > -1) {
        sBrowser = "Samsung Internet";
    // "Mozilla/5.0 (Linux; Android 9; SAMSUNG SM-G955F Build/PPR1.180610.011) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/9.4 Chrome/67.0.3396.87 Mobile Safari/537.36
    } else if (sUsrAg.indexOf("Opera") > -1 || sUsrAg.indexOf("OPR") > -1) {
        sBrowser = "Opera";
    // "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.102 Safari/537.36 OPR/57.0.3098.106"
    } else if (sUsrAg.indexOf("Trident") > -1) {
        sBrowser = "Microsoft Internet Explorer";
    // "Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; .NET4.0C; .NET4.0E; Zoom 3.6.0; wbx 1.0.0; rv:11.0) like Gecko"
    } else if (sUsrAg.indexOf("Edge") > -1) {
        sBrowser = "Microsoft Edge";
    // "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299"
    } else if (sUsrAg.indexOf("Chrome") > -1) {
        sBrowser = "Google Chrome or Chromium";
    // "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Ubuntu Chromium/66.0.3359.181 Chrome/66.0.3359.181 Safari/537.36"
    } else if (sUsrAg.indexOf("Safari") > -1) {
        sBrowser = "Apple Safari";
    // "Mozilla/5.0 (iPhone; CPU iPhone OS 11_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/11.0 Mobile/15E148 Safari/604.1 980x1306"
    } else {
        sBrowser = "unknown";
    }
}

alert("You are using: " + getBrowser());
```

#### Show a confirm dialog to ask to trigger a task

```js
if (window.confirm("Do you really want to leave?")) { 
  window.open("exit.html", "Thanks for Visiting!");
}
```

#### Scroll smoothly to top
```js
window.scrollTo({
  top: 100,
  left: 100,
  behavior: 'smooth'
});
```

#### Log a message when the page is fully loaded:

```js
window.addEventListener('load', (event) => {
  console.log('page is fully loaded');
});
```