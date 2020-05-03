# Pointer Lock

The Pointer Lock API (formerly called Mouse Lock API) provides input methods based on the movement of the mouse over time (i.e., deltas), not just the absolute position of the mouse cursor in the viewport. It gives you access to raw mouse movement, locks the target of mouse events to a single element, eliminates limits on how far mouse movement can go in a single direction, and removes the cursor from view. It is ideal for first person 3D games, for example.

More than that, the API is useful for any applications that require significant mouse input to control movements, rotate objects, and change entries, for example allowing users to control the viewing angle simply by moving the mouse around without any button clicking. The buttons are then freed up for other actions. Other examples include apps for viewing maps or satellite imagery.

Pointer lock lets you access mouse events even when the cursor goes past the boundary of the browser or screen. For example, your users can continue to rotate or manipulate a 3D model by moving the mouse without end. Without Pointer lock, the rotation or manipulation stops the moment the pointer reaches the edge of the browser or screen. Game players can now click buttons and swipe the mouse cursor back and forth without worrying about leaving the game play area and accidentally clicking another application that would take mouse focus away from the game.

## Basic concepts

Pointer lock is related to mouse capture. Mouse capture provides continued delivery of events to a target element while a mouse is being dragged, but it stops when the mouse button is released. Pointer lock is different from mouse capture in the following ways:

It is persistent: Pointer lock does not release the mouse until an explicit API call is made or the user uses a specific release gesture.
It is not limited by browser or screen boundaries.
It continues to send events regardless of mouse button state.
It hides the cursor.

## Method/properties overview

This section provides a brief description of each property and method related to the pointer lock specification.

#### requestPointerLock()

The Pointer lock API, similar to the Fullscreen API, extends DOM elements by adding a new method, requestPointerLock(). As it has recently unprefixed, you would currently declare it something like this, for example if you wanted to request pointer lock on a canvas element:

```js
canvas.requestPointerLock =
  canvas.requestPointerLock || canvas.mozRequestPointerLock;

canvas.requestPointerLock();
```

#### pointerLockElement and exitPointerLock()

The Pointer lock API also extends the Document interface, adding both a new property and a new method. The new property is used for accessing the currently locked element (if any), and is named pointerLockElement and the new method on Document is exitPointerLock() and, as the name implies, it is used to exit the pointer lock.

The pointerLockElement property is useful for determining if any element is currently pointer locked (e.g., for doing a Boolean check) and also for obtaining a reference to the locked element, if any.

Here is an example of using pointerLockElement:

```js
if (
  document.pointerLockElement === canvas ||
  document.mozPointerLockElement === canvas
) {
  console.log("The pointer lock status is now locked");
} else {
  console.log("The pointer lock status is now unlocked");
}
```

The Document.exitPointerLock() method is used to exit pointer lock, and like requestPointerLock, works asynchronously using the pointerlockchange and pointerlockerror events, which you'll see more about below.

```js
document.exitPointerLock =
  document.exitPointerLock || document.mozExitPointerLock;

// Attempt to unlock
document.exitPointerLock();
```

#### pointerlockchange event

When the Pointer lock state changes—for example, when calling requestPointerLock(), exitPointerLock(), the user pressing the ESC key, etc.—the pointerlockchange event is dispatched to the document. This is a simple event and contains no extra data.

```js
if ("onpointerlockchange" in document) {
  document.addEventListener("pointerlockchange", lockChangeAlert, false);
} else if ("onmozpointerlockchange" in document) {
  document.addEventListener("mozpointerlockchange", lockChangeAlert, false);
}

function lockChangeAlert() {
  if (
    document.pointerLockElement === canvas ||
    document.mozPointerLockElement === canvas
  ) {
    console.log("The pointer lock status is now locked");
    // Do something useful in response
  } else {
    console.log("The pointer lock status is now unlocked");
    // Do something useful in response
  }
}
```

#### pointerlockerror event

When there is an error caused by calling requestPointerLock() or exitPointerLock(), the pointerlockerror event is dispatched to the document. This is a simple event and contains no extra data.

````js
document.addEventListener('pointerlockerror', lockError, false);
document.addEventListener('mozpointerlockerror', lockError, false);

function lockError(e) {
  alert("Pointer lock failed");
}
```
````
