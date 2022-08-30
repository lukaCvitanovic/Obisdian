[[Workday intergration]]

# Populate S3 Bucket WIth Historic Invoices Including Credit Memos

## Tags:
#job 

## Links:


---

## Questions:
- Do I have to make some local dev enviroment changes to test this locally -> Y
	- postman collection
	- fire up accountignv1
		- branch is here
- Is this going to be run as cron e.g. once and never again

## Prerequesites
- accounting-service is running
	- branch `NG-20031-create-and-populate-s-3-bucket-to-store-historic-invoices-including-credit-memos`
	- `FEATURE_FLAG_ALWAYS_ENABLED` is **false**
- Modify the DB so that the `root-url` is like in the picture![[image (9).png]]
- Have the [Postman collection](https://gpcorporate.slack.com/archives/C035QQ7M5E0/p1656444656508629)
- Classic is on `deploy/test-patch`
	- Perform the `mvn liquibase:update`
	- **MISSING**
		- **db.changelog.xml** and update to the **db.changelog-master.xml**
- **Describe what changes were made to enable localstack**

## Description
- [ ] Create InvoicePi Entety type for request response