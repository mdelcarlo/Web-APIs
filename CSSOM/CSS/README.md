# CSS 

The CSS interface is a utility interface and no object of this type can be created: only static properties are defined on it.
Methods
The CSS interface is a utility interface and no object of this type can be created: only static methods are defined on it.

## Static methods
No inherited static methods.

#### CSS.registerProperty()
Registers custom properties, allowing for property type checking, default values, and properties that do or do not inherit their value.
#### CSS.supports()
Returns a Boolean indicating if the pair property-value, or the condition, given in parameter is supported.
#### CSS.escape()
Can be used to escape a string mostly for use as part of a CSS selector.
#### CSS factory functions
Can be used to return a new CSSUnitValue with a value of the parameter number of the units of the name of the factory function method used.

```js
CSS.number(number);
CSS.percent(number);

// <length>
CSS.em(number);
CSS.ex(number);
CSS.ch(number);
CSS.ic(number);
CSS.rem(number);
CSS.lh(number);
CSS.rlh(number);
CSS.vw(number);
CSS.vh(number);
CSS.vi(number);
CSS.vb(number);
CSS.vmin(number);
CSS.vmax(number);
CSS.cm(number);
CSS.mm(number);
CSS.Q(number);
CSS.in(number);
CSS.pt(number);
CSS.pc(number);
CSS.px(number);

// <angle>
CSS.deg(number);
CSS.grad(number);
CSS.rad(number);
CSS.turn(number);

// <time>
CSS.s(number);
CSS.ms(number);

// <frequency>
CSS.Hz(number);
CSS.kHz(number);

// <resolution>
CSS.dpi(number);
CSS.dpcm(number);
CSS.dppx(number);

// <flex>
CSS.fr(number);
```

For example:
```js
CSS.em(3) // CSSUnitValue {value: 3, unit: "em"}
```