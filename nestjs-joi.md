[[Joi]]

# Nestjs-joi

## Tags:
#package

---

[[NPM]] package that enables using the [[Joi]] package in [[NestJs]] WOW
- Provides out of the box Pipes that can be easaly intergrated into [[NestJs]] controlers
	- JoiPipe can be integrated with [[NestJs]] HTTP method decorator such as @Post, @Patch ect.

## Used
- Created a fucntion to generate schema based on the **type** and provided payload **class**
	- This was done b/c **types** couldn't be transfomed into schemas or anotated with joi types
	- Example of this is OnDemandGppPayload type
	- b/c the **type** is generic, the provided **class** serves as a way of simulating that generic type in the schema
	- **class** is anotated with Joi descriptiors
		- for getting an Joi **anotated class** as a **Joi.object()** use **getClassSchema** function
- JoiPipe is added to routes that should be validated
	- For each route a separate JoiPipe is used
		- b/c of different payload type that are validated
