# CSSStylesheet
The **CSSStyleSheet** interface represents a single CSS stylesheet, and lets you inspect and modify the list of rules contained in the stylesheet. It inherits properties and methods from its parent, StyleSheet.

A stylesheet consists of a collection of **CSSRule** objects representing each of the rules in the stylesheet. The rules are contained in a **CSSRuleList**, which can be obtained from the stylesheet's cssRules property.

For example, one rule might be a **CSSStyleRule** object containing a style such as:
```css
h1, h2 {
  font-size: 16pt;
}
```
Another rule might be an at-rule such as ```@import``` or ```@media```, and so forth.

## Properties
Inherits properties from its parent, StyleSheet.

#### cssRules | Read only
Returns a live CSSRuleList which maintains an up-to-date list of the CSSRule objects that comprise the stylesheet.

This is normally used to access individual rules like this:
```js
styleSheet.cssRules[i] // where i = 0..cssRules.length-1
```
To add or remove items in cssRules, use the CSSStyleSheet's insertRule() and deleteRule() methods.

#### ownerRule | Read only
If this stylesheet is imported into the document using an @import rule, the ownerRule property returns the corresponding CSSImportRule; otherwise, this property's value is null.
## Methods
Inherits methods from its parent, StyleSheet.

#### deleteRule()
Deletes the rule at the specified index into the stylesheet's rule list.
#### insertRule()
Inserts a new rule at the specified position in the stylesheet, given the textual representation of the rule.