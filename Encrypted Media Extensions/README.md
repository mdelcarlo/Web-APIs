# Encrypted Media Extensions
The Encrypted Media Extensions API provides interfaces for controlling the playback of content which is subject to a digital restrictions management scheme.

## Interfaces
### MediaKeyMessageEvent
Contains the content and related data when the content decryption module (CDM) generates a message for the session.
### MediaKeys
Represents a set of keys that an associated HTMLMediaElement can use for decryption of media data during playback.
### MediaKeySession
Represents a context for message exchange with a content decryption module (CDM).
### MediaKeyStatusMap
Is a read-only map of media key statuses by key IDs. 
### MediaKeySystemAccess
Provides access to a Key System for decryption and/or a content protection provider.
### MediaKeySystemConfiguration
Provides configuration information about the media key system.

## Examples

#### Getting a key from a license server
In typical commercial use, content will be encrypted and encoded using a packaging service or tool. Once the encrypted media is made available online, a web client can obtain a key (contained within a license) from a license server and use the key to enable decryption and playback of the content.

The following code (adapted from the spec examples) shows how an application can select an appropriate key system and obtain a key from a license server.
```js
var video = document.querySelector('video');

var config = [{initDataTypes: ['webm'],
  videoCapabilities: [{contentType: 'video/webm; codecs="vp9"'}]}];

if (!video.mediaKeys) {
  navigator.requestMediaKeySystemAccess('org.w3.clearkey',
      config).then(
    function(keySystemAccess) {
      var promise = keySystemAccess.createMediaKeys();
      promise.catch(
        console.error.bind(console, 'Unable to create MediaKeys')
      );
      promise.then(
        function(createdMediaKeys) {
          return video.setMediaKeys(createdMediaKeys);
        }
      ).catch(
        console.error.bind(console, 'Unable to set MediaKeys')
      );
      promise.then(
        function(createdMediaKeys) {
          var initData = new Uint8Array([...]);
          var keySession = createdMediaKeys.createSession();
          keySession.addEventListener('message', handleMessage,
              false);
          return keySession.generateRequest('webm', initData);
        }
      ).catch(
        console.error.bind(console,
          'Unable to create or initialize key session')
      );
    }
  );
}

function handleMessage(event) {
  var keySession = event.target;
  var license = new Uint8Array([...]);
  keySession.update(license).catch(
    console.error.bind(console, 'update() failed')
  );
}
```
