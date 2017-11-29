# Event Sourcing

Event Sourcing ensures that all changes to application state are stored as a sequence of events. Not just can we query these events, we can also use the event log to reconstruct past states, and as a foundation to automatically adjust the state to cope with retroactive changes.

## How it Works

The fundamental idea of Event Sourcing is that of ensuring every change to the state of an application is captured in an event object, and that these event objects are themselves stored in the sequence they were applied for the same lifetime as the application state itself.

Let's consider a simple example to do with shipping notifications. In this example we have many ships on the high seas, and we need to know where they are. A simple way to do this is to have a tracking application with methods to allow us to tell when a ship arrives or leaves at a port.

![](https://martinfowler.com/eaaDev/eventSourcing/simpleService.gif)

Figure 1: A simple interface for tracking shipping movements.

In this case when the service is called, it finds the relevant ship and updates its location. The ship objects record the current known state of the ships.

Introducing Event Sourcing adds a step to this process. Now the service creates an event object to record the change and processes it to update the ship.

![](https://martinfowler.com/eaaDev/eventSourcing/simpleEventCd.gif)

Figure 2: Using an event to capture the change.

Looking at just the processing, this is just an unnecessary level of indirection. The interesting difference is when we look at what persists in the application after a few changes. Let's imagine some simple changes:

* The Ship 'King Roy' departs San Francisco
* The Ship 'Prince Trevor' arrives at Los Angeles
* The Ship 'King Roy' arrives in Hong Kong

With the basic service, we see just the final state captured by the ship objects. I'll refer to this as the application state.

![](https://martinfowler.com/eaaDev/eventSourcing/simpleServiceHis.gif)

Figure 3: State after a few movements tracked by simple tracker.

With Event Sourcing we also capture each event. If we are using a persistent store the events will be persisted just the same as the ship objects are. I find it useful to say that we are persisting two different things an application state and an event log.

![](https://martinfowler.com/eaaDev/eventSourcing/simpleEventHis.gif)

Figure 4: State after a few movements tracked by event sourced tracker.

The most obvious thing we've gained by using Event Sourcing is that we now have a log of all the changes. Not just can we see where each ship is, we can see where it's been. However this is a small gain. We could also do this by keeping a history of past ports in the ship object, or by writing to a log file whenever a ship moves. Both of these can give us an adequate history.

The key to Event Sourcing is that we guarantee that all changes to the domain objects are initiated by the event objects. This leads to a number of facilities that can be built on top of the event log:

* Complete Rebuild: We can discard the application state completely and rebuild it by re-running the events from the event log on an empty application.
* Temporal Query: We can determine the application state at any point in time. Notionally we do this by starting with a blank state and rerunning the events up to a particular time or event. We can take this further by considering multiple time-lines (analogous to branching in a version control system).
* Event Replay: If we find a past event was incorrect, we can compute the consequences by reversing it and later events and then replaying the new event and later events. (Or indeed by throwing away the application state and replaying all events with the correct event in sequence.) The same technique can handle events received in the wrong sequence - a common problem with systems that communicate with asynchronous messaging.

A common example of an application that uses Event Sourcing is a version control system. Such a system uses temporal queries quite often. Subversion uses complete rebuilds whenever you use dump and restore to move stuff between repository files. I'm not aware of any that do event replay since they are not particularly interested in that information. Enterprise applications that use Event Sourcing are rarer, but I have seen a few applications (or parts of applications) that use it.
