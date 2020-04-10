# NodeList
**NodeList** objects are collections of nodes, usually returned by properties such as Node.childNodes and methods such as document.querySelectorAll().

> Although NodeList is not an Array, it is possible to iterate over it with forEach(). It can also be converted to a real Array using Array.from().

## Properties
#### NodeList.length
The number of nodes in the NodeList.

## Methods
#### NodeList.item()
Returns an item in the list by its index, or null if the index is out-of-bounds.
An alternative to accessing nodeList[i] (which instead returns  undefined when i is out-of-bounds). This is mostly useful for non-JavaScript DOM implementations.
#### NodeList.entries()
Returns an iterator, allowing code to go through all key/value pairs contained in the collection. (In this case, the keys are numbers starting from 0 and the values are nodes.)
#### NodeList.forEach()
Executes a provided function once per NodeList element, passing the element as an argument to the function.
#### NodeList.keys()
Returns an iterator, allowing code to go through all the keys of the key/value pairs contained in the collection. (In this case, the keys are numbers starting from 0.)
#### NodeList.values()
Returns an iterator allowing code to go through all values (nodes) of the key/value pairs contained in the collection.

## Examples

#### Iterate NodeList values

```js
var node = document.createElement("div"); 
var kid1 = document.createElement("p"); 
var kid2 = document.createTextNode("hey"); 
var kid3 = document.createElement("span"); 

node.appendChild(kid1); 
node.appendChild(kid2); 
node.appendChild(kid3); 

var list = node.childNodes; 

// Using for..of 
for(var value of list.values()) { 
  console.log(value); 
}
```
