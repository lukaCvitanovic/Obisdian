[[Client Bill Paid Status]]

# Add Paid Date to Client Bill Paid Status Cron

## Tags:
#job #intergration 

## Links:
[UAT Status Padi Date row](https://globalization-partners.atlassian.net/wiki/spaces/GPB/pages/2597519422/UAT+Status)

---

## Description
- [x] Add a mapping for `lastFunctionallyUpdateDate` property from the RAAS (ASV2) to `padiDate`
- [x] Add a `paidDate` property to `AccountingInvoiceAPI` class
- [x] The `paidDate` will be set using `setDateBillPaid`  or it defaults to `new Date()` ![[Screenshot 2022-06-23 at 16.21.59.png]]
- [x] Test if the date is updated in the [[Classic]]
- [x] Create tests in [[Accounting Service]]