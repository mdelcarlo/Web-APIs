# Resize Observer
The Resize Observer API provides a performant mechanism by which code can monitor an element for changes to its size, with notifications being delivered to the observer each time the size changes.

# Usage
There are a whole raft of use cases for responsive design techniques (and others besides) that respond to changes in an element's size, but previously their implementations have often been hacky and/or brittle.

For example, media queries / window.matchMedia are great for updating layouts at specific points when the viewport changes sizes, but what it you want to change layout in response to a specific element's size changing, which isn't the outer container?

To achieve this, a limited solution would be to listen to changes to a suitable event that hints at the element you are interested in changing size (e.g. the window resize event), then figure out what the new dimensions or other features of the element after a resize using Element.getBoundingClientRect or Window.getComputedStyle, for example.

Such a solution tends to only work for limited use cases, be bad for performance (continually calling the above methods would result in a big performance hit), and often won't work when the browser window size is not changed.

The Resize Observer API provides a solution to exactly these kinds of problems, and more besides, allowing you to easily observe and respond to changes in the size of an element’s content or border box in a performant way. It provides a JavaScript solution to the often-discussed lack of element queries in the web platform.

Usage is simple, and pretty much the same as other observers, such as Performance Observer or Intersection Observer — you create a new ResizeObserver object using the ResizeObserver() constructor, then use ResizeObserver.observe() to make it look for changes to a specific element's size. A callback function set up inside the constructor then runs every time the size changes, providing access to the new dimensions and allowing you to do anything you like in response to those changes.

## Examples
#### Change the element background color on resize

```js
      const resizeObserver = new ResizeObserver(entries => {
        for (let entry of entries) {
          if (entry.contentBoxSize) {
            entry.target.style.backgroundColor = `rgba(${Math.min(255, (entry.contentBoxSize.inlineSize))}, 44,44,1)`;
          } else {
            entry.target.style.backgroundColor = `rgba(${Math.min(255, (entry.contentRect.width))}, 44,44,${Math.min(1, (entry.contentRect.width/400))})`;
          }
        }
      });

      resizeObserver.observe(document.querySelector('div'));

```
Try the code [here](https://jsfiddle.net/zo6w8rp7/5/).