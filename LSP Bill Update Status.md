[[RAAS]]

# LSP Bill Update Status CRON

## Tags:
#job 

## Links:
- [NG-17339](https://globalization-partners.atlassian.net/browse/NG-17339)
- [Tech Hub](https://globalization-partners.atlassian.net/wiki/spaces/EIA/pages/2499543231/Technical+Knowledge+Hub)
---

## Progress
- [x] Get report from [[Workday]]
	- Will need to create **user** for the [[Accounting Service]]
		- Need the **username** and **password** to generate Basic Auth header
			- Add these into envs
		- URL: `https://wd2-impl-services1.workday.com/ccx/service/customreport2/globalizationpartners3/ISU_FINT007_GPP_Supplier_Invoice/CR_FINT007_GPP_AP_LSP_Bill_Status?Company!WID=38b06d064eed0100f5f037986d040000&StartDate=2022-04-10T00:00:00.000-07:00&EndDate=2022-04-11T00:00:00.000-07:00&Document_Payment_Status!WID=d9e4362a446c11de98360015c5e6daf6](https://wd2-impl-services1.workday.com/ccx/service/customreport2/globalizationpartners3/ISU_FINT007_GPP_Supplier_Invoice/CR_FINT007_GPP_AP_LSP_Bill_Status?Company!WID=38b06d064eed0100f5f037986d040000&StartDate=2022-04-10T00:00:00.000-07:00&EndDate=2022-04-11T00:00:00.000-07:00&Document_Payment_Status!WID=d9e4362a446c11de98360015c5e6daf6&format=json`
			- Segment URL so the parameters can be changed
- [x] Mapp retport to GPP schema
	- Found [[Classic]] callback payload on [GitHub](https://github.dev/globalization-partners/gp-accounting-service)
- [x] Send separete callback request for invoices with different billing cycles
- [x] Send data via callback to [[Classic]]
	- find `context` for callback request
		- will need to send `billingCycleAccountingId` in `context`
			- [[Classic]] is updated to find the `billignCycleId` from `billingCycleAccountingId`
- [x] Set the correct cron job execution time
	- Every day at 9pm
- [x] Generate separete reports for different `Document_Payment_Status`-es
	- Generating reports for PAID
- [x] Create time span for which the report is being made
	- Past 25 hours from when the cron is started
- [x] For what companies do reports need to be generated
	- All companies
- [x] Should reports run only for PAID?
	- Yes