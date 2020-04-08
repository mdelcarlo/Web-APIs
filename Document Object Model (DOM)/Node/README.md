# Node

**Node** is an interface from which various types of **DOM API** objects inherit, allowing those types to be treated similarly; for example, inheriting the same set of methods, or being testable in the same way.

All of the following interfaces inherit the Node interface's methods and properties: [Document](./../Document/README.md), [Element](./../Element/README.md), Attr, CharacterData (which Text, Comment, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference

Those interfaces may return null in certain cases where the methods and properties are not relevant. They may throw an exception — for example when adding children to a node type for which no children can exist.

Inherits properties from its parent, [EventTarget](./../EventTarget/README.md).

## Properties

### Node.baseURI | Read only
Returns a DOMString representing the base URL of the document containing the Node.
Node.baseURIObject | Read only
(Not available to web content.) The nsIURI object representing the base URI for the element.

### Node.childNodes | Read only
Returns a live NodeList containing all the children of this node. NodeList being live means that if the children of the Node change, the NodeList object is automatically updated.

### Node.firstChild | Read only
Returns a Node representing the first direct child node of the node, or null if the node has no child.

### Node.isConnected | Read only
A boolean indicating whether or not the Node is connected (directly or indirectly) to the context object, e.g. the Document object in the case of the normal DOM, or the ShadowRoot in the case of a shadow DOM.

### Node.lastChild | Read only
Returns a Node representing the last direct child node of the node, or null if the node has no child.

### Node.nextSibling | Read only
Returns a Node representing the next node in the tree, or null if there isn't such node.

### Node.nodeName | Read only
Returns a DOMString containing the name of the Node. The structure of the name will differ with the node type. E.g. An HTMLElement will contain the name of the corresponding tag, like 'audio' for an HTMLAudioElement, a Text node will have the '#text' string, or a Document node will have the '#document' string.

### Node.nodeType | Read only
Returns an unsigned short representing the type of the node. Possible values are:

| Name | Value |
| ------------- |:-------------:|
| ELEMENT_NODE | 1 |
| ATTRIBUTE_NODE  | 2 |
| TEXT_NODE | 3 |
| CDATA_SECTION_NODE | 4 |
| ENTITY_REFERENCE_NODE  | 5 |
| ENTITY_NODE  | 6 |
| PROCESSING_INSTRUCTION_NODE | 7 |
| COMMENT_NODE | 8 |
| DOCUMENT_NODE | 9 |
| DOCUMENT_TYPE_NODE | 10 |
| DOCUMENT_FRAGMENT_NODE | 11 |
| NOTATION_NODE  | 12 |

### Node.nodeValue
Returns / Sets the value of the current node.
Node.ownerDocumentRead only
Returns the Document that this node belongs to. If the node is itself a document, returns null.

###  Node.parentNode | Read only
Returns a Node that is the parent of this node. If there is no such node, like if this node is the top of the tree or if doesn't participate in a tree, this property returns null.

### Node.parentElement | Read only
Returns an Element that is the parent of this node. If the node has no parent, or if that parent is not an Element, this property returns null.

###  Node.previousSibling | Read only
Returns a Node representing the previous node in the tree, or null if there isn't such node.

### Node.textContent
Returns / Sets the textual content of an element and all its descendants.

## Methods

### Node.appendChild(childNode)
Adds the specified childNode argument as the last child to the current node.
If the argument referenced an existing node on the DOM tree, the node will be detached from its current position and attached at the new position.

### Node.cloneNode()
Clone a Node, and optionally, all of its contents. By default, it clones the content of the node.

### Node.compareDocumentPosition()
Compares the position of the current node against another node in any other document.

### Node.contains()
Returns a Boolean value indicating whether or not a node is a descendant of the calling node.

### Node.getRootNode()
Returns the context object's root which optionally includes the shadow root if it is available. 

### Node.hasChildNodes()
Returns a Boolean indicating whether or not the element has any child nodes.

### Node.insertBefore()
Inserts a Node before the reference node as a child of a specified parent node.

### Node.isDefaultNamespace()
Accepts a namespace URI as an argument and returns a Boolean with a value of true if the namespace is the default namespace on the given node or false if not.

### Node.isEqualNode()
Returns a Boolean which indicates whether or not two nodes are of the same type and all their defining data points match.

### Node.isSameNode()
Returns a Boolean value indicating whether or not the two nodes are the same (that is, they reference the same object).

### Node.lookupPrefix()
Returns a DOMString containing the prefix for a given namespace URI, if present, and null if not. When multiple prefixes are possible, the result is implementation-dependent.

### Node.lookupNamespaceURI()
Accepts a prefix and returns the namespace URI associated with it on the given node if found(and null if not). Supplying null for the prefix will return the default namespace.

### Node.normalize()
Clean up all the text nodes under this element(merge adjacent, remove empty).

### Node.removeChild()
Removes a child node from the current element, which must be a child of the current node.

### Node.replaceChild()
Replaces one child Node of the current one with the second one given in parameter.

## Examples
#### Remove child nodes
Remove its child node until it doesn't have any children.

```js
function removeChildNodes(node)
{
    while (node.firstChild) {
        node.removeChild(node.firstChild);
    }
}
```

#### Remove a specific node
Remove a specific node accesing a parent and using removeChild.

```js
function removeNode(node)
{
    node.parentNode && node.parentNode.removeChild(node);
}
```

#### Replace a specific node
Replace a specific node accesing a parent and using replaceChild.

```js
function removeNode(node)
{
    node.parentNode && node.parentNode.replaceChild(newNode, node);
}
```