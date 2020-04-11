# Request
The Request interface of the [Fetch API](./../README.md) represents a resource request.

You can create a new Request object using the Request() constructor, but you are more likely to encounter a Request object being returned as the result of another API operation, such as a service worker FetchEvent.request.

## Properties
#### Request.cache Read only
Contains the cache mode of the request (e.g., default, reload, no-cache).
#### Request.context Read only 
Contains the context of the request (e.g., audio, image, iframe, etc.)
#### Request.credentials Read only
Contains the credentials of the request (e.g., omit, same-origin, include). The default is same-origin.
#### Request.destination Read only
Returns a string from the RequestDestination enum describing the request's destination. This is a string indicating the type of content being requested.
#### Request.headers Read only
Contains the associated Headers object of the request.
#### Request.integrity Read only
Contains the subresource integrity value of the request (e.g., sha256-BpfBw7ivV8q2jLiT13fxDYAe2tJllusRSZ273h2nFSE=).
#### Request.method Read only
Contains the request's method (GET, POST, etc.)
#### Request.mode Read only
Contains the mode of the request (e.g., cors, no-cors, same-origin, navigate.)
#### Request.redirect Read only
Contains the mode for how redirects are handled. It may be one of follow, error, or manual.
#### Request.referrer Read only
Contains the referrer of the request (e.g., client).
#### Request.referrerPolicy Read only
Contains the referrer policy of the request (e.g., no-referrer).
#### Request.url Read only
Contains the URL of the request.
Request implements Body, so it also inherits the following properties:

body Read only
A simple getter used to expose a ReadableStream of the body contents.
bodyUsed Read only
Stores a Boolean that declares whether the body has been used in a response yet.

---
## Methods
#### Request.clone()
Creates a copy of the current Request object.
Request implements Body, so it also has the following methods available to it:

#### Body.arrayBuffer()
Returns a promise that resolves with an ArrayBuffer representation of the request body.
#### Body.blob()
Returns a promise that resolves with a Blob representation of the request body.
#### Body.formData()
Returns a promise that resolves with a FormData representation of the request body.
#### Body.json()
Returns a promise that resolves with a JSON representation of the request body.
#### Body.text()
Returns a promise that resolves with an USVString (text) representation of the request body.
Note: The Body functions can be run only once; subsequent calls will resolve with empty strings/ArrayBuffers.

---

## Examples

In the following snippet, we create a new request using the Request() constructor (for an image file in the same directory as the script), then return some property values of the request:

```js
const request = new Request('https://www.delca.com/favicon.ico');

const URL = request.url;
const method = request.method;
const credentials = request.credentials;
```
You could then fetch this request by passing the Request object in as a parameter to a WindowOrWorkerGlobalScope.fetch() call, for example:

```js
fetch(request)
  .then(response => response.blob())
  .then(blob => {
    image.src = URL.createObjectURL(blob);
  });
  ```