# URL

The URL API is a component of the URL standard, which defines what constitutes a valid Uniform Resource Locator and the API that accesses and manipulates URLs. The URL standard also defines concepts such as domains, hosts, and IP addresses, and also attempts to describe in a standard way the legacy application/x-www-form-urlencoded MIME type used to submit web forms' contents as a set of key/value pairs.

## URL concepts and usage
The majority of the URL standard is taken up by the definition of a URL and how it is structured and parsed. Also covered are definitions of various terms related to addressing of computers on a network, and the algorithms for parsing IP addresses and DOM addresses are specified. More interesting to most developers is the API itself.

#### Accessing URL components
Creating an URL object for a given URL parses the URL and provides quick access to its constituent parts through its properties.
```js
let addr = new URL("https://developer.mozilla.org/en-US/docs/Web/API/URL_API");
let host = addr.host;
let path = addr.pathname;
```
The snippet above creates a URL object for the article you're reading right now, then fetches the host and pathname properties. In this case, those strings are developer.mozilla.org and /en-US/docs/Web/API/URL_API, respectively.

#### Changing the URL
Most of the properties of URL are settable; you can write new values to them to alter the URL represented by the object. For example, to create a URL and set its username:
```js
let myUsername = "someguy";
let addr = new URL("https://mysite.com/login");
addr.username = myUsername;
```
Setting the value of username not only sets that property's value, but it updates the overall URL. After executing the code snippet above, the value returned by addr.href is https://someguy@mysite.com/login. This is true for any of the writable properties.

#### Queries
The search property on a URL contains the query string portion of the URL. For example, if the URL is `https://mysite.com/login?user=someguy&page=news`, then the value of the search property is ?user=someguy&page=news. You can also look up the values of individual parameters with the URLSearchParams object's get() method:
```js
let addr = new URL("https://mysite.com/login?user=someguy&page=news");
try {
  loginUser(addr.searchParams.get("user"));
  gotoPage(addr.searchParams.get("page"));
} catch(err) {
  showErrorMessage(err);
}
```