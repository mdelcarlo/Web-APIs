# ParentNode

The **ParentNode** mixin contains methods and properties that are common to all types of Node objects that can have children. It's implemented by [Element](./../Element/README.md), [Document](./../Document/README.md), and [DocumentFragment](./../DocumentFragment/README.md) objects.

## Properties

#### ParentNode.childElementCount | Read only
Returns the number of children of this ParentNode which are elements.
#### ParentNode.children | Read only
Returns a live HTMLCollection containing all of the Element objects that are children of this ParentNode, omitting all of its non-element nodes.
#### ParentNode.firstElementChild | Read only
Returns the first node which is both a child of this ParentNode and is also an Element, or null if there is none.
#### ParentNode.lastElementChild | Read only
Returns the last node which is both a child of this ParentNode and is an Element, or null if there is none.

## Methods
#### ParentNode.append() 
Inserts a set of Node objects or DOMString objects after the last child of the ParentNode. DOMString objects are inserted as equivalent Text nodes.
#### ParentNode.prepend() 
Inserts a set of Node objects or DOMString objects before the first child of the ParentNode. DOMString objects are inserted as equivalent Text nodes.
#### ParentNode.querySelector()
Returns the first Element with the current element as root that matches the specified group of selectors.
#### ParentNode.querySelectorAll()
Returns a NodeList representing a list of elements with the current element as root that matches the specified group of selectors.

## Examples
#### Appending an element and text

```js
let parent = document.createElement("div")
let p = document.createElement("p")
parent.append("Some text", p)

console.log(parent.childNodes) // NodeList [ #text "Some text", <p> ]
```
