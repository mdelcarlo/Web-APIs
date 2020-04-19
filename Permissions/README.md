# Permissions
The Permissions API provides a consistent programmatic way to query the status of API permissions attributed to the current context. For example, the Permissions API can be used to determine if permission to access a particular API has been granted or denied.

## Concepts and usage
Historically different APIs handle their own permissions inconsistently — for example the Notifications API allows for explicit checking of permission status and requesting permission, whereas the Geolocation API doesn't (which causes problems if the user denied the initial permission request). The Permissions API provides the tools to allow developers to implement a better user experience as far as permissions are concerned.

The permissions property has been made available on the Navigator object, both in the standard browsing context and the worker context (WorkerNavigator — so permission checks are available inside workers), and returns a Permissions object that provides access to the Permissions API functionality.

Once you have this object you can then perform permission-related tasks, for example querying a permission using the Permissions.query() method to return a promise that resolves with the PermissionStatus for a specific API.

Not all APIs' permission statuses can be queried using the Permissions API. Notable APIs that are Permissions-aware include:

Clipboard API
Notifications API
Push API
Web MIDI API
More APIs will gain Permissions API support over time.

## Examples
#### Querying permission state
In our example, the Permissions functionality is handled by one function — handlePermission(). This starts off by querying the permission status using Permissions.query(). Depending on the value of the state property of the  PermissionStatus object returned when the promise resolves, it reacts differently:

##### "granted"
The "Enable Geolocation" button is hidden, as it isn't needed if Geolocation is already active.
##### "prompt"
The "Enable Geolocation" button is hidden, as it isn't needed if the user will be prompted to grant permission for Geolocation. The Geolocation.getCurrentPosition() function is then run, which prompts the user for permission; it runs the revealPosition() function if permission is granted (which shows the map), or the positionDenied() function if permission is denied (which makes the "Enable Geolocation" button appear).
##### "denied"
The "Enable Geolocation" button is revealed (this code needs to be here too, in case the permission state is already set to denied for this origin when the page is first loaded).
```js
function handlePermission() {
  navigator.permissions.query({name:'geolocation'}).then(function(result) {
    if (result.state == 'granted') {
      report(result.state);
      geoBtn.style.display = 'none';
    } else if (result.state == 'prompt') {
      report(result.state);
      geoBtn.style.display = 'none';
      navigator.geolocation.getCurrentPosition(revealPosition,positionDenied,geoSettings);
    } else if (result.state == 'denied') {
      report(result.state);
      geoBtn.style.display = 'inline';
    }
    result.onchange = function() {
      report(result.state);
    }
  });
}

function report(state) {
  console.log('Permission ' + state);
}

handlePermission();
```

#### Revoking permissions
 This works in exactly the same way as the Permissions.query() method, except that it causes an existing permission to be reverted back to its default state when the promise successfully resolves (which is usually prompt). See the following code in our demo:
```js
var revokeBtn = document.querySelector('.revoke');

  ...

revokeBtn.onclick = function() {
  revokePermission();
}

  ...

function revokePermission() {
  navigator.permissions.revoke({name:'geolocation'}).then(function(result) {
    report(result.state);
  });
}
```

#### Responding to permission state changes
You'll notice that there is an onchange event handler in the code above, attached to the PermissionStatus object — this allows us to respond to any changes in the permission status for the API we are interested in. At the moment we are just reporting the change in state.