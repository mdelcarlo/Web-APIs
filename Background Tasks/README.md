# Background Tasks
The Cooperative Scheduling of Background Tasks API (also referred to as the Background Tasks API or simply the requestIdleCallback() API) provides the ability to queue tasks to be executed automatically by the user agent when it determines that there is free time to do so.

## Concepts and usage
The main thread of a Web browser is centered around its event loop. This code draws any pending updates to the Document currently being displayed, runs any JavaScript code the page needs to run, accepts events from input devices, and dispatches those events to the elements that should receive them. In addition, the event loop handles interactions with the operating system, updates to the browser's own user interface, and so forth. It's an extremely busy chunk of code, and your main JavaScript code may run right inside this thread along with all of this. Certainly most if not all code that is capable of making changes to the DOM is running in the main thread, since it's common for user interface changes to only be available to the main thread.

Because event handling and screen updates are two of the most obvious ways users notice performance issues, it's important for your code to be a good citizen of the Web and help to prevent stalls in the execution of the event loop. In the past, there's been no way to do this reliably other than by writing code that's as efficient as possible and by offloading as much work as possible to workers. Window.requestIdleCallback() makes it possible to become actively engaged in helping to ensure that the browser's event loop runs smoothly, by allowing the browser to tell your code how much time it can safely use without causing the system to lag. If you stay within the limit given, you can make the user's experience much better.

### Getting the most out of idle callbacks
Because idle callbacks are intended to give your code a way to cooperate with the event loop to ensure that the system is utilized to its full potential without over-tasking it, resulting in lag or other performance problems, you should be thoughtful about how you go about using them.

- **Use idle callbacks for tasks which don't have high priority**. Because you don't know how many callbacks have been established, and you don't know how busy the user's system is, you don't know how often your callback will be run (unless you specify a timeout. There's no guarantee that every pass through the event loop (or even every screen update cycle) will include any idle callbacks being executed; if the event loop uses all available time, you're out of luck (again, unless you've used a timeout).
- **Idle callbacks should do their best not to overrun the time allotted**. While the browser, your code, and the Web in general will continue to run normally if you go over the specified time limit (even if you go way over it), the time restriction is intended to ensure that you leave the system enough time to finish the current pass through the event loop and get on to the next one without causing other code to stutter or animation effects to lag. Currently, timeRemaining() has an upper limit of 50 milliseconds, but in reality you will often have less time than that, since the event loop may already be eating into that time on complex sites, with browser extensions needing processor time, and so forth.
- **Avoid making changes to the DOM within your idle callback**. By the time your callback is run, the current frame has already finished drawing, and all layout updates and computations have been completed. If you make changes that affect layout, you may force a situation in which the browser has to stop and do recalculations that would otherwise be unnecessary. If your callback needs to change the DOM, it should use - **Window.requestAnimationFrame() to schedule that**.
Avoid tasks whose run time can't be predicted. Your idle callback should avoid doing anything that could take an unpredictable amount of time. For example, anything which might affect layout should be avoided. You should also avoid resolving or rejecting Promises, since that would invoke the handler for that promise's resolution or rejection as soon as your callback returns.
- **Use timeouts when you need to, but only when you need to**. Using timeouts can ensure that your code runs in a timely manner, but it can also allow you to cause lag or animation stutters by mandating that the browser call you when there's not enough time left for you to run without disrupting performance.

## Interfaces
The Background Tasks API adds only one new interface:

### IdleDeadline
An object of this type is passed to the idle callback to provide an estimate of how long the idle period is expected to last, as well as whether or not the callback is running because its timeout period has expired.

The **Window** interface is also augmented by this API to offer the new `requestIdleCallback()` and `cancelIdleCallback()` methods.

- `requestIdleCallback()` method queues a function to be called during a browser's idle periods. This enables developers to perform background and low priority work on the main event loop, without impacting latency-critical events such as animation and input response. Functions are generally called in first-in-first-out order; however, callbacks which have a timeout specified may be called out-of-order if necessary in order to run them before the timeout elapses.

- `cancelIdleCallback()` method cancels a callback previously scheduled with window.requestIdleCallback().
   