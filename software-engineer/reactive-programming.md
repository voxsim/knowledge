## Observables
Observables are similar to arrays, except instead of being stored in memory, items arrive asynchronously over time (also called streams).
We can subscribe to observables and react to events emitted by them.

## Hot Observables
Hot observables will always push even if we're not specifically reacting to them with a subscription. For example resizing for a window.

## Cold Observables
A cold observable begins pushing only when we subscribe to it. If we subscribe again, it will start over.

## Observables Takeaways
Observables are streams. We can observe any stream: from resize events to existing arrays to API responses. We can create observables from almost anything. A promise is an observable with a single emitted value, but observables can return many values over time.

Reactive Programming

Reactive programming is concerned with propagating and responding to incoming events over time, declaratively (describing what to do rather than how).

Reactive Programming Takeaways

The reactive programming paradigm involves observing and reacting to events in asynchronous data streams. 
