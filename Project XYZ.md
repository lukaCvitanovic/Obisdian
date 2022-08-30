[[Supplier Invoice Integration Bugs]]

# Project XYZ

## Tags:
#job #intergration #bugs 

## Links:
[NG-20287](https://globalization-partners.atlassian.net/browse/NG-20287)

---

## Description
- When the professional is not fully onboarded into [[Classic]] allow lsp invoices to be associated to placeholder professional
	- This unonboarded professional is denoted with `professionalId: X`
- Make the mapping to Proejct XYZ based on **billing silo**

## Workings Out
- Map to project x, y or z based on `company` payload property
	- `comapny` is derived from silo
- Issue:
	1) Thip made a new lsp invoice with `professionalId: X` , given result is unexpected![[image (8).png|1200]]
		- **Billing silo** may be unrelated to **company silo**
			- Find the property or entety from which this billing silo can be extracted
				- Depending on **ACOUNTING_SERVICE** feature flag the `lspInvoice.getLspCountry().getSiloId()` or `lspInvoice.getLspCountry().getAcumaticaSilo()` is used
					- Figure out the SQL to check the siloId of lspCountry
						- SQL reveiled the `acumaticaSilo` is GP - Ireland LTD
							- Split silo with GP - Ireland 2 (MSA)
					- Code throws and error if LSP is **3rdparty** and silo is **not MSA**
						- Since the request went through, the silo is **MSA**
							- Limits to 3 options -> **US MSA silo still possible**
					- Try locally
			- Thip tryed again and had successful lsp invoices that were mapped correctly to project y and z
				- Invoice_Numbers: `00000511`, `00000512`
			- Bug reapetad
				- **gg-classic** logs show getting silo with id 1 -> **Globalization Partners** silo [logs](https://one.newrelic.com/logger?account=1747307&begin=1655318731311&end=1655321690508&state=dd0a752d-1052-2f0f-765b-6d00b5ac1933)
					- 