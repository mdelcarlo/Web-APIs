# Console
The Console API provides functionality to allow developers to perform debugging tasks, such as logging messages or the values of variables at set points in your code, or timing how long an operation takes to complete.

## Concepts and usage
The Console API started as a largely proprietary API, with different browsers implementing it, albeit it in inconsistent ways. The Console API spec was created to define consistent behavior, and all modern browsers eventually settled on implementing this behavior — although some implementations still have their own additional proprietary functions. 

Usage is very simple — the console object — available via window.console, or WorkerGlobalScope.console in workers; accessible using just console — contains many methods that you can call to perform rudimentary debugging tasks, generally focused around logging various values to the browser's Web Console.

## Methods

#### console.assert()
Log a message and stack trace to console if the first argument is false.
#### console.clear()
Clear the console.
#### console.count()
Log the number of times this line has been called with the given label.
#### console.countReset()
Resets the value of the counter with the given label.
#### console.debug()
Outputs a message to the console with the log level "debug".
#### console.dir()
Displays an interactive listing of the properties of a specified JavaScript object. This listing lets you use disclosure triangles to examine the contents of child objects.
#### console.dirxml()
Displays an XML/HTML Element representation of the specified object if possible or the JavaScript Object view if it is not possible.

#### console.error()
Outputs an error message. You may use string substitution and additional arguments with this method.
#### console.exception()  
An alias for error().
#### console.group()
Creates a new inline group, indenting all following output by another level. To move back out a level, call groupEnd().
#### console.groupCollapsed()
Creates a new inline group, indenting all following output by another level. However, unlike group() this starts with the inline group collapsed requiring the use of a disclosure button to expand it. To move back out a level, call groupEnd().
#### console.groupEnd()
Exits the current inline group.
#### console.info()
Informative logging of information. You may use string substitution and additional arguments with this method.
#### console.log()
For general output of logging information. You may use string substitution and additional arguments with this method.
#### console.profile() 
Starts the browser's built-in profiler (for example, the Firefox performance tool). You can specify an optional name for the profile.
#### console.profileEnd() 
Stops the profiler. You can see the resulting profile in the browser's performance tool (for example, the Firefox performance tool).
#### console.table()
Displays tabular data as a table.
#### console.time()
Starts a timer with a name specified as an input parameter. Up to 10,000 simultaneous timers can run on a given page.
#### console.timeEnd()
Stops the specified timer and logs the elapsed time in seconds since it started.
#### console.timeLog()
Logs the value of the specified timer to the console.
#### console.timeStamp() 
Adds a marker to the browser's Timeline or Waterfall tool.
#### console.trace()
Outputs a stack trace.
#### console.warn()
Outputs a warning message. You may use string substitution and additional arguments with this method.

## Examples

#### Using groups in the console
You can use nested groups to help organize your output by visually combining related material. To create a new nested block, call console.group(). The console.groupCollapsed() method is similar but creates the new block collapsed, requiring the use of a disclosure button to open it for reading.

To exit the current group, simply call console.groupEnd(). For example, given this code:
```js
console.log("This is the outer level");
console.group("First group");
console.log("In the first group");
console.group("Second group");
console.log("In the second group");
console.warn("Still in the second group");
console.groupEnd();
console.log("Back to the first group");
console.groupEnd();
console.debug("Back to the outer level");
```

#### Using Timers
You can start a timer to calculate the duration of a specific operation. To start one, call the console.time() method, giving it a name as the only parameter. To stop the timer, and to get the elapsed time in milliseconds, just call the console.timeEnd() method, again passing the timer's name as the parameter. Up to 10,000 timers can run simultaneously on a given page.

For example, given this code:
```js
console.time("answer time");
alert("Click to continue");
console.timeLog("answer time");
alert("Do a bunch of other stuff...");
console.timeEnd("answer time");
```

#### Output stack traces
The console object also supports outputting a stack trace; this will show you the call path taken to reach the point at which you call console.trace(). Given code like this:
```js
function foo() {
  function bar() {
    console.trace();
  }
  bar();
}

foo();
```