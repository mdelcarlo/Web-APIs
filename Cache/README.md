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

## Examples
#### Custom responses to requests with respondWith, Deleting old caches with Activate and Recovering failed requests

<img width="585" alt="Captura de Pantalla 2020-04-21 a la(s) 07 49 29" src="https://user-images.githubusercontent.com/20034230/79793464-b99a6500-83a4-11ea-9e03-641a676c03f8.png">

```js
// If at any point you want to force pages that use this service worker to start using a fresh
// cache, then increment the CACHE_VERSION value. It will kick off the service worker update
// flow and the old cache(s) will be purged as part of the activate event handler when the
// updated service worker is activated.
const CACHE_VERSION = 1;
const CURRENT_CACHES = {
  font: 'font-cache-v' + CACHE_VERSION
};

self.addEventListener('activate', function(event) {
  // Delete all caches that aren't named in CURRENT_CACHES.
  // While there is only one cache in this example, the same logic will handle the case where
  // there are multiple versioned caches.
  const expectedCacheNamesSet = new Set(Object.values(CURRENT_CACHES));
  event.waitUntil(
    caches.keys().then(function(cacheNames) {
      return Promise.all(
        cacheNames.map(function(cacheName) {
          if (!expectedCacheNamesSet.has(cacheName)) {
            // If this cache name isn't present in the set of "expected" cache names, then delete it.
            console.log('Deleting out of date cache:', cacheName);
            return caches.delete(cacheName);
          }
        })
      );
    })
  );
});

self.addEventListener('fetch', function(event) {
  console.log('Handling fetch event for', event.request.url);

  event.respondWith(
    caches.open(CURRENT_CACHES.font).then(function(cache) {
      return cache.match(event.request).then(function(response) {
        if (response) {
          // If there is an entry in the cache for event.request, then response will be defined
          // and we can just return it. Note that in this example, only font resources are cached.
          console.log(' Found response in cache:', response);

          return response;
        }

        // Otherwise, if there is no entry in the cache for event.request, response will be
        // undefined, and we need to fetch() the resource.
        console.log(' No response for %s found in cache. About to fetch ' +
          'from network...', event.request.url);

        // We call .clone() on the request since we might use it in a call to cache.put() later on.
        // Both fetch() and cache.put() "consume" the request, so we need to make a copy.
        return fetch(event.request.clone()).then(function(response) {
          console.log('  Response for %s from network is: %O',
            event.request.url, response);

          if (response.status < 400 &&
              response.headers.has('content-type') &&
              response.headers.get('content-type').match(/^font\//i)) {
            // This avoids caching responses that we know are errors (i.e. HTTP status code of 4xx or 5xx).
            // We also only want to cache responses that correspond to fonts,
            // i.e. have a Content-Type response header that starts with "font/".
            // We call .clone() on the response to save a copy of it to the cache. By doing so, we get to keep
            // the original response object which we will return back to the controlled page.
            console.log('  Caching the response to', event.request.url);
            cache.put(event.request, response.clone());
          } else {
            console.log('  Not caching the response to', event.request.url);
          }

          // Return the original response object, which will be used to fulfill the resource request.
          return response;
        });
      }).catch(function(error) {
        // This catch() will handle exceptions that arise from the match() or fetch() operations.
        // Note that a HTTP error response (e.g. 404) will NOT trigger an exception.
        // It will return a normal response object that has the appropriate error code set.
        console.error('  Error in fetch handler:', error);

        throw error;
      });
    })
  );
});
```