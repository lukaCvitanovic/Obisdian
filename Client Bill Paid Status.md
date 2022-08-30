[[RAAS]]

# Client Bill Paid Status

## Tags:
#job 

## Links:
- [NG-17338](https://globalization-partners.atlassian.net/browse/NG-17338)
- [Tech Hub](https://globalization-partners.atlassian.net/wiki/spaces/EIA/pages/2499543231/Technical+Knowledge+Hub)
- [[Client Bill Paid Status Bugs]]

---

## Progress
- [x] Add report url constructor
	- **What is the time span used in the report?**
- [x] Add report GPP serializer
- [x] Find the cron callback method
- [x] Send callback request
	- [x] callback payload has to be `AccountingInvoiceAPI` type
	- ![[Screenshot 2022-05-26 at 16.13.03.png|500]]
- [x] Modify [[Classic]] to be able to handle the callback payload
	- [x] Resolve clientBillIds from clientBillAccountingIds
		- Added `extractClientBillIdsFromClientBillAccountingIds` that gets clientBillIds from clientBillAccountingIds
	- [x] Confirm client bills status gets updated to PAID
- [x] Create Unit tests for new cron job
- [x] Set Cron job execution times

## Upgrade
- [ ] [[Add Paid Date to Client Bill Paid Status Cron]]