# FontFace 
The FontFace interface represents a single usable font face. It allows control of the source of the font face, being a URL to an external resource, or a buffer; it also allows control of when the font face is loaded and its current status.

## Constructor
#### FontFace()
Constructs and returns a new FontFace object, built from an external resource described by an URL or from an ArrayBuffer.

## Properties
This interface doesn't inherit any property.

#### FontFace.display
A CSSOMString that determines how a font face is displayed based on whether and when it is downloaded and ready to use.
#### FontFace.family
A CSSOMString that retrieves or sets the family of the font. It is equivalent to the font-family descriptor.
#### FontFace.featureSettings
A CSSOMString that retrieves or sets infrequently used font features that are not available from a font's variant properties. It is equivalent to the font-feature-settings descriptor.
#### FontFace.loaded Read only
Returns a Promise that resolves with the current FontFace object when the font specified in the object's constructor is done loading or rejects with a SyntaxError.
#### FontFace.status Read only
Returns an enumerated value indicating the status of the font, one of  "unloaded", "loading", "loaded", or "error".
#### FontFace.stretch
A CSSOMString that retrieves or sets how the font stretches. It is equivalent to the font-stretch descriptor.
#### FontFace.style
A CSSOMString that retrieves or sets the style of the font. It is equivalent to the font-style descriptor.
#### FontFace.unicodeRange
A CSSOMString that retrieves or sets the range of unicode codepoints encompassing the font. It is equivalent to the unicode-range descriptor.
#### FontFace.variant
A CSSOMString that retrieves or sets the variant of the font. It is equivalent to the font-variant descriptor.
#### FontFace.weight
A CSSOMString that contains the weight of the font. It is equivalent to the font-weight descriptor.

## Methods
This interface doesn't inherit any method.

#### FontFace.load()
Loads a font based on current object's constructor-passed requirements, including a location or source buffer, and returns a Promise that resolves with the current FontFace object.