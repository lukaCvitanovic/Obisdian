[[Creational Patterns]]

## Tags:
#programing-concept 

## Links:
- [Docs](https://refactoring.guru/design-patterns/builder)
- [Example](https://refactoring.guru/design-patterns/builder/typescript/example)
---

## Description
- Lets us constrict complex objects step by step
- Lets us produce different types and representations of an object using the same construction code

## Problem
- How to optimally construct complex object that can have multiple variants (some properties are slightly different)

## Crude Solutions
1) Create subclasses from the base class
	- This would lead to huge number of classes needed
		- Difficult to maintain and update
2) Create a huge constructor in the base class
	- It's not a desired coding pattern
	- Ugly

## Solution Provided By The Pattern
- ### Builder
	- Extract the construction code from the base class into separate Builder class
	- Object construction is organized into building steps → methods of a Builder class
	- Object construction is done by calling those building steps in a sequence
	- With this pattern only needed building steps that are required are called
		- We can choose the building steps used
	- Some building steps can differ in their implementation resulting in different object representation
- ### Director
	- Extracts Builder's construction steps into specific building sequences
	- Director provides the execution order of building steps while Builder provides the specific implementation of a building step

## Application
- To remove telescoping constructor
- To be able to have different representation of the object

## Pros
- Construct objects step by step, defer steps or run steps recursively
- Reuse construction steps when building new object representations
- *Single Responsibility Principle*, isolate complex construction code from the business logic

## Cons
- Increased code complexity since we are creating new classes