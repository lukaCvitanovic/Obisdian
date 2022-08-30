[[Supplier Invoice Integration Bugs]]

# Strict Validation Bug

## Tags:
#job #intergration #bugs 

## Links:
[NG-18500](https://globalization-partners.atlassian.net/browse/NG-18500)

---

## Description
- [[Classic]] displayes this error when sending LSP transaction
	- ![[Screenshot 2022-05-06 at 18.38.39.png]]

## Workings out
- To strict Joi validation
	- Check serializer to determine what is necessary for the mapping, based on that loosen the validation
- Default value for the `wd:Supplier_Reference`
	- **Needs Change**
		- use `fundedLspCountryAccountingId` value
- Mapped values for `wd:Supplier_Reference` are not accepted by Workday
- In `GPSpendCategoryToWorkSpendCategory` mapped value `Deposit_with_LSP` is not accepted and doesn't exist in [[Workday]]
	- **Find some other mapping**

## Fix
- Loosen the schema validation based on whats required for mappign