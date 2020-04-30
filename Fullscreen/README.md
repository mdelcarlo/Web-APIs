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