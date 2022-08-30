[[Submit Project Bugs]]

# 199999 Invalid Customer

## Tags:
#job #intergration #bugs 

## Links:
[NG-18067](https://globalization-partners.atlassian.net/browse/NG-18067)

---

## Description
- For some countries under the same customer the professional creation is failing
	- Tryign to get cusomer with id 199999
		- [[Classic]] could be possible source of the error
			- **Hint:** that user together with 199998 and 199997 is used for intercompany transactions
		- If the `isMsaSilo` is `false` then the `msaSilo.getSiloCustomerAccountingId()` is used and results in one of the above mentioned ids
			- `AccountingService.createProjectAcumaticaEntities`

## Fix
- Try to replicate localy
	- Find the US customer in silo
- Should we make so that all createProfessioanl calls are made with `isMsaSilo` set to `true` behind the feature flag
	- **Courrently that is determined if the professional doesn't have accountingId ?**
		- Made so that the `createProfessional` is called without msaClientId regerdeless of the `isMsaSilo` flag