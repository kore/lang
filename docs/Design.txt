===============
Language Design
===============

Goals
=====

The goal is to define a clean object oriented language which fulfills a set of
goals:

* Integration of functional concepts to verify if this works together with OOP
  and open the space for horizontal scalability

* Sane support for values / value objects

* Less boilerplate code

  * Constructors (field assignements), Setter, Getters are always the same.

Core principles
===============

* Structs ("Objects" with copy on write) (newables)

  * Are they allowed to define methods?

  * Are inline validations allowed?

  * Assign Validators to fields

  * How do we want to implement autoboxing (/ weak typing)?

* Scalar types

  * Work like structs, is there a differentiation required?

  * Weak typing (string to integer, …) MUST work somehow. Conversions of
    complex types chould work somehow alike.

* Entities

  * Entities are value objects with an ID. They should only occur once in an
    application and often mimic a remote state (database, web service, file
    system, …). Remote state is gloabl state and often managed by a central
    identity map. How can this be mapped to functional concepts?

* Classes ("Services")

  * Fields on defined dependencies, no scalar "properties" allowed

  * Fields are automatically initialized

    * If multiple implementations of a type exist (undefined auto-wiring
      resolution) we require dependency configuration, how should that look
      like?

    * Constructors / Destructors do NOT exist

  * Interfaces

    * Just as always

  * Abstract classes

    * Work just like interfaces, no concrete methods allowed

  * By now I do not see a real usecase for private / protected / package
    visibility any more … is this really needed? Some annotation which classes
    are the "public" interface would be required, though.

* Side effects

  * All side effects must be explicit (output, exceptions, global scope
    modifications).

    * In development mode side effects are allowed (debugging output), in
      production mode there will be "warnings".

  * Pure methods (functions) are preferred (they are distributable (accross
    threads, CPUs, machines, …))

  * Monads can help to pass side effects around without interfering with other
    execution paths. Monads should be first class language citizens.

* Asynchronous IO

  * Simple with pure functions. Wanted side effects / join points via messaging
    / promises?

Syntax
======

I could not care less, but we will need one…

Compilation Target
==================

What would be the best compilation target for such a language?

* Java Bytecode

* asm.js

* Erlang

* C

* …?

..
   Local Variables:
   mode: rst
   fill-column: 79
   End: 
   vim: et syn=rst tw=79
