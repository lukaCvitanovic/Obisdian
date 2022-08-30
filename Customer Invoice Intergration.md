[[Workday intergration]]

# Customer Invoice Intergration

## Tags:
#job  #intergration 

## Links:
- [[Customer Invoice Intergration Bugs]]

---


## Progress

## Manual Testing In Classic
1) Create client
	- Assign user
	- Set user as Main Acumatica User
2) Create professional in client
	- Add necessary fields
	- Add home address
	- Add work address
		- Remove validation in AccountingProfessionalAPI schema
3) Generate setup bill for professional
	- In professional Onboarding tab
4) Open Client Bill page
	- Find the bill
		- Should be type "Setup"
5) Select the checkbox by the bill
6) Change the bill status to "Ready to Validate"
7) Clikc "Relise to Acumatica"