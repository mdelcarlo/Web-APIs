# HTMLCollection
The **HTMLCollection** interface represents a generic collection (array-like object similar to arguments) of elements (in document order) and offers methods and properties for selecting from the list.

>Note: This interface is called **HTMLCollection** for historical reasons (before the modern DOM, collections implementing this interface could only have HTML elements as their items).

An **HTMLCollection** in the HTML DOM is live; it is automatically updated when the underlying document is changed.

The getElementsByTagName method returns an **HTMLCollection**.

## Properties
#### HTMLCollection.length Read only
Returns the number of items in the collection.

## Methods
#### HTMLCollection.item()
Returns the specific node at the given zero-based index into the list. Returns null if the index is out of range.
An alternative to accessing collection[i] (which instead returns  undefined when i is out-of-bounds). This is mostly useful for non-JavaScript DOM implementations.
#### HTMLCollection.namedItem()
Returns the specific node whose ID or, as a fallback, name matches the string specified by name. Matching by name is only done as a last resort, only in HTML, and only if the referenced element supports the name attribute. Returns null if no node exists by the given name.
An alternative to accessing collection[name] (which instead returns  undefined when name does not exist). This is mostly useful for non-JavaScript DOM implementations.