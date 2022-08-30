[[Workday intergration]]

# Accounting Service v2 File Structure

## Tags:
#job

---

## Main Idea
- Separate [[Acumatica]] from [[Workday]] code
	- so that the current flow to [[Acumatica]] is not disturbed
	- to know when when changes are made on the workday related code

## File Structure
**Entety** - logicly separte part reflected in the DB, requests, classic and workday
**(will not need to change)** - no changes needed if the workday entety mapping is added

- /src
	- /entety
		- entety.controler
		- entety.workday.service.spec
		- entety.workday.service
		- /enteties
			-  ?
		- /mocks
			- /v2
				- workday mocks
	- /workday-api
		- /mocks (will not need to change)
		- workday-api.service.spec (will not need to change)
		- workday-api.service (will not need to change)
	- /workday
		- /serializer
			- /operations
				- /entety-operation
					- operation-entety.serialier
		- worday.constants (will not need to change)
		- workday.type (will not need to change)



## Required changes when adding workday mapping
- ### entety.controller
	- eg. customer.controller
	- needs to support [[Acumatica]] and [[Workday]] calls
		- needs to support OnDemandGppPayload and OnDemandPriorityRequestPayload
		- needs the workday entety service
			- eg. CustomerWorkdayService
- ### entety.module
	- needs ParserModule
	- entety acumatica service
		- eg. CustomerService
	- entety workday service
		- eg. CustomerWorkdayService
- ### entety.workday.service
	- handels calls to workday for that entety
- ### workday-api.service
	- handels all calls to workday
	- is envoked in entety.workday.services
- ### operation-entety.serializer
	- naming convention is from workday operations
	- workday serializer that maps from gpp schema to workday schema
		- ==? will the reverse serializers be in the same folder==
		- ==? what would be their naming convention==
			- for submit-customer maybe ==submit-customer.deserializer==