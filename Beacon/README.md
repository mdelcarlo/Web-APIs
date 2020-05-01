# Beacon
The Beacon interface is used to schedule an asynchronous and non-blocking request to a web server. Beacon requests use the HTTP POST method and requests typically do not require a response. Requests are guaranteed to be initiated before a page is unloaded and they are run to completion, without requiring a blocking request (for example XMLHttpRequest).

## Why use Beacon?
The Beacon interface addresses the needs of analytics and diagnostics code that typically attempts to send data to a web server before unloading the document. Sending the data any sooner may result in a missed opportunity to gather data. However, ensuring that the data is sent during the unloading of a document is something that has traditionally been difficult for developers.

User agents will typically ignore asynchronous XMLHttpRequests made in an unload handler. To solve this problem, analytics and diagnostics code will typically make a synchronous XMLHttpRequest in an unload or beforeunload handler to submit the data. The synchronous XMLHttpRequest forces the browser to delay unloading the document, and makes the next navigation appear to be slower. There is nothing the next page can do to avoid this perception of poor page load performance.

There are other techniques used to ensure that data is submitted. One such technique is to delay the unload to submit data by creating an Image element and setting its src attribute within the unload handler. As most user agents will delay the unload to complete the pending image load, data can be submitted during the unload. Another technique is to create a no-op loop for several seconds within the unload handler to delay the unload and submit data to a server.

Not only do these techniques represent poor coding patterns, some of them are unreliable and result in the perception of poor page load performance for the next navigation. The Beacon API provides a standard way to address these issues.

## Examples
#### Send a request on network
```js
window.onbeforeunload = function() {
  json_array=[{a: 'very good'}]
	var delca = JSON.stringify(json_array);
  navigator.sendBeacon("http://sandbox.amung.us/beacon/", delca);
}
```