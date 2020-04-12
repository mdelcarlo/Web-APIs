# CSSRule

The CSSRule interface represents a single CSS rule. There are several types of rules, listed in the Type constants section below.

The CSSRule interface specifies the properties common to all rules, while properties unique to specific rule types are specified in the more specialized interfaces for those rules' respective types.

References to a CSSRule may be obtained by looking at a CSSStyleSheet's cssRules list.

## Properties
#### CSSRule.cssText
Represents the textual representation of the rule, e.g. "h1,h2 { font-size: 16pt }" or "@import 'url'". To access or modify parts of the rule (e.g. the value of "font-size" in the example) use the properties on the specialized interface for the rule's type.
#### CSSRule.parentRule Read only
Returns the containing rule, otherwise null. E.g. if this rule is a style rule inside an @media block, the parent rule would be that CSSMediaRule.
#### CSSRule.parentStyleSheet Read only
Returns the CSSStyleSheet object for the style sheet that contains this rule
#### CSSRule.type Read only
One of the Type constants indicating the type of CSS rule.


## Examples

#### Log first cssRule from first stylesheet

```js
  var stylesheet = document.styleSheets[0];
  console.log(stylesheet.cssRules[0].cssText);
  ```