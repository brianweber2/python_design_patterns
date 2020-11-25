# Python Design Patterns
Examples of common design patterns using Python.

**Gamma Categorization**
* Design patterns are typically split into three categories.
* This is called *Gamma Categorization* after Enrich Gamma.

1. **Creational Patterns**
    * Deal with the creation (construction) of objects
    * Explicit (constructor) vs. implicit (DI, reflection, etc.)
    * Wholesale (single statement) vs. piecewise (step-by-step)
2. **Structural Patterns**
    * Concerned with the structure (e.g., class members)
    * Many patterns are wrappers that mimic the underlying class' interface
    * Stress the importance of good API design
3. **Behavioral Patterns**
    * They are all different; no central theme

## SOLID Design Principles
Design principles introduced by Robert C. Martim, aka *Uncle Bob*.

### Single Responsibility Principle (SRP)
If you have a class or function, it should only take on one responsibility.

### Open-Closed Principle (OCP)
"Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"; that is, such an entity can allow its behaviour to be extended without modifying its source code.

### Liskov Substitution Principle (LSP)
If you have an interface that takes some sort of base class, you should be able to stick a derived class in there and everything should work. 

### Interface Segregation Principle
States that no client should be forced to depend on methods it does not use. ISP splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them.

### Dependency Inversion Principle
Is a specific form of decoupling software modules.
* High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces).
* Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

## Builder
**Motivation**
* Some objects are simple and can be created in a single initializer call
* Other objects require a lot of ceremony to create
* Having an object with 10 initializer arguments is not productive
* Instead, opt for piecewise construction
* Builder provides an API for constructing an object step-by-step

### Builder
Is required when you have a complicated way of constructing an object like HTML elements.

### Builder Facets
Used when your object requires more than one builder to build your object.

### Builder Inheritance
When needing to build up an object, you can inherit from another builder object.

## Factories
A Factory is a component responsible solely for the wholesale (not piecewise) creation of objects.

**Motivation**
* Object creation logic becomes too convoluted
* Initializer is not descriptive
    * Name is always *__init__*
    * Cannot overload with same sets of arguments with different names
    * Can turn into 'optional parameter hell'
* Wholesale object creation (non-piecewise, unlike Builder) can be outsourced to
    * A separate method (Factory Method)
    * That may exist in a separate class (Factory)
    * Can create hierarchy of factories with Abstract Factory

### Factory Method
The factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

### Factory
In Factory pattern, we create object without exposing the creation logic to the client and refer to newly created object using a common interface.

### Abstract Factory
The abstract factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes.

## Prototype
When it's easier to copy an existing object to fully initialize a new one.

**Motivation**
* Complicated objects (e.g., cars) aren't designed from scratch
    * They reiterate existing designs
* An existing (partially or fully constructed) design is a Prototype
* We make a copy (clone) of the prototype and customize it
    * Requires `deepy copy` support.
* We make the cloning convenient (e.g., via a Factory)

### Prototype
Prototype pattern refers to creating duplicate object while keeping performance in mind. This pattern involves implementing a prototype interface which tells to create a clone of the current object. This pattern is used when creation of object directly is costly. For example, an object is to be created after a costly database operation. We can cache the object, returns its clone on next request and update the database as and when needed thus reducing database calls.

### Prototype Factory
Takes an existing Prototype object and creates a new object with updated values.

## Singleton
A design pattern that everyone loves to hate!

**Motivation**
* For some components it only makes sense to have one in the system
    * Database repository
    * Object factory
* E.g., the initializer call is expensive
    * We only do it once
    * We provide everyone with the same instance
* Want to prevent anyone creating additional copies
* Need to take care of lazy instantiation

### Singleton Allocator
Not the recommended way.

### Singleton Decorator
Uses Python decorator to enforce an object to only be loaded once.

### Singleton Metaclass
Only need to specify `metaclass` with singleton class when creating singleton objects.

### Monostate
It avoids all the complications of having a single instance of a class, but all the instances use the same data. This is accomplished mostly by using `static` data members. One of the most important feature is that it's absolutely transparent for the users, that are completely unaware they are working with a Monostate. Users can create as many instances of a Monostate as they want and any instance is good as another to access the data.

### Singleton Testability
Need a way to work with dummy data so your tests are not dependent on a single object's data.

## Adapter
Getting the interface you want from the interface you have.

An adapter is a construct which adapts an existing interface X to conform to the required interface Y.

### Adapter (no caching)
The problem with this method is generating too many temporary objects over and over again.

### Adapter (with caching)
Caches temporary objects so that creation only happens once.

## Bridge
Connecting components together through abstractions.

**Motivation**
* Bridge prevents a 'Cartesian product' complexity explosion
* Example:
    * Base class ThreadScheduler
    * Can be preemptive or coorperative
    * Can run on Windows or Unix
    * End up with a 2x2 scenario: WindowsPTS, UnixPTS, WindowsCTS, UnixCTS
* Bride patterns avoid the entity explosion

![Before Bridge](img/bridge-before.png?raw=true "Before applying Bridge pattern")

![After Bridge](img/bridge-after.png?raw=true "After applying Bridge pattern")

### Bridge
A mechanism that decouples an interface (hierarchy) from an implementation (hierarchy).
