[[Supplier Invoice Integration Bugs]]

# Relise 3rd Party Invoice Held At WD

## Tags:
#job #intergration #bugs 

## Links:
[NG-20066](https://globalization-partners.atlassian.net/browse/NG-20066)
[NewRelic Logs](https://one.newrelic.com/logger?account=1747307&duration=259200000&state=0f082521-6eda-286b-06d6-dc4a9d762351)

---

## Description
- [[Accounting Service]] returns `Error converting JS to XML`
	- ![[image (3).png|700]]
		- When sending **LSP invoice** of type LSP Deposit Help
	- Noticed failed **getProject** during this LSP invoice call

## Workings Out
- Error replicated locally
- Spend category code doesn't exsit in ASV2

## Fix
- Added code to Spend category