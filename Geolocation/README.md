# Geolocation API

The Geolocation API allows the user to provide their location to web applications if they so desire. For privacy reasons, the user is asked for permission to report location information.

WebExtensions that wish to use the Geolocation object must add the "geolocation" permission to their manifest. The user's operating system will prompt the user to allow location access the first time it is requested.

This feature is available only in secure contexts (HTTPS), in some or all supporting browsers.

The Geolocation API is accessed via a call to navigator.geolocation; this will cause the user's browser to ask them for permission to access their location data. If they accept, then the browser will use the best available functionality on the device to access this information (for example, GPS).

The developer can now access this location information in a couple of different ways:

Geolocation.getCurrentPosition(): Retrieves the device's current location.
Geolocation.watchPosition(): Registers a handler function that will be called automatically each time the position of the device changes, returning the updated location.
In both cases, the method call takes up to three arguments:

A mandatory success callback: If the location retrieval is successful, the callback executes with a GeolocationPosition object as its only parameter, providing access to the location data.
An optional error callback: If the location retrieval is unsuccessful, the callback executes with a GeolocationPositionError object as its only parameter, providing access information on what went wrong.
An optional PositionOptions object, which provides options for retrieval of the position data.

---

## Interfaces
#### Geolocation
The main class of this API — contains methods to retrieve the user's current position, watch for changes in their position, and clear a previously-set watch.
#### GeolocationPosition
Represents the position of a user. A GeolocationPosition instance is returned by a successful call to one of the methods contained inside Geolocation, inside a success callback, and contains a timestamp plus a GeolocationCoordinates object instance.
#### GeolocationCoordinates
Represents the coordinates of a user's position; a GeolocationCoordinates instance contains latitude, longitude, and other important related information.
#### GeolocationPositionError
A GeolocationPositionError is returned by an unsuccessful call to one of the methods contained inside Geolocation, inside an error callback, and contains an error code and message.
#### Navigator.geolocation
The entry point into the API. Returns a Geolocation object instance, from which all other functionality can be accessed.

---

## Dictionaries
#### PositionOptions
Represents an object containing options to pass in as a parameter of Geolocation.getCurrentPosition() and Geolocation.watchPosition().

---

## Examples

#### Get your current position and create a map with its cords

[<img width="539" alt="Captura de Pantalla 2020-04-10 a la(s) 08 32 29" src="https://user-images.githubusercontent.com/20034230/78938184-e2e60600-7b05-11ea-8c16-831d80d7d6ea.png">](https://jsfiddle.net/njr9zayb/1/)