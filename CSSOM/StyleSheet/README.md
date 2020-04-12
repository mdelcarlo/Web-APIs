# Stylesheet
An object implementing the **StyleSheet** interface represents a single style sheet. CSS style sheets will further implement the more specialized **CSSStyleSheet** interface.

## Properties
#### StyleSheet.disabled
Is a Boolean representing whether the current stylesheet has been applied or not.
#### StyleSheet.href | Read only
Returns a DOMString representing the location of the stylesheet.
#### StyleSheet.media | Read only
Returns a MediaList representing the intended destination medium for style information.
#### StyleSheet.ownerNode | Read only
Returns a Node associating this style sheet with the current document.
#### StyleSheet.parentStyleSheet | Read only
Returns a StyleSheet including this one, if any; returns null if there aren't any.
#### StyleSheet.title | Read only
Returns a DOMString representing the advisory title of the current style sheet.
#### StyleSheet.typeRead only
Returns a DOMString representing the style sheet language for this style sheet.

## Example
```html
 // on a local machine: 
 <html> 
  <head> 
   <link rel="StyleSheet" href="example.css" type="text/css" /> 
   <script> 
    function sref() { 
     alert(document.styleSheets[0].href); 
    }
   </script> 
  </head> 
  <body> 
   <div class="thunder">Thunder</div>
   <button onclick="sref()">ss</button>
  </body> 
 </html>
// returns "file:////C:/Windows/Desktop/example.css

```