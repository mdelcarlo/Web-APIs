# Performance
The High Resolution Time standard defines a Performance interface that supports client-side latency measurements within applications. The Performance interfaces are considered high resolution because they are accurate to a thousandth of a millisecond (subject to hardware or software constraints). The interfaces support a number of use cases including calculating frame-rates (potentially important in animations) and benchmarking (such as the time to load a resource).

Since a platform's system clock is subject to various skews (such as NTP adjustments), the interfaces support a monotonic clock i.e. a clock that is always increasing. As such, the Performance API defines a DOMHighResTimeStamp type rather than using the Date.now() interface.

## Properties
The Performance interface has two properties. The **timing** property returns a `PerformanceTiming` object containing latency-related performance information such as the start of navigation time, start and end times for redirects, start and end times for responses, etc.

The *navigation* property returns a `PerformanceNavigation` object representing the type of navigation that occurs in the given browsing context, such as the page was navigated to from history, the page was navigated to by following a link, etc.

## Interfaces
`Performance`
Provides methods and properties containing timing-related performance information for the given page.
`PerformanceEntry`
Provides methods and properties the encapsulate a single performance metric that is part of the performance timeline.
`PerformanceFrameTiming`
Provides methods and properties containing frame timing data about the browser's event loop.
`PerformanceMark`
An abstract interface for performance entries with an entry type of "mark". Entries of this type are created by calling performance.mark() to add a named DOMHighResTimeStamp (the mark) to the browser's performance timeline.
`PerformanceMeasure`
An abstract interface for performance entries with an entry type of "measure". Entries of this type are created by calling performance.measure() to add a namedDOMHighResTimeStamp (the measure) between two marks to the browser's performance timeline.
`PerformanceNavigationTiming`
Provides methods and properties to store and retrieve high resolution timestamps or metrics regarding the browser's document navigation events.
`PerformanceObserver`
Provides methods and properties used to observe performance measurement events and be notified of new performance entries as they are recorded in the browser's performance timeline.

[`PerformanceResourceTiming`](./PerformanceResourceTiming/README.md)
Provides methods and properties for retrieving and analyzing detailed network timing data regarding the loading of an application's resources.