[[Info And Error Codes Rework]]

# Info And Error Code Rework Learned

## Tags:
#learning , #naming_convention, #structuring

## Links:

---

## Description[[Programing Learned#Naming convention|**]]
- Done imeplementation solves the issue of adding new codes by reducing the number of code names that are needed to be changed when a new code is added
	- Codes are restructured like HTTP status codes
	- The same issue still persists inside the code sections
- Proposed improved solution
	- Usses this pattern
		- AS(E/I){code}#{code}#{code}
		- This pattern would be used like JSON where each code represents holds a set of codes or a code value
	- Improvments
		- This pattern further reduces the need to change existing code names when adding a new code
		- Clear separation of nested code numbers levels
		- Allowes unlimited number of codes and nested codes
	- Drawbacks
		- Less readable
