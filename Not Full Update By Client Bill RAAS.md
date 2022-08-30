[[Client Bill Paid Status Bugs]]

# Not Full Update By Client Bill RAAS

## Tags:
#job #intergration #bugs 

## Links:
[NG-19847](https://globalization-partners.atlassian.net/browse/NG-19847)
[Slac message](https://gpcorporate.slack.com/archives/D035DQNF63A/p1654113041271689)

---

# Description
- Not all Client Bills are updated by the RAAS
	- ReportClientBillPaidStatusSerializer maps `Invoice_Number` into callback payload
	- Some invoices have the `GaplessInvoiceNumber` which should be mapped insted of `Invoice_Number`
	- The RAAS has 3 types of invoices:
		1) Customer Invoice without `GaplessInvoiceNumber`
			- ![[Screenshot 2022-06-02 at 09.37.51.png|500]]
		2) Customer Invoice with `GaplessInvoiceNumber`
			- ![[Screenshot 2022-06-02 at 09.38.55.png|500]]
		3) Customer Invoice Adjustment
			- ![[Screenshot 2022-06-02 at 09.40.01.png|500]]

## Workings Out
- For the 1 nad 3 map back `Invoice_Number`, for 2 map `Gapless_Invoice_Number`