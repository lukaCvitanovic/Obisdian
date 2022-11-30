[[Creational Patterns]]

## Tags:
#programing-concept 

## Links:
- [Resource](https://sourcemaking.com/design_patterns/prototype)

---

## Description
- Enables copying existing objects without **coupling** code to their classes

## Problem
- How to create an exact copy of an object
	- The direct approach **doesn't take into account** the "hidden" or private properties and methods and this is a cumbersome process
		- This creates a **coupling** between the code and the class of the copied object
			- Forces us to use the object interface that **we can't avoid**

## Solution
- Delegate the cloning to the object itself
- This pattern declares the common interface for cloning objects
	- This **decouples** the code from the object class
	- Interface contains the `clone` method
		- `clone` method is implemented similarly, method creates new object of the same class,  caries over all the properties from the current object into the new one even the private ones
			- Most languages allows access to private properties to the objects of the same class
- Objects that allow cloning are called **prototypes**
- Example of use
	- We have an object that we configured in a certain way, if we want the object with the same configuration we just clone the original object

## Application
- Use the pattern when code needs to be decoupled from the objects class
	- Particularly useful when working with objects passed from 3rd party libs
- Use the pattern to cut-down on the number of subclasses with slightly different initializations
	- If a complex class can be configured in a number of different ways create a couple of subclasses that are configured differently and with cloning we have dummy classes from which we can generate objects configured in a certain way

## Implementation
1) Create prototype **interface** with **clone** method
	- Or add the method to all the classes of the class hierarchy
2) Prototype class must define an alternative constructor that accepts and object of that class and an input
	- This constructor copies all the properties of the given object into a new class instance
	- If the subclass is changed the superclass constructor needs to be called to handle the private class properties
	- If the programming language doesn't support the method overloading it will be impossible to create separatee `prototype`
		- Object copying would need to be done inside the `clone` method
		- Having the cloning code inside the regular constructor is safer because the resulting object is returned fully configured right after the `new` operator is called
3) Usually cloning consists of running a `new` operator with the prototypical version of the constructor
	- Every class must override the cloning method and use its own class name along with the `new` operator
		- Otherwise the `clone` will be of the parent class
4) Optionaly create a centralized prototype registry to store a catalog of frequently used prototypes
	- Registry could be implemented as a [[Factory Method|Factory Class]]
		- Or put it in the base prototype class with a static method for fetching the prototype

## Pros
- Ability to clone objects without coupling to their concrete classes
- Get rid of repeated initialization code
- Conveniant reproduction of complex objects
- Alternative to inheritance when dealing with configuration presets for complex objects

## Cons
- Cloning complex objects that have circular references may be tricky