[[Creational Patterns]]

## Tags:
#programing-concept 

## Links:
- [Resource](https://refactoring.guru/design-patterns/builder)

---

## Description
- Interface for creating objects in a superclass which allows subclasses to alter the type of object that would be created

## Problem
- How to create a variation on existing class that is coupled in the codebase as seen in the example from the [[Factory Method#Links|Resource]], without introducing unnecessary conditionals large scale rewriting of the codebase

## Solution
- Replace direct object construction calls with calls to *factory* method
	- We are moving `new` into that method
	- With object construction being done in the factory method it allows subclasses to override the method to return different product
		- **Caveat** is that these different products must have a common base class or interface
			- Return type of the factory method must be the declared interface

## Application
- When we don't know in advance the type and dependencies of the object used
	- Separates the object construction code and code that uses the object
		- The client code doesn't care about the object construction code as long as that class extends the base class or common interface
- A way of opening up a lib or framework so that other code users can extend it with their own implementations
	- This is done with combination of inheritance and factory method
		- This enables the new subclass to be recognized as a valid class to be used by the base components of the lib or framework
- When we want to save resources by reusing existing objects

## Pros
- Removes tight coupling between the creator and concrete products
- [[Single Responsibility Principle]]
- [[Open/Closed Principle]]

## Cons
- Increase in complexity
	- Best case scenario is when we introduce the pattern into existing hierarchy of creator classes