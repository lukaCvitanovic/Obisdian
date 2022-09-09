[[RAAS Cron Jobs Rework]]

# RaaS Cron Jobs Rework Implementation

## Tags:
#job, #rework

## Links:
- [[RaaS Cron Jobs Rework Learned]]

---

## Troubleshooting SQS
- Works with older set of creds
	- Ones that start with AKIA
- The creds from AWS only work when sessionToken is present
	- Ones that start with ASIA
- The core problem is still unknown
	- This issue should be happening, because how was the SQS accessed in the past
		- This issue was not present on **staging or staging1** (env in which the invoice file migration was tested also using SQS)
	- **DevOps** was contacted to provide **support**
- Possible solutions:
	1) If env do have AWS credentials set as env variables and are available to **all** envs
		- Session token is available in the envs and can be used in SQS config
	2) Return the SQS devCredentials to its initial state and don't use them in deployed dev envs
		- The current situation is different from when we tested invoice file downloading since that was done on **staging** or **staging1** which are **production envs**
			- As such they have devCredentials set to **undefined** which lets the natural env permissions do its thing and grant access to corresponding queues
			- Since **work-uat** is **development env** it devCredentials were set which led to denial of access because of incorrect credentials
		- [x] Find out if the v1 invoice file migration was performed on production env
			- If true then the theory is correct
				- Figure out how to differentiate between local env and deployed development env
			- Maybe Nathan, Jason or Stuart can remember
				- Invoice migration was done on **staging** env
			- Pedro revealed that work-uat should've had NODE_ENV set to production, but Jason requested the switch to development
				- The switch back is not possible since work-uat would point to production Workday
				- devCredentials condition was changed, so the deployed envs have the undefined and local env use AWS credentials
					- `process.env.NODE_ENV === 'development' && !process.env.SSM_ENVIRONMENT_PREFIX`
		- Finally works

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
- [x] Implement logging when the RaaS is finished
	- [x] Add new InfoCode/ErrorCode for new RaaS logging
	- [x] Rework InfoCodes to make it easier to add new codes
	- [x] Log when the all the requests are pushed into the queue
	- [x] Log when the queue is empty
- [x] Implement new pattern to the other crons
	- To Do
		- [x] Add gatewayId in the controller
		- [x] Add priority in the context
		- [x] Modify the mapper to forward ids
		- [x] Make one schedule call where all the requests are called with Promise.allSetteled
		- [x] use queueBulkJobStandalone
		- [x] Call retryReceivingMessages at the end of the cron
		- [x] Modify the unit tests
	- Crons
		- [x] lspBillUpdateStatus
		- [x] clientBillPaidStatus
		- [x] clientBillUnpaidStatus
- [x] Implement temp pattern for processing live entries
	- [x] Set the schedule
	- [x] Add condition to stop the execution if start date is end date
	- to do
		- [x] Remove payload
		- [x] Add initialRaasSize
		- [x] Set the date range that progresses towards today
		- [x] Use original report sertvice code
		- [x] set initial size
		- [x] change schedule parameters
		- [x] chage queueBulkJobStandalone parameters
		- [x] Increment cron start date
		- [x] change retryReceivingMessages parameters
		- [x] modify unit tests
	- Crons
		- [x] lspBillUpdateStatus
		- [x] clientBillPaidStatus
		- [x] clientBillUnpaidStatus
- [x] Optimization
	- Goal is to reach at least **1000req/hour** throughput
		- Reached **4800req/hour**
	- Try with Bottleneck limit to 2000
	- Try with priority ON_DEMAND
		- Throughput seams the same
	- **We are incountering deduplication issue**
- [ ] Testing
	- [x] For local testing find 10 client deposits and create a mock JSON to generate high volume mock payload
	- [x] For the env test find 10 client deposits from GP3 or GP1 and create a mock JSON to generate high volume mock payload
	- [ ] Check the queue can be accessed
		- The default access policy is not granting access to local env, presumably it's the same for other envs
			- More specific access policy is needed
		- [x] Check the work-uat queue
		- [ ] Check the staging queue
		- [ ] Check the prod queue
	- [x] Call routes on work-uat env where the code was deployed to check if the changes had the desired effect
		- [ ] Check lspBillUpdateStatus handler
		- [x] Check clientDepositUpdate handler
			- Initial work-uat testing
				- Testing with 1k entries -> ETA is 11 hours 
				- Initial throughput with Bottleneck value of 900 is **1.83req/min** or **110req/hour**
			- work-uat testing with correct Bottleneck pattern and disabled deduplication
				- 100 entries
					- Throughput is **80req/min** or **4800req/hour**
				- 1k entries
					- Throughput **79.42req/min**
					- Finished in 12 min
					- [x] 47 entries were not delivered
						- Caused because entries payloads didn't have ids derived from the index but defaulted to the random value that was repeated 47 time and thus those entries were deduplicated
		- [ ] Check clientBillPaidStatus handler
- [x] Changes to the crons
	- [x] Separate the scheduale for unpaid and paid cron so they don't overlap
		- Offset the Unpaid by 30 min
	- [x] No hardcoded date values
		- This was done only for testing purposes
	- [x] Reenable client deposit cron
		- Done for testing purposes
	- [x] Understand the flow of the reworked cron on SQS
- [x] Getting ready for production
	- [x] Revert changes regarding high load payloads for crons
		- This includes the unit tests

## Post Relies Improvements
- [ ] Make the crons log the current index of the entire instead of the number of the lest in queue
	- [ ] Implement InfoCodes upgrade
	- [ ] Make it so that on the entire number the cron name is visible in the logger context
	- [x] Debounce was not working since it needed to be called
		- Caused infinite loop of retries

## [Executions](https://globalization-partners.atlassian.net/wiki/spaces/GPB/pages/2779644220/Report+as+a+Service+-+update+Billed+to+Paid+status)
### lspBillUpdateStatus
**Date Range** | **# Entries** | **Status**
---------- | --------- | -------
3.7. - 10.7. |     1    | Done
10.7. - 17.7. |     74     | Done
17.7. - 24.7. |     336     | 337/ Done, without last 4
24.7. - 31.7.|      505     | Done
31.7. - 7.8. |      263     |
7.8. - 14.8. |      117      |
14.8. - 21.8. |     200     | Done, without the last
21.8. - 28.8. |     533     |
28.8. - 4.9. |      584     |
4.9. - 8.9. |       28     |


### clientBillPaidStatus
**Date Range** | **# Entries** | **Status**
---------- | --------- | -------
3.7. - 10.7. |     216     | Done
10.7. - 17.7. |    106      | Done, without the last
17.7. - 24.7. |    1317      | without the last 86
24.7. - 31.7.|      9605     | Done
31.7. - 7.8. |      2520     | Skiped
7.8. - 14.8. |      2247      | Done
14.8. - 21.8. |     3140     | 
21.8. - 28.8. |     3975     |
28.8. - 4.9. |      4685     |
4.9. - 8.9. |      1257      |

### clientBillUnpaidStatus
**Date Range** | **# Entries** | **Status**
---------- | --------- | -------
3.7. - 10.7. |     355     | 341 - 4 Done
10.7. - 17.7. |    134      | Done, without first 3 and last 1
17.7. - 24.7. |    41      |
24.7. - 31.7.|     90      |
31.7. - 7.8. |     26      |
7.8. - 14.8. |     73       | Done/61
14.8. - 21.8. |    231      |
21.8. - 28.8. |    899      |
28.8. - 4.9. |     199      |
4.9. - 8.9. |      782      |

