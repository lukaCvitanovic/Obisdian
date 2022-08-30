[[Customer Invoice Intergration Bugs]]

# Customer Bill Type Bug

## Tags:
#job #intergration #bugs 

## Links:
[NG-18571](https://globalization-partners.atlassian.net/browse/NG-18571)

---

# Description
- Unclear error displayed on [[Classic]]
	- ![[Pasted image 20220510102004.png]]
	- ![[Screenshot 2022-05-10 at 10.21.24.png]]
		- NewRelic logs for failed request

## Working Out
- Logs point to Workday not accepting the `Regular` as `Customer_Invoice_Type`
	- **Solutions**:
		1) Map `billType` to valid Workday types
			- Other types are passed as they are, `Regular` is mapped to `Regular Bill`

## Fix
- Mapped GPP values to Workday acceptable values