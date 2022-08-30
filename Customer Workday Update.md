[[Customer Integration Bugs]]

# Customer Workday Update

## Tags:
#job #intergration #bugs 

## Links:
[NG-19716](https://globalization-partners.atlassian.net/browse/NG-19716)

---

## Description
- After the customer is created
	1) When client user is added to the customer with **Accounts Payable** role
		- His email address is sent to Workday -> **CORECT**
	2) When the same client is updated to not have **Accounts Payable** role
		- His email is still pressent in Workdat -> **INCORECT**
			- Should be removed from Workday
	3) When the same same client was **AP** and now is **UNASSOCIATED**
		- His email is still pressent in Workdat -> **INCORECT**
			- Should be removed from Workday

## Working Outs
2) Classic removes the client users email from the PUT payload to [[Accounting Service]]
	- ASV2 is sends only emails present in the Classic's payload
		- Client users email is not present
	- Client in workday is not updated
		- When the `Do_Not_Replace_All` flag on the Workday payload is set to `false` then the emails are **updated correctly**
			- After implementation **issue Fixed**
3) Classic doen't remove the email of the clients that have **UNASSIGNED** only the ones that have **IsNoLongerWithTheFirm**
	- Added a `ClientPersonService`  method to find Clients by role except for ones with **UNASSIGNED** role
	- Added a condition when the user is **Accounts Payable** and has a change on **UNASSIGNED** role

## Fix