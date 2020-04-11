# Fetch
The **Fetch API** provides an interface for fetching resources (including across the network). It will seem familiar to anyone who has used XMLHttpRequest, but the new API provides a more powerful and flexible feature set.

---

## Concepts and usage
Fetch provides a generic definition of Request and Response objects (and other things involved with network requests). This will allow them to be used wherever they are needed in the future, whether it’s for service workers, Cache API, and other similar things that handle or modify requests and responses, or any kind of use case that might require you to generate your own responses programmatically(that is, the use of computer program or personal programming instructions).

It also provides a definition for related concepts such as CORS and the HTTP origin header semantics, supplanting their separate definitions elsewhere.

For making a [request](./Request/README.md) and fetching a resource, use the WindowOrWorkerGlobalScope.fetch() method. It is implemented in multiple interfaces, specifically Window and WorkerGlobalScope. This makes it available in pretty much any context you might want to fetch resources in.

The fetch() method takes one mandatory argument, the path to the resource you want to fetch. It returns a Promise that resolves to the Response to that [request](./Request/README.md), whether it is successful or not. You can also optionally pass in an init options object as the second argument (see Request).

Once a Response is retrieved, there are a number of methods available to define what the body content is and how it should be handled (see Body).

You can create a [request](./Request/README.md) and [response](./Response/README.md) directly using the [Request()](./Request/README.md) and [Response()](./Response/README.md) constructors, but it's uncommon to do this directly. Instead, these are more likely to be created as results of other API actions (for example, FetchEvent.respondWith() from service workers).

## Methods

#### WindowOrWorkerGlobalScope.fetch()

The fetch() method of the WindowOrWorkerGlobalScope mixin starts the process of fetching a resource from the network, returning a promise which is fulfilled once the response is available. The promise resolves to the Response object representing the response to your request. The promise does not reject on HTTP errors — it only rejects on network errors. You must use then handlers to check for HTTP errors.

WindowOrWorkerGlobalScope is implemented by both Window and WorkerGlobalScope, which means that the fetch() method is available in pretty much any context in which you might want to fetch resources.

## Syntax
```js
const fetchResponsePromise = fetch(resource [, init])
```
### Parameters
#### resource
This defines the resource that you wish to fetch. This can either be:
A USVString containing the direct URL of the resource you want to fetch. Some browsers accept the blob: and data: schemes.
A Request object.
#### init Optional
An object containing any custom settings that you want to apply to the request. The possible options are:

<details><summary>method</summary>

The request method, e.g., GET, POST.

</details>
<details><summary>headers</summary>
Any <a href="./Headers/README.md">headers</a> you want to add to your request, contained within a Headers object or an object literal with ByteString values. Note that some names are forbidden.
</details>
<details><summary>body</summary>
Any body that you want to add to your request: this can be a Blob, BufferSource, FormData, URLSearchParams, USVString, or ReadableStream object. Note that a request using the GET or HEAD method cannot have a body.
</details>
<details><summary>mode</summary>
The mode you want to use for the request, e.g., cors, no-cors, or same-origin.
credentials
The request credentials you want to use for the request: omit, same-origin, or include. To automatically send cookies for the current domain, this option must be provided. Starting with Chrome 50, this property also takes a FederatedCredential instance or a PasswordCredential instance.
</details>
<details><summary>cache</summary>
The cache mode you want to use for the request.
</details>
<details><summary>redirect</summary>
The redirect mode to use: follow (automatically follow redirects), error (abort with an error if a redirect occurs), or manual (handle redirects manually). In Chrome the default is follow (before Chrome 47 it defaulted to manual).
</details>
<details><summary>referrer</summary>
A USVString specifying the referrer of the request. This can be a same-origin URL, about:client, or an empty string.
</details>
<details><summary>referrerPolicy</summary>
Specifies the referrer policy to use for the request. May be one of no-referrer, no-referrer-when-downgrade, same-origin, origin, strict-origin, origin-when-cross-origin, strict-origin-when-cross-origin, or unsafe-url.
</details>
<details><summary>integrity</summary>
Contains the subresource integrity value of the request (e.g., sha256-BpfBw7ivV8q2jLiT13fxDYAe2tJllusRSZ273h2nFSE=).
</details>
<details><summary>keepalive</summary>
The keepalive option can be used to allow the request to outlive the page. Fetch with the keepalive flag is a replacement for the Navigator.sendBeacon() API. 
</details>
<details><summary>signal</summary>
An AbortSignal object instance; allows you to communicate with a fetch request and abort it if desired via an AbortController.
</details>

## Examples
#### Request an image and add it to the page

```js
const myImage = document.querySelector('img');

let myRequest = new Request('flowers.jpg');

fetch(myRequest)
.then(function(response) {
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return response.blob();
})
.then(function(response) {
  let objectURL = URL.createObjectURL(response);
  myImage.src = objectURL;
});
```

#### Fetch an image with init

```js
const myImage = document.querySelector('img');

let myHeaders = new Headers();
myHeaders.append('Content-Type', 'image/jpeg');

const myInit = {
  method: 'GET',
  headers: myHeaders,
  mode: 'cors',
  cache: 'default'
};

let myRequest = new Request('flowers.jpg');

fetch(myRequest, myInit).then(function(response) {
  // ... 
});
```

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