# Response
TThe Response interface of the [Fetch API](./../README.md) represents the response to a request.

You can create a new Response object using the Response.Response() constructor, but you are more likely to encounter a Response object being returned as the result of another API operation—for example, a service worker Fetchevent.respondWith, or a simple GlobalFetch.fetch().


Properties
#### Response.headers Read only
The Headers object associated with the response.
#### Response.ok Read only
A boolean indicating whether the response was successful (status in the range 200–299) or not.
#### Response.redirected Read only
Indicates whether or not the response is the result of a redirect (that is, its URL list has more than one entry).
#### Response.status Read only
The status code of the response. (This will be 200 for a success).
#### Response.statusText Read only
The status message corresponding to the status code. (e.g., OK for 200).
#### Response.trailers
A Promise resolving to a Headers object, associated with the response with #### Response.headers for values of the HTTP Trailer header.
#### Response.type Read only
The type of the response (e.g., basic, cors).
#### Response.url Read only
The URL of the response.
#### Response.useFinalURL
A boolean indicating whether this is the final URL of the response.
Body Interface Methods
Response implements Body, so it also has the following properties available to it:

#### Body.body Read only
A simple getter exposing a ReadableStream of the body contents.
#### Body.bodyUsed Read only
Stores a Boolean that declares whether the body has been used in a response yet.

---
## Methods
#### Response.clone()
Creates a clone of a Response object.
#### Response.error()
Returns a new Response object associated with a network error.
#### Response.redirect()
Creates a new response with a different URL.

### Body Interface Methods
Response implements Body, so it also has the following methods available to it:

#### Body.arrayBuffer()
Takes a Response stream and reads it to completion. It returns a promise that resolves with an ArrayBuffer.
#### Body.blob()
Takes a Response stream and reads it to completion. It returns a promise that resolves with a Blob.
#### Body.formData()
Takes a Response stream and reads it to completion. It returns a promise that resolves with a FormData object.
#### Body.json()
Takes a Response stream and reads it to completion. It returns a promise that resolves with the result of parsing the body text as JSON.
#### Body.text()
Takes a Response stream and reads it to completion. It returns a promise that resolves with a USVString (text).

---
## Examples
In our basic fetch example (run example live) we use a simple fetch() call to grab an image and display it in an <img> element. The fetch() call returns a promise, which resolves to the Response object associated with the resource fetch operation.

You'll notice that since we are requesting an image, we need to run #### Body.blob (Response implements Body) to give the response its correct MIME type.

```js
const image = document.querySelector('.my-image');
fetch('flowers.jpg').then(function(response) {
  return response.blob();
}).then(function(blob) {
  const objectURL = URL.createObjectURL(blob);
  image.src = objectURL;
});
```