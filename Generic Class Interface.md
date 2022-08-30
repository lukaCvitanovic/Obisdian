[[Typescript]]

# Generic Class Interface

## Tags:
#typescript 

---
```ts
interface GenericClass<T> {
	// Can declare only methods and properties
	// No Constructor declaration
	property: T;
	method(): T;
}
```