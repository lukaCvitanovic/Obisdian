[[Creational Patterns]]

## Tags:
#programing-concept 

## Links:
- [Resource](https://refactoring.guru/design-patterns/abstract-factory)

---

## Description
- A way to create a family of similar products

## Motivation

## Problem
- How to create variants of family of products
	- Family of products has different products that have the same style
- Example problem given in the [Resource](https://refactoring.guru/design-patterns/abstract-factory): how to create a chair, coffetable and a sofa that can belong to different styles

## Solution
- First create interfaces for each of products
	- Interface for `Chair`, `Coffetable` and `Sofa`
		- From these interfaces we can create variants of these products
- Then create `apstract factory` to define what creation method for products that can be inside the product family
	- Creation methods for products must return **abstract** product type represented by interfaces for each of the family products
- To implement variants of the product family we create factory based out of `abstract factory` that created the particular variant of the products
- The client code is working with factories and products using their respective abstract interfaces
	- This means that client doesn't care what factory variant or product variant it uses as long as it is using the same base interface for both cases
	- This enables easy switching between the variants
- The product variant is determined with **config** or **environmental variable**

## Application
- when your code needs to work with various families of related products, but you don’t want it to depend on the concrete classes of those products—they might be unknown beforehand or you simply want to allow for future extensibility
- Consider implementation when a class has a set of factory methods that blur its primary responsibility

## Implementation Steps
1) Create a matrix of product type vs variants
2) Create an `abstract product interface` for each product type
	- Make each of product classes implement their respective `interface`
3) Create an `abstract factory` with creation methods for each of the `abstract products`
4) Create set of `concrete factories` for each of the products variants
5) Create factory initialization in the app
	- This should generate one of the `concrete factories`
		- Based on app configuration or env
	- Pass the factory to the classes the construct the products
6) Replace all calls to the product constructors and replace them with the calls to the creation method for the respective object

## Pros
- Products from the factory are compactible with each other
- Lessens the coupling between concrete products and client code
- [[Single Responsibility Principle]]
- [[Open/Closed Principle]]

## Cons
- Increase in complexity and added boiler plate code