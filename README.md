This is an MIT-licensed convenience library for the JavaScript
[pointer lock API](https://developer.mozilla.org/en-US/docs/WebAPI/Pointer_Lock).
It saves you having to write a bunch of redundant code to cover different
browsers and provides saner enter, exit, and error callbacks.

Most of the time it makes sense to use pointer lock in full screen, so you may
also want to check out [BigScreen](https://github.com/bdougherty/BigScreen), a
convenience library for making the browser window full-screen.

## Usage

 - `PL.requestPointerLock(element, onEnter, onExit, onError)` turns on
   pointer lock on the specified element (typically `document.body`). The
   callbacks have the specified element as `this` and receive the `event`
   object as their only parameter. If the `onError` event parameter is
   undefined, pointer lock is unsupported.
 - `PL.exitPointerLock(element)` cancels pointer lock on the specified element
   (typically `document.body`) if possible.
 - `PL.isSupported` is a boolean indicating whether pointer lock is supported.
   Note that `PL.requestPointerLock()` and `PL.exitPointerLock()` check this
   before attempting to do anything.
 - `PL.isEnabled()` returns a boolean indicating whether pointer lock is
   currently on.

In order to use pointer lock, a `mousemove` listener should be registered that
checks the `event.movementX` and `event.movementY` properties to see how far
the mouse would have moved if it wasn't locked. (This library also normalizes
the `movementX` and `movementY` properties which are otherwise inconsistent
across browsers.) For example:

    document.addEventListener('mousemove', function(event) {
     moveCamera(event.movementX, event.movementY);
    }, false);

## Browser compatibility

**Chrome:**
 - 16: full screen only, off by default (requires toggling a flag), no iframes
 - 21: supports all elements except iframes, off by default (requires toggling a flag)
 - 22: on by default, supports all elements except iframes
 - 23: on by default, supports all elements except that iframes must have the
   appropriate sandbox property, e.g.
   `<iframe sandbox="webkit-allow-pointer-lock ...">`

**Firefox;**
 - 15: full screen only
 - 22: supports all elements

Other browsers do not yet support the pointer lock API.