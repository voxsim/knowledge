# Law of demeter

How can i recognize this?
- Multiple dots
- Multiple assignments

It happens when we encode structural knowledge on how the system is wired togheter inside of our object. Please don't.

Example:
- A system have an object A, that calls B that calls C that calls D to have the hour => this.B().C().D().getHour() where this is A
- When C change in E; it brokes B and A and every class that call C for calling D for the hour.
- A right example is this.B().getHour(); that internally call this.C().getHour and so on.. this permits that every object has knowledge of the neighbour dependencies.
