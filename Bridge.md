[[Structural Patterns]]

# [Bridge](https://refactoring.guru/design-patterns/bridge)

## Tags:
#programing-concept

## Description
- [[Structural Patterns]] that allowes splitting a large class or set of closely related classes into two hierarchies: **abstraction** and **implementation**
	- Those can then be developed independently

## Problem
- We are trying to create subclasses that will solve one combination of the property dimensions that we are working with
	- Resulting in **exponentional number** of new classes that need to be added when new property for single dimension is added
	- In the example bellow property dimensinos are shape and color
		- Functionality of colored shapes is solved using inheritance

![[Pasted image 20220325135415.png]]


	

## Solution
- Instead of using inheritance, by separting each property dimensino into individial classes: **Shape** and **Color**, we can use **composition** to get the colored shapes
	- Composition is done i such a way that one class hierarhy references the other one
		- eg. **Shape** has property **Color** that then can by red or blue or any other color that is added afterwards
![[Pasted image 20220325140126.png]]

## Structure
![[Pasted image 20220325140946.png]]
- **Abstraction** or in this case super class describes higher level logic
	- Logic is described through features that implement the interface methods
	- Client using this abstraction only cares about the higher level functionality
	- **Refined Abstractions** use Concrete Implementations
- **Implementation** or in this case the interface deals with lower level methods from which the abstraction features are constructed
	- Implementation does all of the actual work
	- **Concerete Implementations** imeplement the interface in different ways to accomodate the given useage

## Use Cases
- For division of a monolitic class that has several similar functions, like connecting to different DBs
	- Splitting of a monolitic class makes those classes independent
		- Changes don't effect other classes
		- Minimizes the possibility of bugs
- For extending a class in differnect dimensions
	- Delegate dimensional work to separate classes 
- To be able to switch between imeplementations
	- eg. DB connection
		- Changing DB from the point of DB connection requires changing DB connection implementation or creating one if it doesn't exist

## Pros
- Adds the ability to create platform-idependent classes and apps
- Client code works with high-level abstractions
	- not with the platform details
- Open/Closed Principle
	- Introduction of abstractions and implementations can be done separatly
- Signle Responibility Principle
	- Focus on high-level logic in abstractions
	- Focus on platform details in implementation

## Cons
- Complicates highly cohesive classes