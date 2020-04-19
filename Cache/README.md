# Cache
The Cache interface provides a storage mechanism for Request / Response object pairs that are cached, for example as part of the ServiceWorker life cycle. Note that the Cache interface is exposed to windowed scopes as well as workers. You don't have to use it in conjunction with service workers, even though it is defined in the service worker spec.

An origin can have multiple, named Cache objects. You are responsible for implementing how your script (e.g. in a ServiceWorker) handles Cache updates. Items in a Cache do not get updated unless explicitly requested; they don’t expire unless deleted. Use CacheStorage.open() to open a specific named Cache object and then call any of the Cache methods to maintain the Cache.

You are also responsible for periodically purging cache entries. Each browser has a hard limit on the amount of cache storage that a given origin can use. Cache quota usage estimates are available via the StorageEstimate API. The browser does its best to manage disk space, but it may delete the Cache storage for an origin. The browser will generally delete all of the data for an origin or none of the data for an origin. Make sure to version caches by name and use the caches only from the version of the script that they can safely operate on. See Deleting old caches for more information.

## Methods
#### Cache.match(request, options)
Returns a Promise that resolves to the response associated with the first matching request in the Cache object.
#### Cache.matchAll(request, options)
Returns a Promise that resolves to an array of all matching requests in the Cache object.
#### Cache.add(request)
Takes a URL, retrieves it and adds the resulting response object to the given cache. This is functionally equivalent to calling fetch(), then using put() to add the results to the cache.
#### Cache.addAll(requests)
Takes an array of URLs, retrieves them, and adds the resulting response objects to the given cache.
#### Cache.put(request, response)
Takes both a request and its response and adds it to the given cache.
#### Cache.delete(request, options)
Finds the Cache entry whose key is the request, returning a Promise that resolves to true if a matching Cache entry is found and deleted. If no Cache entry is found, the promise resolves to false.
#### Cache.keys(request, options)
Returns a Promise that resolves to an array of Cache keys.