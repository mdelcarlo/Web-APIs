# Blob
The Blob object represents a blob, which is a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a ReadableStream so its methods can be used for processing the data.

Blobs can represent data that isn't necessarily in a JavaScript-native format. The File interface is based on Blob, inheriting blob functionality and expanding it to support files on the user's system.

## Properties
#### Blob.size Read only
The size, in bytes, of the data contained in the Blob object.
#### Blob.type Read only
A string indicating the MIME type of the data contained in the Blob. If the type is unknown, this string is empty.
## Methods
#### Blob.arrayBuffer()
Returns a promise that resolves with an ArrayBuffer containing the entire contents of the Blob as binary data.
#### Blob.slice()
Returns a new Blob object containing the data in the specified range of bytes of the blob on which it's called.
#### Blob.stream()
Returns a ReadableStream that can be used to read the contents of the Blob.
#### Blob.text()
Returns a promise that resolves with a USVString containing the entire contents of the Blob interpreted as UTF-8 text.
## Examples
####Creating a blob
The Blob() constructor can create blobs from other objects. For example, to construct a blob from a JSON string:

```js
const obj = {hello: 'world'};
const blob = new Blob([JSON.stringify(obj, null, 2)], {type : 'application/json'});
```
