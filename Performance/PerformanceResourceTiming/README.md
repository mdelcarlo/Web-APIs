# PerformanceResourceTiming
The PerformanceResourceTiming interface enables retrieval and analysis of detailed network timing data regarding the loading of an application's resources. An application can use the timing metrics to determine, for example, the length of time it takes to fetch a specific resource, such as an XMLHttpRequest, ``<SVG>``, ``image``, or ``script``.

The interface's properties create a resource loading timeline with high-resolution timestamps for network events such as redirect start and end times, fetch start, DNS lookup start and end times, response start and end times, etc.. Additionally, the interface extends PerformanceEntry with other properties which provide data about the size of the fetched resource as well as the type of resource that initiated the fetch.

## Properties
This interface extends the following PerformanceEntry properties for resource performance entry types by qualifying and constraining them as follows:

<img width="964" alt="Captura de Pantalla 2020-04-22 a la(s) 07 28 11" src="https://user-images.githubusercontent.com/20034230/79905770-e4e78780-846a-11ea-8625-b7936eff9969.png">

#### PerformanceEntry.entryType | Read only
Returns "resource".
#### PerformanceEntry.name | Read only
Returns the resources URL.
#### PerformanceEntry.startTime | Read only
Returns the timestamp for the time a resource fetch started. This value is equivalent to #### PerformanceEntry.fetchStart.
#### PerformanceEntry.duration | Read only
Returns a timestamp that is the difference between the responseEnd and the startTime properties.
The interface also supports the following properties which are listed in the order in which they are recorded for the fetching of a single resource. An alphabetical listing is shown in the navigation, at left.
#### 
PerformanceResourceTiming.initiatorType | Read only
A string representing the type of resource that initiated the performance entry, as specified in #### PerformanceResourceTiming.initiatorType.#### 
PerformanceResourceTiming.nextHopProtocol | Read only
A string representing the network protocol used to fetch the resource, as identified by the ALPN Protocol ID (RFC7301).
#### PerformanceResourceTiming.workerStar | tRead only
Returns a DOMHighResTimeStamp immediately before dispatching the FetchEvent if a Service Worker thread is already running, or immediately before starting the Service Worker thread if it is not already running. If the resource is not intercepted by a Service Worker the property will always return 0.#### 
PerformanceResourceTiming.redirectStart | Read only
A DOMHighResTimeStamp that represents the start time of the fetch which initiates the redirect.
#### PerformanceResourceTiming.redirectEn | dRead only
A DOMHighResTimeStamp immediately after receiving the last byte of the response of the last redirect.
#### PerformanceResourceTiming.fetchStart | Read only
A DOMHighResTimeStamp immediately before the browser starts to fetch the resource.#### 
PerformanceResourceTiming.domainLookupStar | tRead only
A DOMHighResTimeStamp immediately before the browser starts the domain name lookup for the resource.#### 
PerformanceResourceTiming.domainLookupEnd | Read only
A DOMHighResTimeStamp representing the time immediately after the browser finishes the domain name lookup for the resource.#### 
PerformanceResourceTiming.connectStart | Read only
A DOMHighResTimeStamp immediately before the browser starts to establish the connection to the server to retrieve the resource.
#### PerformanceResourceTiming.connectEnd | Read only
A DOMHighResTimeStamp immediately after the browser finishes establishing the connection to the server to retrieve the resource.#### 
PerformanceResourceTiming.secureConnectionStart | Read only
A DOMHighResTimeStamp immediately before the browser starts the handshake process to secure the current connection.#### 
PerformanceResourceTiming.requestStart | Read only
A DOMHighResTimeStamp immediately before the browser starts requesting the resource from the server.#### 
PerformanceResourceTiming.responseStart | Read only
A DOMHighResTimeStamp immediately after the browser receives the first byte of the response from the server.
#### PerformanceResourceTiming.responseEn | dRead only
A DOMHighResTimeStamp immediately after the browser receives the last byte of the resource or immediately before the transport connection is closed, whichever comes first.#### 
PerformanceResourceTiming.transferSize | Read only
A number representing the size (in octets) of the fetched resource. The size includes the response header fields plus the response payload body.#### 
PerformanceResourceTiming.encodedBodySize | Read only
A number representing the size (in octets) received from the fetch (HTTP or cache), of the payload body, before removing any applied content-codings.
#### PerformanceResourceTiming.decodedBodySize | Read only
A number that is the size (in octets) received from the fetch (HTTP or cache) of the message body, after removing any applied content-codings.
#### PerformanceResourceTiming.serverTimin | gRead only
An array of PerformanceServerTiming entries containing server timing metrics.
## Methods
#### PerformanceResourceTiming.toJSON()
Returns a DOMString that is the JSON representation of the PerformanceResourceTiming object.
## Example
See the example in Using the Resource Timing API.

## Examples

#### Timing resource loading phases
The following example illustrates using the resource timing properties to calculate the amount of time the following phases take: redirection (redirectStart and redirectEnd ), DNS lookup (domainLookupStart and domainLookupEnd), TCP handshake (connectStart and connectEnd), and response (responseStart and responseEnd). This example also calculates the time from the start of the fetch and request start phases (fetchStart and requestStart, respectively), until the response has ended (responseEnd). This timing data provides a detailed profile of the resource loading phases and this data can be used to help identify performance bottlenecks.

```js
function calculate_load_times() {
  // Check performance support
  if (performance === undefined) {
    console.log("= Calculate Load Times: performance NOT supported");
    return;
  }

  // Get a list of "resource" performance entries
  var resources = performance.getEntriesByType("resource");
  if (resources === undefined || resources.length <= 0) {
    console.log("= Calculate Load Times: there are NO `resource` performance records");
    return;
  }

  console.log("= Calculate Load Times");
  for (var i=0; i < resources.length; i++) {
    console.log("== Resource[" + i + "] - " + resources[i].name);
    // Redirect time
    var t = resources[i].redirectEnd - resources[i].redirectStart;
    console.log("... Redirect time = " + t);

    // DNS time
    t = resources[i].domainLookupEnd - resources[i].domainLookupStart;
    console.log("... DNS lookup time = " + t);

    // TCP handshake time
    t = resources[i].connectEnd - resources[i].connectStart;
    console.log("... TCP time = " + t);

    // Secure connection time
    t = (resources[i].secureConnectionStart > 0) ? (resources[i].connectEnd - resources[i].secureConnectionStart) : "0";
    console.log("... Secure connection time = " + t);

    // Response time
    t = resources[i].responseEnd - resources[i].responseStart;
    console.log("... Response time = " + t);

    // Fetch until response end
    t = (resources[i].fetchStart > 0) ? (resources[i].responseEnd - resources[i].fetchStart) : "0";
    console.log("... Fetch until response end time = " + t);

    // Request start until reponse end
    t = (resources[i].requestStart > 0) ? (resources[i].responseEnd - resources[i].requestStart) : "0";
    console.log("... Request start until response end time = " + t);

    // Start until reponse end
    t = (resources[i].startTime > 0) ? (resources[i].responseEnd - resources[i].startTime) : "0";
    console.log("... Start until response end time = " + t);
  }
}
```

#### Size matters?
The size of an application's resources can affect an application's performance so getting accurate data on resource size can be important (especially for non-hosted resources). The PerformanceResourceTiming interface has three properties that can be used to obtain size data about a resource. The transferSize property returns the size (in octets) of the fetched resource including the response header fields plus the response payload body. The encodedBodySize property returns the size (in octets) received from the fetch (HTTP or cache), of the payload body, before removing any applied content-codings. decodedBodySize returns the size (in octets) received from the fetch (HTTP or cache) of the message body, after removing any applied content-codings.

The following example demonstrates using these three properties.
```js
function display_size_data(){
  // Check for support of the PerformanceResourceTiming.*size properties and print their values
  // if supported.
  if (performance === undefined) {
    console.log("= Display Size Data: performance NOT supported");
    return;
  }

  var list = performance.getEntriesByType("resource");
  if (list === undefined) {
    console.log("= Display Size Data: performance.getEntriesByType() is  NOT supported");
    return;
  }

  // For each "resource", display its *Size property values
  console.log("= Display Size Data");
  for (var i=0; i < list.length; i++) {
    console.log("== Resource[" + i + "] - " + list[i].name);
    if ("decodedBodySize" in list[i])
      console.log("... decodedBodySize[" + i + "] = " + list[i].decodedBodySize);
    else
      console.log("... decodedBodySize[" + i + "] = NOT supported");

    if ("encodedBodySize" in list[i])
      console.log("... encodedBodySize[" + i + "] = " + list[i].encodedBodySize);
    else
      console.log("... encodedBodySize[" + i + "] = NOT supported");

    if ("transferSize" in list[i])
      console.log("... transferSize[" + i + "] = " + list[i].transferSize);
    else
      console.log("... transferSize[" + i + "] = NOT supported");
  }
}
```
#### Managing the resource buffer
Although the browser is required to support at least 150 resource timing performance entries in its resource timing buffer, some applications may use more resources than that limit. To help the developer manage the buffer size, Resource Timing defines two methods that extend the Performance interface. The clearResourceTimings() method removes all "resource" type performance entries from the browser's resource performance entry buffer. The setResourceTimingBufferSize() method sets the resource performance entry buffer size to the specified number of resource performance entries.

The following example demonstrates the usage of these two methods.
```js
function clear_resource_timings() {
  if (performance === undefined) {
    console.log("= performance.clearResourceTimings(): peformance NOT supported");
    return;
  }
  // Check if Performance.clearResourceTiming() is supported 
  console.log ("= Print performance.clearResourceTimings()");
  var supported = typeof performance.clearResourceTimings == "function";
  if (supported) {
    console.log("... Performance.clearResourceTimings() = supported");
    performance.clearResourceTimings();
  } else {
    console.log("... Performance.clearResourceTiming() = NOT supported");
    return;
  }
  // getEntries should now return zero
  var p = performance.getEntriesByType("resource");
  if (p.length == 0)  
    console.log("... Performance data buffer cleared");
  else
    console.log("... Performance data buffer NOT cleared (still have `" + p.length + "` items");
}

function set_resource_timing_buffer_size(n) {
  if (performance === undefined) {
    console.log("= performance.setResourceTimingBufferSize(): peformance NOT supported");
    return;
  }
  // Check if Performance.setResourceTimingBufferSize() is supported 
  console.log ("= performance.setResourceTimingBufferSize()");
  var supported = typeof performance.setResourceTimingBufferSize == "function";
  if (supported) {
    console.log("... Performance.setResourceTimingBufferSize() = supported");
    performance.setResourceTimingBufferSize(n);
  } else {
    console.log("... Performance.setResourceTimingBufferSize() = NOT supported");
  }
}
```
The Performance interface has a onresourcetimingbufferfull event handler that gets called (with an Event of type Event.type of "resourcetimingbufferfull") when the browser's resource performance entry buffer is full. The following code example sets a onresourcetimingbufferfull event callback in the init() function.
```js
function buffer_full(event) {
  console.log("WARNING: Resource Timing Buffer is FULL!");
  set_resource_timing_buffer_size(200);
}

function init() {
  // load some image to trigger "resource" fetch events
  var image1 = new Image();
  image1.src = "https://developer.mozilla.org/static/img/opengraph-logo.png";
  var image2 = new Image();
  image2.src = "http://mozorg.cdn.mozilla.net/media/img/firefox/firefox-256.e2c1fc556816.jpg"
 
  // Set a callback if the resource buffer becomes filled
  performance.onresourcetimingbufferfull = buffer_full;
}
```

#### Coping with CORS
When CORS is in effect, many of the timing properties' values are returned as zero unless the server's access policy permits these values to be shared. This requires the server providing the resource to send the Timing-Allow-Origin HTTP response header with a value specifying the origin or origins which are allowed to get the restricted timestamp values.