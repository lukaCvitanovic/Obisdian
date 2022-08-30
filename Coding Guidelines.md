[[Coding]]

# Coding Guidelines

## Tags:
#guidelines, #coding 

---
Most of these try to impore readability of the code.


- KIS - **Keep It Simple**
	- Don't make thing complicated
- SSOT - **Single Source Of Thruth**
	- Only one location in the codebase must be used as the source of some value
	- Don't pull the value from multiple sources
- **Separation Of Concearns**
	- One thing (some scope of code) must do only one thing
		- If code does multiple things, break it down into smaller segments
	- Implementation is helped by:
		- Short methods
			- Method shouldn't be longer than 20 lines
				- In most cases methods can be broken down into smaller methods
					- Which help in readability
		- Implementing each branch of if clouse in a separate method
