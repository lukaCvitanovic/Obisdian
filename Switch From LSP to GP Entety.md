[[Update Project Bugs]]

# Switch From LSP to GP Entety

## Tags:
#job #intergration #bugs 

## Links:
[NG-19609](https://globalization-partners.atlassian.net/browse/NG-19609)
[Stuart's work on Classic](https://github.com/globalization-partners/gp-go-global/compare/NG-19609-switching-professionals-from-lsp-entity-to-gp-entity)

---

## Description
- When a professional that is associated with **3rd party LSP** is switched to **GP entety** that change is not present in the Workday
- [[Classic]] is sending `null` for professional status

## Workings Out
- Change is not present b/c [[Classic]] is sending in the payload `isGpEntety: false`
	- Which should be set to `true`
		- Issue with the [[Classic]]
	- The issue was that professional that was sent to [[Accounting Service]] didn't have changes the user made, but was the professional as it was before the changes happend
		- This is b/c the professional was being retreived from DB which was being updated after the request to [[Accounting Service]] was resolved
			- **FIX** -> first update the DB and then send the professional to [[Accounting Service]]
- The [[Accounting Service]] request to [[Workday]] was failing
	- This is due to using the default workday web service instead of `Resource Management`

## Fix
- Changed the order of the operations, first update the DB and then send the updated professional to [[Accounting Service]]
	- Also made small changes with the payload creation for the [[Accounting Service]] so that the professional has the active status
- Changed the posProject method in [[Accounting Service]] to use `Resource Management` workdat web service to sucessfully make update requests