[[Invoice Listing Report Bugs]]

# Positive Values on Credit Memos
## Tags:
#job #intergration #bugs 

## Links:
[Invoice Listing Report Comapny 45](https://globalizationpartners-my.sharepoint.com/:x:/g/personal/lsanchez_globalization-partners_com/EezZc1LSKN5Pt3ufrhM0v6AB4F5NArKZBjoXTue3aBJomA?e=uI0Okl)

---

## Description
- The Credit Memo with accountingId is negative
	- The ones without it are positive
		- They came from Credit Memo Cron Job
			- Locally only 3 out of 3842 Credit Memos are postive
				- Felds that are the same for 3 positive Credit Memos:
					- creted_by -> 1
					- status -> 11
					- calculated_managment_fee -> 0
					- contractual_management_fee -> 0
					- is_management_fee -> 0
					- legacy_invoice_file_msa_acumatica_silo_id -> 1
					- document_type -> 1
					- lsp_country.status -> 2
					- lsp_country.lsp_status -> 2
					- lsp_country.client_payroll_cycle_status -> 2
					- lsp_country.is_founding_entety -> 1
					- lsp_country.is_prefered_partner -> 1
				- No relation between these same values and positive values
			- Need to get access to the env DB and work-uat classic to check the audit logs
				- [[How To Access Deployed Envs]]
				- Table generated based on data from the env
					- Data is incorect in the DB, mistake is **not caused by faulty logic**
					- From the DB audit logs it seams that the values are added by some cron job (credit-memo or historical-credit-memo)
						- Check what are the values in [[Acumatica]] with Deborah
**ID** | **Total Bill** | **Amount in DB** | Value Added By | Date
-----------|-----------:|----------:|-----------:|-----------:
78235 | 103.42 | -103.42 | System User | 2021-09-16
67357 | 6115.07 | -6115.07 | System User | 2021-09-17
7739 | -198.02 | 198.02 | System User | 2021-09-24


