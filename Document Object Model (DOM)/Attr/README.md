# Attr
The Attr interface represents one of a DOM element's attributes as an object. In most DOM methods, you will directly retrieve the attribute as a string (e.g., Element.getAttribute()), but certain functions (e.g., Element.getAttributeNode()) or means of iterating return Attr types.

---
## Properties
#### name | Read only
The attribute's name.
namespaceURI | Read only
A DOMString representing the namespace URI of the attribute, or null if there is no namespace.
#### localName | Read only
A DOMString representing the local part of the qualified name of the attribute.
#### prefix | Read only
A DOMString representing the namespace prefix of the attribute, or null if no prefix is specified.
#### ownerElement | Read only
The element holding the attribute.

#### specified | Read only
This property always returns true. Originally, it returned true if the attribute was explicitly specified in the source code or by a script, and false if its value came from the default one defined in the document's DTD.
#### value
The attribute's value.

## Examples
#### Get an array of attribute local name and value of the element

```js
const getAttrsLocalNameAndValue = element => element.attributes.map(getAttrLocalNameAndValue);

const getAttrLocalNameAndValue = attr => ({
    localName: attr.localName,
    value: attr.value,
});
```