## Ubiquitous Language
A ubiquitous language is a shared set of concepts, terms and definitions between the business stakeholders and the technical staff.
We can use the language to drive the design of the system.

## Bounded Context
* Concretely: A software system
* Linguistically: a delineation in your domain where concepts are "bounded", contained
Each *Domain* should have its own *Bounded Context*
A Bounded Context can have multiple subdomains and its own event handler.

## Context Map
?

## Aggregate Root
An aggregate root are top-level domain models that reveal an object graph of related entities beneath them.
Each domain can and only exposes multiple aggregate roots via:
* Direct method calls
* JSON payloads
* API endpoint

## Anti Corruption Layer
The *Anti Corruption Layer* is an adapter that maps an external concept to our internal concept

More detail:
- Read Domain Driven Design distilled
- Read Domain Driven ecc..

- https://www.youtube.com/watch?v=sFCgXH7DwxM
