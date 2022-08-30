[[Workday intergration]]

# Validation Pattern

## Tags:
#job,

## Links:
- [[Deep Nested Application of JoiValidationGroups]]

---

- Anotate classes that describe the payload with JoiSchema
	- **Usefull tip**: for loading class as object schemas use getClassSchema method
- in the @Body annotation put schameValidationPipe method
	- Provide it with prevously mentioned class that has JoiSchema annotations
		- Create Joi.object() that coresponds to the type that is used in describing the payload type
			- Types can't be transformed into schemas
	- If the payload can ==differ== depending on ==HTTP method== then
		- provide ==JoiValidationGroup== which inicated how the payload should be validated
			- This requires that the properties that should have different validation depending on HTTP method need to have JoiValidationGroup that coresponds to the HTTP method
	- Customer error messages can be written folowing [[Joi Custom Error Messages]]