# Fullscreen
The Fullscreen API adds methods to present a specific Element (and its descendants) in full-screen mode, and to exit full-screen mode once it is no longer needed. This makes it possible to present desired content—such as an online game—using the user's entire screen, removing all browser user interface elements and other applications from the screen until full-screen mode is shut off.

## Methods
The Fullscreen API adds methods to the Document and Element interfaces to allow turning off and on full-screen mode.


### Methods on the Document interface
#### Document.exitFullscreen()
Requests that the user agent switch from full-screen mode back to windowed mode. Returns a Promise which is resolved once full-screen mode has been completely shut off.
Methods on the Element interface
#### Element.requestFullscreen()
Asks the user agent to place the specified element (and, by extension, its descendants) into full-screen mode, removing all of the browser's UI elements as well as all other applications from the screen. Returns a Promise which is resolved once full-screen mode has been activated.

## Properties
The Document interface provides properties that can be used to determine if full-screen mode is supported and available, and if full-screen mode is currently active, which element is using the screen.

#### DocumentOrShadowRoot.fullscreenElement
The fullscreenElement property tells you the Element that's currently being displayed in full-screen mode on the DOM (or shadow DOM). If this is null, the document is not in full-screen mode.
document.fullscreenEnabled
The fullscreenEnabled property tells you whether or not it is possible to engage full-screen mode. This is false if full-screen mode is not available for any reason (such as the "fullscreen" feature not being allowed, or full-screen mode not being supported).
Event handlers
The Fullscreen API defines two events which can be used to detect when full-screen mode is turned on and off, as well as when errors occur during the process of changing between full-screen and windowed modes. Event handlers for these events are available on the Document and Element interfaces.


### Event handlers on documents
#### Document.onfullscreenchange
An event handler for the fullscreenchange event that's sent to a Document when that document is placed into full-screen mode, or when that document exits full-screen mode. This handler is called only when the entire document is presented in full-screen mode.
#### Document.onfullscreenerror
An event handler for the fullscreenerror event that gets sent to a Document when an error occurs while trying to enable or disable full-screen mode for the entire document.

### Event handlers on elements
#### Element.onfullscreenchange
An event handler which is called when the fullscreenchange event is sent to the element, indicating that the element has been placed into, or removed from, full-screen mode.
#### Element.onfullscreenerror
An event handler for the fullscreenerror event when sent to an element which has encountered an error while transitioning into or out of full-screen mode.

## Example
In this example, a video is presented in a web page. Pressing the Return or Enter key lets the user toggle between windowed and full-screen presentation of the video.



#### Watching for the Enter key
When the page is loaded, this code is run to set up an event listener to watch for the Enter key.
```js
document.addEventListener("keypress", function(e) {
  if (e.keyCode === 13) {
    toggleFullScreen();
  }
}, false);
```
#### Toggling full-screen mode
This code is called by the event handler above when the user hits the Enter key.
```js
function toggleFullScreen() {
  if (!document.fullscreenElement) {
      document.documentElement.requestFullscreen();
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen(); 
    }
  }
}
```
This starts by looking at the value of the document's fullscreenElement attribute. In a real-world deployment, at this time, you'll want to check for prefixed versions of this (mozFullScreenElement, msFullscreenElement, or webkitFullscreenElement, for example). If the value is null, the document is currently in windowed mode, so we need to switch to full-screen mode; otherwise, it's the element that's currently in full-screen mode. Switching to full-screen mode is done by calling Element.requestFullscreen() on the ``<video>`` element.

If full-screen mode is already active (fullscreenElement is not null), we call exitFullscreen() on the document to shut off full-screen mode.