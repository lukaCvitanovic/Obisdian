[[RAAS]]

# RAAS Bugs

## Tags:
#job #intergration #bugs 

## Links:
[NG-20335](https://globalization-partners.atlassian.net/browse/NG-20335)

---

## Description
- Client depostis are not visible in [[Classic]] even though they are present in Client Deposit RAAS


## Workings Out
- `Transaction_Amount` returned by RAAS has negative value
	- Classic code sets t balance to be updated to 0 if the `Transaction_Amount` is negative
