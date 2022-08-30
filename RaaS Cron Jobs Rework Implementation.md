[[RAAS Cron Jobs Rework]]

# RaaS Cron Jobs Rework Implementation

## Tags:
#job, #rework

## Links:
- [[RaaS Cron Jobs Rework Learned]]

---

## Steps
- [x] Implement [[SQS]] Pattern in [[Accounting Service]]
	- [x] Implement queueJob method in CronJobsService
	- [x] Rework crons to use sqs
		- [x] Rework lspBillUpdateStatus
			- [x] Rework lspBillUpdateStatus mapper to generate list of payloads for each report entrie
			- [x] Test locally the sqs flow 
		- [x] Rework clientDepositUpdate
			- [x] Rework testingClientDepositUpdate
				- [x] Check if the sqs flow works
				- [x] Do the sqs flow with high load
				- [x] Instead of filtering out proccesed entries from the array, have a cron job entrie counter
				- [x] Check if the getStatus for the queue works now
			- [x] Move the changes to real clientDepositUpdate method 
		- [x] Rework clientBillPaidStatus
			- Reworked in such a way that each entry is its own payload
		- [x] Rework clientBillUnpaidStatus
			- Reworked in such a way that each entry is its own payload
	- [x] Modify getQueuqJob method
	- [x] Add new env variable for new queue
	- [x] Modify sqs-worker.handleBulkJob to handle cron jobs
		- [x] Add lspBillUpdateStatus handler
		- [x] Add clientDepositUpdate handler
		- [x] Add clientBillPaidStatus handler
		- [x] Add clientBillUnpaidStatus handler
	- [x] Implement worker callback methods
		- [x] Add lspBillUpdateStatus handler
		- [x] Add clientDepositUpdate handler
		- [x] Add clientBillPaidStatus handler
		- [x] Add clientBillUnpaidStatus handler
	- [x] Check why on docker start of [[Accounting Service]] the RAM is filled to 100%
- [x] Implement Loggging when the RaaS is finished
	- [x] Add new InfoCode/ErrorCode for new RaaS logging
	- [x] Rework InfoCodes to make it easier to add new codes
	- [x] Log when the all the requests are pushed into the queue
	- [x] Log when the queue is empty
- [ ] Testing
	- [x] For local testing find 10 client deposits and create a mock JSON to generate high volume mock payload
	- [x] For the env test find 10 client deposits from GP3 or GP1 and create a mock JSON to generate high volime mock payload
	- [ ] Check the queue can be accesed
		- The default access policy is not granting access to local env, presumably it's the same for other envs
			- More specific access policty is needed
		- [x] Check the work-uat queue
		- [ ] Check the stagin queue
		- [ ] Check the prod queue
	- [ ] Call routes on wokr-uat env where the code was deployed to check if the changes had the desiered effect
		- [ ] Check lspBillUpdateStatus handler
		- [ ] Check clientDepositUpdate handler
		- [ ] Check clientBillPaidStatus handler
- [x] Changes to the crons
	- [x] Separate the scheduale for unpaid and paid cron so they don't overlap
		- Offset the Unpaid by 30 min
	- [x] No hardcoded date values
		- This was done only for testing purposes
	- [x] Reenable client deposit cron
		- Done for testing purposes
	- [x] Understand the flow of the reworked cron on SQS
- [ ] Getting ready for production
	- [ ] Revert changes regarding high load payloads for crons
		- This includes the unit tests

