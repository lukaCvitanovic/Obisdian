[[Accounting Service]]

# Workday Intergration

## Tags:
#job, #process

## Description
- Plan for [[Accounting Service]] to change [[ERP]] by migrating from [[Acumatica]] to [[Workday]]
	- Will be caried out in 2 stepts

## Step 1
Have the [[Workday]] intergrated with [[Accounting Service]] along side [[Acumatica]] so that the 2 ERPs could be compared and show to business.

### Implementation

![[Pasted image 20220318171015.png]]

- 2 repos for [[accounting-serivce-v1]] and [[accounting-service-v2]]
	- Pros:
		- b/c of inexperienced team this ensures the stability of the current [[Accounting Service]]
		- Removes the posibility for confusion of the concearn
	- Cons:
		- Have to maintain two repos (acceptable for a short time)
		- Drives the changes to [[Classic]]
		- Drives the nead for new dev setup as this will be treated as a new service
	- Required changes:
		- [x] Will require some way of [[AS tranfic routing]]
			- Complexity that arises when having 2 repos
		- [x] Will require changes in [[Classic]]
			- [x] At the payload level
				- Could be problems if the [[Classic]] doesn't have the needed info
			- [x] At the endpoint level
		- Will require heavy changes to [[accounting-service-v2]] to support [[Workday]]
			- [x] Will remove [[Silo]] (very dificult)
			- [x] Will have to implement [[XML2JSON]] adapter
			- [x] Will require new mapping for [[Workday]] payloads
				- Mappings are shown in [[Workday Mappings]]
			- [x] Will require [[Schema Validation]]

### Intergrations
- [x] [[Customer Intergration]]
- [x] [[Project Intergration]]
- [x] [[Customer Invoice Intergration]]
- [x] [[Supplier Invoice Intergration]]

## Misc
- [x] [[Workday Maintenance Window]]
- [ ] [[Report PII Data From Logs and Platform]]
- [x] [[Non-Secure JWT Logging]]
- [x] [[NewRelic Dashboards]]
- [ ] [[Hystoric PDFs from S3]]
- [x] [[invoice Listing Report]]
- [x] [[Credit Memo Document Type]]
- [ ] [[Populate S3 Bucket WIth Historic Invoices Including Credit Memos]]

## [[RAAS]]

### Patterns Going Forward:
- [[ASv2 File Structure]]
- [[Serializers Pattern]]
- [[Mapping Pattern]]
- [[Validation Patters]]
- [[Cron Pattern]]

## Step 2
After the [[accounting-service-v2]] is stable enough and all current operations and funcionalities are supported, [[Acumatica]] will be droped