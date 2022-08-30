[[Joi]]

# Deep Neste Application of JoiValidationGroups

## Tags:
#package,

---

## How To Apply JoiValidationGroups into Deeply Nested Objects
- Instead of using the pattern `@JoiSchema(getClassSchema(AnotatedClass).allow(null).required())` use `@JoiSchema(AnotatedClass, (schema: Joi.Schema) => schema.allow(null).required())`
	- `AnotatedClass` is the class that describes the payload which has been anotated with `joi` descriptors inside `@JoiSchema` decorator
	- **Described pattern** should be **used only** if the `AnotatedClass` has a **deep nested property** that needs to be **validated differently depending on used HTTP method**

### Explenation
Than suggested looking into `JoiSchema` function signature `JoiSchema(groups[], nestedType, customizeSchemaCallback?)` as a possible solution, which led to the revelation that the `nestedType` is of `Constructor<any>` type. `Constructor<any>` type supports `Joi.Schema` and `Joi.Object` types as well as any **class consturctor**.

This ment that instead of using `getClassSchema` to create `Joi.object()` from the `AnotatedClass`, we could directly pass the `AnotatedClass`. By using `JoiSchema(nestedType, customizeSchemaCallback?)` function signature inside the `AnotatedClass` we are esencialy constructing `Joi.object({})` literal with all the deep nested properties all at once and calling that whole object with the single `getClassSchema` with the apropriate `JoiValidationGroup` at the top level. With a single `getClassSchema` class the provided `JoiValidationGroup` will be applied to all of the properties that have specific validations per validation group, no matter how deeply nested they are.

## How To Apply JoiValidationGroups into Deeply Nested Arrays
Instead of using the pattern 
 ```ts
@JoiSchema(Joi.array().items(getClassSchema(AnotatedClass)))
arrayProperty: Array<unknown>;
```
use pattern
```ts
@JoiSchema(Joi.array().itmes(
	getClassSchema(AnotatedClass, { group: JoiValidationGroups.CREATE }),
	getClassSchema(AnotatedClass, { group: JoiValidationGroups.UPDATE })
))
arrayProperty: Array<unknown>;
```

### Explanation
We can't apply the same solution that was used on `@JoiSchema` since `Joi.array().items()` accepts `Joi.Schema` type. So instead of avoiding the use of the `getClassSchema` we double down and serve all the versions of the `AnotatedClass` regarding the `JoiValidationGroups`. 