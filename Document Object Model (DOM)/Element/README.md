# Element
**Element** is the most general base class from which all element objects (i.e. objects that represent elements) in a [Document](./../Document/README.md) inherit. It only has methods and properties common to all kinds of elements. More specific classes inherit from **Element**. For example, the HTMLElement interface is the base interface for HTML elements, while the SVGElement interface is the basis for all SVG elements. Most functionality is specified further down the class hierarchy.

Inherits properties from its parent interface, [Node](./../Node/README.md), and by extension that interface's parent, [EventTarget](./../EventTarget/README.md).

## Properties

### Element.attributes | Read only
Returns a NamedNodeMap object containing the assigned attributes of the corresponding HTML element.

### Element.classList | Read only
Returns a DOMTokenList containing the list of class attributes.

### Element.className
Is a DOMString representing the class of the element.

### Element.clientHeight | Read only
Returns a Number representing the inner height of the element.

### Element.clientLeft | Read only
Returns a Number representing the width of the left border of the element.

### Element.clientTop | Read only
Returns a Number representing the width of the top border of the element.

### Element.clientWidth | Read only
Returns a Number representing the inner width of the element.

### Element.computedName | Read only
Returns a DOMString containing the label exposed to accessibility.

### Element.computedRole | Read only
Returns a DOMString containing the ARIA role that has been applied to a particular element.

### Element.id
Is a DOMString representing the id of the element.

### Element.innerHTML
Is a DOMString representing the markup of the element's content.

### Element.localName | Read only
A DOMString representing the local part of the qualified name of the element.

### Element.namespaceURI | Read only
The namespace URI of the element, or null if it is no namespace.

### NonDocumentTypeChildNode.nextElementSibling | Read only
Is an Element, the element immediately following the given one in the tree, or null if there's no sibling node.

### Element.outerHTML
Is a DOMString representing the markup of the element including its content. When used as a setter, replaces the element with nodes parsed from the given string.

### Element.part
Represents the part identifier(s) of the element (i.e. set using the part attribute), returned as a DOMTokenList.

### Element.prefix | Read only
A DOMString representing the namespace prefix of the element, or null if no prefix is specified.

### NonDocumentTypeChildNode.previousElementSibling | Read only
Is a Element, the element immediately preceding the given one in the tree, or null if there is no sibling element.

### Element.scrollHeight | Read only
Returns a Number representing the scroll view height of an element.

### Element.scrollLeft
Is a Number representing the left scroll offset of the element.

### Element.scrollLeftMax  Read only
Returns a Number representing the maximum left scroll offset possible for the element.

### Element.scrollTop
A Number representing number of pixels the top of the document is scrolled vertically.

### Element.scrollTopMax | Read only
Returns a Number representing the maximum top scroll offset possible for the element.

### Element.scrollWidth | Read only
Returns a Number representing the scroll view width of the element.

### Element.shadowRoot | Read only
Returns the open shadow root that is hosted by the element, or null if no open shadow root is present.

### Element.openOrClosedShadowRoot | Read only
Returns the shadow root that is hosted by the element, regardless if its open or closed. Available only to WebExtensions.

### Element.slot 
Returns the name of the shadow DOM slot the element is inserted in.

### Element.tabStop 
Is a Boolean indicating if the element can receive input focus via the tab key.

### Element.tagName | Read only
Returns a String with the name of the tag for the given element.

## Methods

### EventTarget.addEventListener()
Registers an event handler to a specific event type on the element.

### Element.attachShadow()
Attaches a shadow DOM tree to the specified element and returns a reference to its ShadowRoot.

### Element.animate() 
A shortcut method to create and run an animation on an element. Returns the created Animation object instance.

### Element.closest() 
Returns the Element which is the closest ancestor of the current element (or the current element itself) which matches the selectors given in parameter.

### Element.createShadowRoot()  
Creates a shadow DOM on on the element, turning it into a shadow host. Returns a ShadowRoot.

### Element.computedStyleMap() 
Returns a StylePropertyMapReadOnly interface which provides a read-only representation of a CSS declaration block that is an alternative to CSSStyleDeclaration.

### EventTarget.dispatchEvent()
Dispatches an event to this node in the DOM and returns a Boolean that indicates whether no handler canceled the event.

### Element.getAnimations() 
Returns an array of Animation objects currently active on the element.

### Element.getAttribute()
Retrieves the value of the named attribute from the current node and returns it as an Object.

### Element.getAttributeNames()
Returns an array of attribute names from the current element.

### Element.getAttributeNS()
Retrieves the value of the attribute with the specified name and namespace, from the current node and returns it as an Object.

### Element.getAttributeNode() 
Retrieves the node representation of the named attribute from the current node and returns it as an Attr.

### Element.getAttributeNodeNS() 
Retrieves the node representation of the attribute with the specified name and namespace, from the current node and returns it as an Attr.

### Element.getBoundingClientRect()
Returns the size of an element and its position relative to the viewport.

### Element.getClientRects()
Returns a collection of rectangles that indicate the bounding rectangles for each line of text in a client.

### Element.getElementsByClassName()
Returns a live HTMLCollection that contains all descendants of the current element that possess the list of classes given in the parameter.

### Element.getElementsByTagName()
Returns a live HTMLCollection containing all descendant elements, of a particular tag name, from the current element.

### Element.getElementsByTagNameNS()
Returns a live HTMLCollection containing all descendant elements, of a particular tag name and namespace, from the current element.

### Element.hasAttribute()
Returns a Boolean indicating if the element has the specified attribute or not.

### Element.hasAttributeNS()
Returns a Boolean indicating if the element has the specified attribute, in the specified namespace, or not.

### Element.hasAttributes()
Returns a Boolean indicating if the element has one or more HTML attributes present.

### Element.hasPointerCapture()
Indicates whether the element on which it is invoked has pointer capture for the pointer identified by the given pointer ID.

### Element.insertAdjacentElement()
Inserts a given element node at a given position relative to the element it is invoked upon.

### Element.insertAdjacentHTML()
Parses the text as HTML or XML and inserts the resulting nodes into the tree in the position given.

### Element.insertAdjacentText()
Inserts a given text node at a given position relative to the element it is invoked upon.

### Element.matches() 
Returns a Boolean indicating whether or not the element would be selected by the specified selector string.

### Element.pseudo() 
Returns a CSSPseudoElement representing the child pseudo-element matched by the specified pseudo-element selector.

### Element.querySelector()
Returns the first Node which matches the specified selector string relative to the element.

### Element.querySelectorAll()
Returns a NodeList of nodes which match the specified selector string relative to the element.

### Element.releasePointerCapture()
Releases (stops) pointer capture that was previously set for a specific pointer event.
ChildNode.remove() 
Removes the element from the children list of its parent.

### Element.removeAttribute()
Removes the named attribute from the current node.

### Element.removeAttributeNS()
Removes the attribute with the specified name and namespace, from the current node.

### Element.removeAttributeNode() 
Removes the node representation of the named attribute from the current node.

### EventTarget.removeEventListener()
Removes an event listener from the element.

### Element.requestFullscreen() 
Asynchronously asks the browser to make the element full-screen.

### Element.requestPointerLock() 
Allows to asynchronously ask for the pointer to be locked on the given element.

### Element.scroll()
Scrolls to a particular set of coordinates inside a given element.

### Element.scrollBy()
Scrolls an element by the given amount.

### Element.scrollIntoView() 
Scrolls the page until the element gets into the view.

### Element.scrollTo()
Scrolls to a particular set of coordinates inside a given element.

### Element.setAttribute()
Sets the value of a named attribute of the current node.

### Element.setAttributeNS()
Sets the value of the attribute with the specified name and namespace, from the current node.

### Element.setAttributeNode() 
Sets the node representation of the named attribute from the current node.

### Element.setAttributeNodeNS() 
Sets the node representation of the attribute with the specified name and namespace, from the current node.

### Element.setCapture() 
Sets up mouse event capture, redirecting all mouse events to this element.

### Element.setPointerCapture()
Designates a specific element as the capture target of future pointer events.

### Element.toggleAttribute()
Toggles a boolean attribute, removing it if it is present and adding it if it is not present, on the specified element.

## Examples

#### Enumerating elements attributes

```js
  function listAttributes() {
     const paragraph = document.getElementById("paragraph");
     const result = document.getElementById("result");

     // First, let's verify that the paragraph has some attributes    
     if (paragraph.hasAttributes()) {
       const attrs = paragraph.attributes;
       let output = "";
       for(var i = attrs.length - 1; i >= 0; i--) {
         output += `${attrs[i].name} -> ${attrs[i].value}`;
       }
       result.value = output;
     } else {
       result.value = "No attributes to show";
     }
   }
```

Try the code [here](https://jsfiddle.net/xc06y4ms/6/).

#### Remove all children of an element

```js
function removeAllChildren(element){
    element.innerHTML = '';
}
```

This method isn't recommended because it doesn't remove event handlers of child node. Hence, it might cause a memory leak if you are managing a big list of elements.

#### Classlist methods

```js
// <div class="anotherclass"></div>
console.log(div.outerHTML);

// if visible is set remove it, otherwise add it
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10 );

console.log(div.classList.contains("foo"));

// add or remove multiple classes
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// add or remove multiple classes using spread syntax
const cls = ["foo", "bar"];
div.classList.add(...cls); 
div.classList.remove(...cls);

// replace class "foo" with class "bar"
div.classList.replace("foo", "bar");
```

#### Get element relative position to other

```js
function getRelativePosition(elementA, elementB) {
  const elementAPosition = elementA.getBoundingClientRect();
  const elementBPosiotion = elementB.getBoundingClientRect();

  return {
    top: elementBPosiotion.top - elementAPosition.top,
    right: elementBPosiotion.right - elementAPosition.right,
    bottom: elementBPosiotion.bottom - elementAPosition.bottom,
    left: elementBPosiotion.left - elementAPosition.left,
  };
}
```

Try the code [here](https://jsfiddle.net/keLajq76/1/)

#### Insert an element after another

```js
refEle.parentNode.insertBefore(ele, refEle.nextSibling); // inherited from Node interface
```
Or
```js
refEle.insertAdjacentElement('afterend', ele);
```

#### Insert an element before another

```js
refEle.parentNode.insertBefore(ele, refEle); // inherited from Node interface
```

Or
```js
refEle.insertAdjacentElement('beforebegin', ele);
```

#### Insert html after an element

```js
ele.insertAdjacentHTML('afterend', html);
```

#### Insert html before the ele element:

```js
ele.insertAdjacentHTML('beforebegin', html);
```
