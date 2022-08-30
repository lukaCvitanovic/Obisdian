[[Workday intergration]]

# Serializers Pattern

## Tags:
#job

## Links:
- [[Workday Envelope Serializer]]

---

## Basic Principles
- Serializer use the [[class-transformer]] package to perform transformations to the classes
	- @Exclude anotation is used to exclude the property or method from being visible when printing the class instance
		- **Crutial** since we want only the one top level class property to be visible so that the class instance will bi similar to the payload
	- instanceToPlain method that transforms the class into its instance
		- Same sa JSON stringify parse but more elegant
