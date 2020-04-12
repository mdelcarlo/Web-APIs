# File
The File interface provides information about files and allows JavaScript in a web page to access their content.

File objects are generally retrieved from a FileList object returned as a result of a user selecting files using the ```<input>``` element, from a drag and drop operation's DataTransfer object, or from the ```mozGetAsFile()``` API on an HTMLCanvasElement.

A File object is a specific kind of a Blob, and can be used in any context that a Blob can. In particular, FileReader, ```URL.createObjectURL()```, ```createImageBitmap()```, and ```XMLHttpRequest.send()``` accept both Blobs and Files.

## Properties
#### File.lastModified | Read only
Returns the last modified time of the file, in millisecond since the UNIX epoch (January 1st, 1970 at Midnight).
#### File.lastModifiedDate  | Read only
Returns the last modified Date of the file referenced by the File object.
#### File.name | Read only
Returns the name of the file referenced by the File object.
#### File.webkitRelativePath  | Read only
Returns the path the URL of the File is relative to.
File implements Blob, so it also has the following properties available to it:

#### File.size | Read only
Returns the size of the file in bytes.
#### File.type | Read only
Returns the MIME type of the file.

## Methods
The File interface doesn't define any methods, but inherits methods from the Blob interface

## Examples
Reading from file input
```html
<input type="file" multiple id="fileInput">
```

```js
const fileInput = document.querySelector('#fileInput');
fileInput.addEventListener('change', (event) => {
  // files is a FileList object (similar to NodeList) 
  const files = event.target.files;

  for (let file of files) {
    const date = new Date(file.lastModified);
    console.log(`${file.name} has a last modified date of ${date}`);
  }
});
```js