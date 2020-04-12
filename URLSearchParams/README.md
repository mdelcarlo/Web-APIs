# URLSearchParams
The **URLSearchParams** interface defines utility methods to work with the query string of a URL.

An object implementing **URLSearchParams** can directly be used in a ```for...of``` structure, for example the following two lines are equivalent:

```js
for (const [key, value] of mySearchParams) {}
```
```js
for (const [key, value] of mySearchParams.entries()) {}
```

## Constructor
#### URLSearchParams()
Returns a URLSearchParams object instance.
#### Methods
#### URLSearchParams.append()
Appends a specified key/value pair as a new search parameter.
#### URLSearchParams.delete()
Deletes the given search parameter, and its associated value, from the list of all search parameters.
#### URLSearchParams.entries()
Returns an iterator allowing iteration through all key/value pairs contained in this object.
#### URLSearchParams.forEach()
Allows iteration through all values contained in this object via a callback function.
#### URLSearchParams.get()
Returns the first value associated with the given search parameter.
#### URLSearchParams.getAll()
Returns all the values associated with a given search parameter.
#### URLSearchParams.has()
Returns a Boolean indicating if such a given parameter exists.
#### URLSearchParams.keys()
Returns an iterator allowing iteration through all keys of the key/value pairs contained in this object.
#### URLSearchParams.set()
Sets the value associated with a given search parameter to the given value. If there are several values, the others are deleted.
#### URLSearchParams.sort()
Sorts all key/value pairs, if any, by their keys.
#### URLSearchParams.toString()
Returns a string containing a query string suitable for use in a URL.
#### URLSearchParams.values()
Returns an iterator allowing iteration through all values of the key/value pairs contained in this object.

## Examples
#### Play with URLSearchParams

```js
var paramsString = "q=URLUtils.searchParams&topic=api";
var searchParams = new URLSearchParams(paramsString);

//Iterate the search parameters.
for (let p of searchParams) {
  console.log(p);
}

searchParams.has("topic") === true; // true
searchParams.get("topic") === "api"; // true
searchParams.getAll("topic"); // ["api"]
searchParams.get("foo") === null; // true
searchParams.append("topic", "webdev");
searchParams.toString(); // "q=URLUtils.searchParams&topic=api&topic=webdev"
searchParams.set("topic", "More webdev");
searchParams.toString(); // "q=URLUtils.searchParams&topic=More+webdev"
searchParams.delete("topic");
searchParams.toString(); // "q=URLUtils.searchParams"
```