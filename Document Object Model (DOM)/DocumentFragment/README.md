# DocumentFragment
The **DocumentFragment** interface represents a minimal document object that has no parent. It is used as a lightweight version of Document that stores a segment of a document structure comprised of nodes just like a standard document. The key difference is due to the fact that the document fragment isn't part of the active document tree structure. Changes made to the fragment don't affect the document (even on reflow) or incur any performance impact when changes are made.

A common use for **DocumentFragment** is to create one, assemble a DOM subtree within it, then append or insert the fragment into the DOM using [Node](./../Node/README.md) interface methods such as **appendChild()** or **insertBefore()**. Doing this moves the fragment's nodes into the DOM, leaving behind an empty **DocumentFragment**. Because all of the nodes are inserted into the document at once, only one reflow and render is triggered instead of potentially one for each node inserted if they were inserted separately.

An empty **DocumentFragment** can be created using the **document.createDocumentFragment()** method or the constructor.

---

## Constructor
DocumentFragment()
Creates a new DocumentFragment object.

---

## Properties
This interface has no specific properties, but inherits those of its parent, [Node](./../Node/README.md), and implements those of the [ParentNode](./../ParentNode/README.md) interface.


## Methods
This interface inherits the methods of its parent, [Node](./../Node/README.md), and implements those of the [ParentNode](./../ParentNode/README.md) interface.

## Example

HTML
```html
<ul id="list"></ul>
```

JavaScript
```js
var list = document.querySelector('#list')
var fruits = ['Apple', 'Orange', 'Banana', 'Melon']

var fragment = new DocumentFragment()

fruits.forEach(function (fruit) {
  var li = document.createElement('li')
  li.innerHTML = fruit
  fragment.appendChild(li)
})

list.appendChild(fragment)
```
