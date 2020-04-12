# Screen
The Screen interface represents a screen, usually the one on which the current window is being rendered, and is obtained using ```window.screen```.

>Note that browsers determine which screen to report as current by detecting which screen has the center of the browser window.

## Properties
#### Screen.availTop 
Specifies the y-coordinate of the first pixel that is not allocated to permanent or semipermanent user interface features.
#### Screen.availLeft 
Returns the first available pixel available from the left side of the screen.
#### Screen.availHeight
Specifies the height of the screen, in pixels, minus permanent or semipermanent user interface features displayed by the operating system, such as the Taskbar on Windows.
#### Screen.availWidth
Returns the amount of horizontal space in pixels available to the window.
#### Screen.colorDepth
Returns the color depth of the screen.
#### Screen.height
Returns the height of the screen in pixels.
#### Screen.left 
Returns the distance in pixels from the left side of the main screen to the left side of the current screen.
#### Screen.orientation
Returns the ScreenOrientation instance associated with this screen.
#### Screen.pixelDepth
Gets the bit depth of the screen.
#### Screen.top 
Returns the distance in pixels from the top side of the current screen.
#### Screen.width
Returns the width of the screen.
#### Screen.mozEnabled  
Boolean. Setting to false will turn off the device's screen.
#### Screen.mozBrightness  
Controls the brightness of a device's screen. A double between 0 and 1.0 is expected.
## Events handler
#### Screen.onorientationchange 
A handler for the orientationchange event.
Methods
#### Screen.lockOrientation
Lock the screen orientation (only works in fullscreen or for installed apps)
#### Screen.unlockOrientation
Unlock the screen orientation (only works in fullscreen or for installed apps)
Methods inherited from EventTarget:

#### EventTarget.addEventListener()
Registers an event handler of a specific event type on the EventTarget.
#### EventTarget.removeEventListener()
Removes an event listener from the EventTarget.
#### EventTarget.dispatchEvent()
Dispatches an event to this EventTarget.

## Examples

#### Change volor version depending on resolution
```js
if (screen.pixelDepth < 8) {
  // use low-color version of page
} else { 
  // use regular, colorful page
}
```

#### Detect orientation

```js
var orientation = (screen.orientation || {}).type || screen.mozOrientation || screen.msOrientation;

if (orientation === "landscape-primary") {
  console.log("That looks good.");
} else if (orientation === "landscape-secondary") {
  console.log("Mmmh... the screen is upside down!");
} else if (orientation === "portrait-secondary" || orientation === "portrait-primary") {
  console.log("Mmmh... you should rotate your device to landscape");
} else if (orientation === undefined) {
  console.log("The orientation API isn't supported in this browser :("); 
}
```