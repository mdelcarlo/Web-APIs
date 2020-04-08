# Document
The **Document** interface represents any web page loaded in the browser and serves as an entry point into the web page's content, which is the DOM tree. The DOM tree includes elements such as ```<body>``` and ```<table>```, among many others. It provides functionality globally to the document, like how to obtain the page's URL and create new elements in the document.

<img width="370" alt="Captura de Pantalla 2020-04-09 a la(s) 07 53 55" src="https://user-images.githubusercontent.com/20034230/78827523-59680280-7a37-11ea-8d43-0b6151e313cd.png">

The Document interface describes the common properties and methods for any kind of document. Depending on the document's type (e.g. HTML, XML, SVG, …), a larger API is available: HTML documents, served with the "text/html" content type, also implement the HTMLDocument interface, whereas XML and SVG documents implement the XMLDocument interface.

---

## Constructor
Document()
Creates a new Document object.

---

## Properties
This interface also inherits from the Node and EventTarget interfaces.

#### Document.anchors | Read only
Returns a list of all of the anchors in the document.
#### Document.body
Returns the ```<body>``` or ```<frameset>``` node of the current document.
#### Document.characterSet | Read only
Returns the character set being used by the document.
#### Document.compatMode  | Read only
Indicates whether the document is rendered in quirks or strict mode.
#### Document.contentType  | Read only
Returns the Content-Type from the MIME Header of the current document.
#### Document.doctype | Read only
Returns the Document Type Definition (DTD) of the current document.
#### Document.documentElement | Read only
Returns the Element that is a direct child of the document. For HTML documents, this is normally the HTMLHtmlElement object representing the document's <html> element.
#### Document.documentURI | Read only
Returns the document location as a string.
#### Document.embeds | Read only
Returns a list of the embedded ```<embed>``` elements within the current document.
#### Document.fonts
Returns the FontFaceSet interface of the current document.
#### Document.forms | Read only
Returns a list of the ```<form>``` elements within the current document.
#### Document.head | Read only
Returns the <head> element of the current document.
#### Document.hidden | Read only
Returns a Boolean value indicating if the page is considered hidden or not.
#### Document.images | Read only
Returns a list of the images in the current document.
#### Document.implementation | Read only
Returns the DOM implementation associated with the current document.
#### Document.lastStyleSheetSet | Read only
Returns the name of the style sheet set that was last enabled. Has the value null until the style sheet is changed by setting the value of selectedStyleSheetSet.
#### Document.links | Read only
Returns a list of all the hyperlinks in the document.
#### Document.mozSyntheticDocument 
Returns a Boolean that is true only if this document is synthetic, such as a standalone image, video, audio file, or the like.
#### Document.plugins | Read only
Returns a list of the available plugins.
#### Document.featurePolicy  | Read only
Returns the FeaturePolicy interface which provides a simple API for introspecting the feature policies applied to a specific document.
#### Document.preferredStyleSheetSet | Read only
Returns the preferred style sheet set as specified by the page author.
#### Document.scripts | Read only
Returns all the ```<script>```elements on the document.
#### Document.scrollingElement | Read only
Returns a reference to the Element that scrolls the document.
#### Document.selectedStyleSheetSet
Returns which style sheet set is currently in use.
#### Document.styleSheetSets | Read only
Returns a list of the style sheet sets available on the document.
#### Document.timeline | Read only
Returns timeline as a special instance of DocumentTimeline that is automatically created on page load.

#### Document.visibilityState | Read only
Returns a string denoting the visibility state of the document. Possible values are visible, hidden, prerender, and unloaded.
The Document interface is extended with the ParentNode interface:

#### ParentNode.childElementCount  | Read only
Returns the number of children of this ParentNode which are elements.
#### ParentNode.children  | Read only
Returns a live HTMLCollection containing all of the Element objects that are children of this ParentNode, omitting all of its non-element nodes.
#### ParentNode.firstElementChild  | Read only
Returns the first node which is both a child of this ParentNode and is also an Element, or null if there is none.
#### ParentNode.lastElementChild  | Read only
Returns the last node which is both a child of this ParentNode and is an Element, or null if there is none.

### Extensions for HTMLDocument
The Document interface for HTML documents inherits from the HTMLDocument interface or, since HTML5, is extended for such documents.

#### Document.cookie
Returns a semicolon-separated list of the cookies for that document or sets a single cookie.
#### Document.defaultView | Read only
Returns a reference to the window object.
#### Document.designMode
Gets/sets the ability to edit the whole document.
#### Document.dir | Read only
Gets/sets directionality (rtl/ltr) of the document.
#### Document.domain
Gets/sets the domain of the current document.
#### Document.lastModified | Read only
Returns the date on which the document was last modified.
#### Document.location | Read only
Returns the URI of the current document.
#### Document.readyState | Read only
Returns loading status of the document.
#### Document.referrer | Read only
Returns the URI of the page that linked to this page.
#### Document.title
Sets or gets the title of the current document.
#### Document.URL | Read only
Returns the document location as a string.

### Properties included from DocumentOrShadowRoot
The Document interface includes the following properties defined on the DocumentOrShadowRoot mixin. Note that this is currently only implemented by Chrome; other browsers still implement them directly on the Document interface.

#### DocumentOrShadowRoot.activeElement | Read only
Returns the Element within the shadow tree that has focus.
#### Document.fullscreenElement | Read only
The element that's currently in full screen mode for this document.
#### DocumentOrShadowRoot.pointerLockElement  | Read only
Returns the element set as the target for mouse events while the pointer is locked. null if lock is pending, pointer is unlocked, or if the target is in another document.
#### DocumentOrShadowRoot.styleSheets | Read only
Returns a StyleSheetList of CSSStyleSheet objects for stylesheets explicitly linked into, or embedded in a document.

### Event handlers
#### Document.onafterscriptexecute 
Represents the event handling code for the afterscriptexecute event.
#### Document.onbeforescriptexecute 
Represents the event handling code for the beforescriptexecute event.
#### Document.oncopy 
Represents the event handling code for the copy event.
#### Document.oncut 
Represents the event handling code for the cut event.
#### Document.onfullscreenchange
Is an EventHandler representing the code to be called when the fullscreenchange event is raised.
#### Document.onfullscreenerror
Is an EventHandler representing the code to be called when the fullscreenerror event is raised.
#### Document.onpaste 
Represents the event handling code for the paste event.
#### Document.onreadystatechange
Represents the event handling code for the readystatechange event.
#### Document.onselectionchange 
Is an EventHandler representing the code to be called when the selectionchange event is raised.
#### Document.onvisibilitychange
Is an EventHandler representing the code to be called when the visibilitychange event is raised.

---

## Methods
This interface also inherits from the [Node](./../Node/Readme.md) and [EventTarget](./../EventTarget/Readme.md) interfaces.

#### Document.adoptNode()
Adopt node from an external document.
#### Document.captureEvents() 
See Window.captureEvents.
#### Document.caretRangeFromPoint() 
Gets a Range object for the document fragment under the specified coordinates.
#### Document.createAttribute()
Creates a new Attr object and returns it.
#### Document.createAttributeNS()
Creates a new attribute node in a given namespace and returns it.
#### Document.createCDATASection()
Creates a new CDATA node and returns it.
#### Document.createComment()
Creates a new comment node and returns it.
#### Document.createDocumentFragment()
Creates a new document fragment.
#### Document.createElement()
Creates a new element with the given tag name.
#### Document.createElementNS()
Creates a new element with the given tag name and namespace URI.
#### Document.createEntityReference() 
Creates a new entity reference object and returns it.
#### Document.createEvent()
Creates an event object.
#### Document.createNodeIterator()
Creates a NodeIterator object.
#### Document.createProcessingInstruction()
Creates a new ProcessingInstruction object.
#### Document.createRange()
Creates a Range object.
#### Document.createTextNode()
Creates a text node.
#### Document.createTouch() 
Creates a Touch object.
#### Document.createTouchList()
Creates a TouchList object.
#### Document.createTreeWalker()
Creates a TreeWalker object.
#### Document.enableStyleSheetsForSet()
Enables the style sheets for the specified style sheet set.
#### Document.exitPointerLock() 
Release the pointer lock.
#### Document.getAnimations() 
Returns an array of all Animation objects currently in effect, whose target elements are descendants of the document.
#### Document.getElementsByClassName()
Returns a list of elements with the given class name.
#### Document.getElementsByTagName()
Returns a list of elements with the given tag name.
#### Document.getElementsByTagNameNS()
Returns a list of elements with the given tag name and namespace.
#### Document.hasStorageAccess()
Returns a Promise that resolves with a boolean value indicating whether the document has access to its first-party storage.
#### Document.importNode()
Returns a clone of a node from an external document.
#### Document.normalizeDocument() 
Replaces entities, normalizes text nodes, etc.
#### Document.releaseCapture() 
Releases the current mouse capture if it's on an element in this document.
#### Document.releaseEvents()  
See Window.releaseEvents().
#### Document.requestStorageAccess()
Returns a Promise that resolves if the access to first-party storage was granted, and rejects if access was denied.
#### Document.routeEvent()  Obsolete since Gecko 24
See Window.routeEvent().
#### Document.mozSetImageElement() 
Allows you to change the element being used as the background image for a specified element ID.
The Document interface is extended with the ParentNode interface:

#### Document.getElementById(String id)
Returns an object reference to the identified element.
#### Document.querySelector()
Returns the first Element node within the document, in document order, that matches the specified selectors.
#### Document.querySelectorAll()
Returns a list of all the Element nodes within the document that match the specified selectors.
The Document interface is extended with the XPathEvaluator interface:

#### Document.createExpression()
Compiles an XPathExpression which can then be used for (repeated) evaluations.
#### Document.createNSResolver()
Creates an XPathNSResolver object.
#### Document.evaluate()
Evaluates an XPath expression.

### Extension for HTML documents
The Document interface for HTML documents inherit from the HTMLDocument interface or, since HTML5, is extended for such documents:

#### Document.clear()  
In majority of modern browsers, including recent versions of Firefox and Internet Explorer, this method does nothing.
#### Document.close()
Closes a document stream for writing.
#### Document.execCommand()
On an editable document, executes a formating command.
#### Document.getElementsByName()
Returns a list of elements with the given name.
#### Document.hasFocus()
Returns true if the focus is currently located anywhere inside the specified document.
#### Document.open()
Opens a document stream for writing.
#### Document.queryCommandEnabled()
Returns true if the formating command can be executed on the current range.
#### Document.queryCommandIndeterm()
Returns true if the formating command is in an indeterminate state on the current range.
#### Document.queryCommandState()
Returns true if the formating command has been executed on the current range.
#### Document.queryCommandSupported()
Returns true if the formating command is supported on the current range.
#### Document.queryCommandValue()
Returns the current value of the current range for a formating command.
#### Document.write()
Writes text in a document.
#### Document.writeln()
Writes a line of text in a document.
Methods included from DocumentOrShadowRoot
The Document interface includes the following methods defined on the DocumentOrShadowRoot mixin. Note that this is currently only implemented by Chrome; other browsers still implement them on the Document interface.

#### DocumentOrShadowRoot.getSelection()
Returns a Selection object representing the range of text selected by the user, or the current position of the caret.
#### DocumentOrShadowRoot.elementFromPoint()
Returns the topmost element at the specified coordinates.
#### DocumentOrShadowRoot.elementsFromPoint()
Returns an array of all elements at the specified coordinates.
#### DocumentOrShadowRoot.caretPositionFromPoint()
Returns a CaretPosition object containing the DOM node containing the caret, and caret's character offset within that node.

### Example
#### Adopt a node from an iframe
```js
const iframe = document.querySelector('iframe');
const iframeImages = iframe.contentDocument.querySelectorAll('img');
const newParent = document.getElementById('images');

iframeImages.forEach(function(imgEl) {
  newParent.appendChild(document.adoptNode(imgEl));
});
```

#### Use DocumentFragment to avoid page reflow (computation of element's position and geometry), resulting in better performance.

```js
var element  = document.getElementById('ul'); // assuming ul exists
var fragment = document.createDocumentFragment();
var browsers = ['Firefox', 'Chrome', 'Opera', 
    'Safari', 'Internet Explorer'];

browsers.forEach(function(browser) {
    var li = document.createElement('li');
    li.textContent = browser;
    fragment.appendChild(li);
});

element.appendChild(fragment);
```

### Slow down all animations on a page

```js
document.getAnimations().forEach(
  function (animation) {
    animation.playbackRate *= .5;
  }
);
```

### Do stuff when Dom content is loaded

```js
function doStuff() {
  console.info('DOM loaded');
}

if (document.readyState === 'loading') {  // Loading hasn't finished yet
  document.addEventListener('DOMContentLoaded', doStuff);
} else {  // `DOMContentLoaded` has already fired
  doStuff();
}
```