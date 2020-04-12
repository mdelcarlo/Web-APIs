# FormData
The **FormData** interface provides a way to easily construct a set of key/value pairs representing form fields and their values, which can then be easily sent using the ```XMLHttpRequest.send()``` method. It uses the same format a form would use if the encoding type were set to ```"multipart/form-data"```.

You can also pass it directly to the URLSearchParams constructor if you want to generate query parameters in the way a ```<form>``` would do if it were using simple GET submission.

An object implementing **FormData** can directly be used in a ```for...of``` structure, instead of ```entries()```: ```for (var p of myFormData)``` is equivalent to ```for (var p of myFormData.entries())```.

## Constructor
#### FormData()
Creates a new FormData object.
## Methods
#### FormData.append()
Appends a new value onto an existing key inside a FormData object, or adds the key if it does not already exist.
#### FormData.delete()
Deletes a key/value pair from a FormData object.
#### FormData.entries()
Returns an iterator allowing to go through all key/value pairs contained in this object.
#### FormData.get()
Returns the first value associated with a given key from within a FormData object.
#### FormData.getAll()
Returns an array of all the values associated with a given key from within a #### FormData.
#### FormData.has()
Returns a boolean stating whether a FormData object contains a certain key.
#### FormData.keys()
Returns an iterator allowing to go through all keys of the key/value pairs contained in this object.
#### FormData.set()
Sets a new value for an existing key inside a FormData object, or adds the key/value if it does not already exist.
#### FormData.values()
Returns an iterator allowing to go through all values  contained in this object.

## Examples

#### Create a FormData object

```js
// Create a test FormData object
var formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');

// Display the key/value pairs
for(var pair of formData.entries()) {
   console.log(pair[0]+ ', '+ pair[1]); 
}
```

#### Return every value of a key

```js
var formData = new FormData();

formData.append('username', 'Chris');
formData.append('username', 'Bob');

formData.getAll('username'); // Returns ["Chris", "Bob"]
```

#### Set new values
```js
var formData = new FormData(); // Currently empty

formData.set('username', 'Chris');
formData.set('userpic', myFileInput.files[0], 'chris.jpg');

formData.set('name', 72);
formData.get('name'); // "72"
```
