# Text
The **Text** interface represents the textual content of Element or Attr.

If an element has no markup within its content, it has a single child implementing **Text** that contains the element's text. However, if the element contains markup, it is parsed into information items and **Text** nodes that form its children.

New documents have a single **Text** node for each block of text. Over time, more **Text** nodes may be created as the document's content changes. The Node.normalize() method merges adjacent **Text** objects back into a single node for each block of text.

## Properties
Inherits properties from its parent, CharacterData.

#### Text.isElementContentWhitespace Read only
Returns a Boolean flag indicating whether or not the text node contains only whitespace.

#### Text.wholeText Read only
Returns a DOMString containing the text of all Text nodes logically adjacent to this Node, concatenated in document order.
#### Text.assignedSlot Read only
Returns the HTMLSlotElement object associated with the element.
### Properties included from Slotable
The Text interface includes the following property, defined on the Slotable mixin.

Slotable.assignedSlot Read only
Returns a HTMLSlotElement representing the <slot> the node is inserted in.
## Methods
Inherits methods from its parent, CharacterData.

#### Text.replaceWholeText 
Replaces the text of the current node and all logically adjacent nodes with the specified text.
#### Text.splitText
Breaks the node into two nodes at a specified offset.

## Examples

#### Split text node into several text nodes
```js
const p = document.querySelector('p');

// Get contents of <p> as a text node
const foobar = p.firstChild;

// Split 'foobar' into two text nodes, 'foo' and 'bar',
// and save 'bar' as a const
const bar = foobar.splitText(3);

// Create a <u> element containing ' new content '
const u = document.createElement('u');
u.appendChild(document.createTextNode(' new content '));

// Add <u> before 'bar'
p.insertBefore(u, bar);

// The result is: <p>foo<u> new content </u>bar</p>
```