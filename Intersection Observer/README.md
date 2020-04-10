# Intersection Observer
The **Intersection Observer API** provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.

Historically, detecting visibility of an element, or the relative visibility of two elements in relation to each other, has been a difficult task for which solutions have been unreliable and prone to causing the browser and the sites the user is accessing to become sluggish. As the web has matured, the need for this kind of information has grown. Intersection information is needed for many reasons, such as:

Lazy-loading of images or other content as a page is scrolled.
Implementing "infinite scrolling" web sites, where more and more content is loaded and rendered as you scroll, so that the user doesn't have to flip through pages.
Reporting of visibility of advertisements in order to calculate ad revenues.
Deciding whether or not to perform tasks or animation processes based on whether or not the user will see the result.

Implementing intersection detection in the past involved event handlers and loops calling methods like Element.getBoundingClientRect() to build up the needed information for every element affected. Since all this code runs on the main thread, even one of these can cause performance problems. When a site is loaded with these tests, things can get downright ugly.

The **Intersection Observer API** lets code register a callback function that is executed whenever an element they wish to monitor enters or exits another element (or the viewport), or when the amount by which the two intersect changes by a requested amount. This way, sites no longer need to do anything on the main thread to watch for this kind of element intersection, and the browser is free to optimize the management of intersections as it sees fit.

---

## Usage
The Intersection Observer API allows you to configure a callback that is called:

1) whenever one element, called the target, intersects either the device viewport or a specified element; for the purpose of this API, this is called the root element or root

2) and whenever the observer is asked to watch a target for the very first time

Typically, you'll want to watch for intersection changes with regard to the element's closest scrollable ancestor, or, if the element isn't a descendant of a scrollable element, the viewport. To watch for intersection relative to the root element, specify null.

### Creating an intersection observer
Create the intersection observer by calling its constructor and passing it a callback function to be run whenever a threshold is crossed in one direction or the other:

```js
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0
}

let observer = new IntersectionObserver(callback, options);
```
A threshold of 1.0 means that when 100% of the target is visible within the element specified by the root option, the callback is invoked.

#### Intersection observer options
The options object passed into the IntersectionObserver() constructor let you control the circumstances under which the observer's callback is invoked. It has the following fields:

##### root
The element that is used as the viewport for checking visibility of the target. Must be the ancestor of the target. Defaults to the browser viewport if not specified or if null.
##### rootMargin
Margin around the root. Can have values similar to the CSS margin property, e.g. "10px 20px 30px 40px" (top, right, bottom, left). The values can be percentages. This set of values serves to grow or shrink each side of the root element's bounding box before computing intersections. Defaults to all zeros.
##### threshold
Either a single number or an array of numbers which indicate at what percentage of the target's visibility the observer's callback should be executed. If you only want to detect when visibility passes the 50% mark, you can use a value of 0.5. If you want the callback to run every time visibility passes another 25%, you would specify the array [0, 0.25, 0.5, 0.75, 1]. The default is 0 (meaning as soon as even one pixel is visible, the callback will be run). A value of 1.0 means that the threshold isn't considered passed until every pixel is visible.

### Targeting an element to be observed
Once you have created the observer, you need to give it a target element to watch:
```js
let target = document.querySelector('#listItem');
observer.observe(target);

// the callback we setup for the observer will be executed now for the first time
// it waits until we assign a target to our observer (even if the target is currently not visible)
```
Whenever the target meets a threshold specified for the IntersectionObserver, the callback is invoked. The callback receives a list of IntersectionObserverEntry objects and the observer:
```js
let callback = (entries, observer) => {
  entries.forEach(entry => {
    // Each entry describes an intersection change for one observed
    // target element:
    //   entry.boundingClientRect
    //   entry.intersectionRatio
    //   entry.intersectionRect
    //   entry.isIntersecting
    //   entry.rootBounds
    //   entry.target
    //   entry.time
  });
};
```

## Examples

#### Modifiying box color with intersection observer API

[<img width="399" alt="Captura de Pantalla 2020-04-11 a la(s) 08 33 13" src="https://user-images.githubusercontent.com/20034230/79021259-235d8680-7bcf-11ea-9e78-bc8e66e9f2dd.png">](https://jsfiddle.net/ugwf2nLs/7/)
