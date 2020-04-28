# Network Information
The Network Information API provides information about the system's connection in terms of general connection type (e.g., 'wifi', 'cellular', etc.). This can be used to select high definition content or low definition content based on the user's connection. The entire API consists of the addition of the NetworkInformation interface and a single property to the Navigator interface: Navigator.connection.

## Examples
Detect connection changes
This example watches for changes to the user's connection.

```js
var connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
var type = connection.effectiveType;

function updateConnectionStatus() {
  console.log("Connection type changed from " + type + " to " + connection.effectiveType);
  type = connection.effectiveType;
}

connection.addEventListener('change', updateConnectionStatus);
```

## Preload large resources
The connection object is useful for deciding whether to preload resources that take large amounts of bandwidth or memory. This example would be called soon after page load to check for a connection type where preloading a video may not be desirable. If a cellular connection is found, then the preloadVideo flag is set to false. For simplicity and clarity, this example only tests for one connection type. A real-world use case would likely use a switch statement or some other method to check all of the possible values of #### NetworkInformation.type. Regardless of the type value you can get an estimate of connection speed through the #### NetworkInformation.effectiveType property.
```js
let preloadVideo = true;
var connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
if (connection) {
  if (connection.effectiveType=== 'cellular') {
    preloadVideo = false;
  }
}
```

## Properties
This interface also inherits properties of its parent, EventTarget.

#### NetworkInformation.downlink | Read only
Returns the effective bandwidth estimate in megabits per second, rounded to the nearest multiple of 25 kilobits per seconds.
#### NetworkInformation.downlinkMax | Read only
Returns the maximum downlink speed, in megabits per second (Mbps), for the underlying connection technology.
#### NetworkInformation.effectiveType|  Read only
Returns the effective type of the connection meaning one of 'slow-2g', '2g', '3g', or '4g'. This value is determined using a combination of recently observed round-trip time and downlink values.
#### NetworkInformation.rtt | Read only
Returns the estimated effective round-trip time of the current connection, rounded to the nearest multiple of 25 milliseconds.
#### NetworkInformation.saveData | Read only
Returns true if the user has set a reduced data usage option on the user agent.
#### NetworkInformation.type | Read only
Returns the type of connection a device is using to communicate with the network. It will be one of the following values:
`bluetooth`
`cellular`
`ethernet`
`none`
`wifi`
`wimax`
`other`
`unknown`
## Event handlers
#### NetworkInformation.onchange
The event that's fired when connection information changes and the change is fired on this object.