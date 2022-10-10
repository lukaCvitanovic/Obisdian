[[RAAS Cron Jobs Rework]]

# RaaS Cron Jobs Rework Implementation

## Tags:
#job, #rework

## Links:
- [[RaaS Cron Jobs Rework Learned]]
- [Updating Bills to Paid Status in Platform](https://globalization-partners.atlassian.net/wiki/spaces/GPB/pages/2825453796/Updating+Bills+to+Paid+Status+in+Platform)
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
	- [x] Check the queue can be accessed
		- The default access policy is not granting access to local env, presumably it's the same for other envs
			- More specific access policy is needed
		- [x] Check the work-uat queue
		- [x] Check the staging queue
		- [x] Check the prod queue
	- [x] Call routes on work-uat env where the code was deployed to check if the changes had the desired effect
		- [x] Check lspBillUpdateStatus handler
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
		- [x] Check clientBillPaidStatus handler
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

## [Executions](https://globalization-partners.atlassian.net/wiki/spaces/GPB/pages/2779644220/Report+as+a+Service+-+update+Billed+to+Paid+status)
### lspBillUpdateStatus
**Date Range** | **# Entries** | **Status**
---------- | --------- | -------
3.7. - 10.7. |     1    | Done
10.7. - 17.7. |     74     | Done
17.7. - 24.7. |     336     | 337/ Done, without last 4
24.7. - 31.7.|      505     | Done
31.7. - 7.8. |      263     | 261/ Done
7.8. - 14.8. |      117      |
14.8. - 21.8. |     200     | Done, without the last
21.8. - 28.8. |     533     | Done, till -97
28.8. - 4.9. |      584     |
4.9. - 8.9. |       28     |


### clientBillPaidStatus
**Date Range** | **# Entries** | **Status**
---------- | --------- | -------
3.7. - 10.7. |     216     | Done
10.7. - 17.7. |    106      | Done, without the last
17.7. - 24.7. |    1317      | without the last 86
24.7. - 31.7.|      9605     | Done
31.7. - 7.8. |      2520     | Skipped
7.8. - 14.8. |      2247      | Done
14.8. - 21.8. |     3140     | Done, till -2052
21.8. - 28.8. |     3975     |
28.8. - 4.9. |      4685     | Done/4640, till -3940
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
21.8. - 28.8. |    899      | Done/814, till -430
28.8. - 4.9. |     199      | Done/161, till -220
4.9. - 8.9. |      782      |

## Unknown
- [42](https://one.newrelic.com/logger?account=1747307&duration=259200000&state=acfc0c9e-048e-6ba2-2515-3a1c6d5ec4df)
	- na lsp cron job
	- unknown date span
	- till -68

## Missing
- First run
	- Missing
		- 00262316
		- 00268322  
		- 00254571  
		- 00263152
- Second run
	- Processed
		- 00263152
			- Was [processed 2 times](https://one.newrelic.com/logger?account=1747307&begin=1662023777172&end=1663578980554&state=dd3f9738-8d73-1b20-9600-953ed9e605dd)
				- on the 13th and 17th of Sept
		- 00254571
			- [Processed only last time](https://one.newrelic.com/logger?account=1747307&begin=1662023777172&end=1663578980554&state=6c9a60a1-b752-afd0-64ea-4c7846c01b36)
	- Missing
		- 00262316  
		- 00268322
			- [Processed as well](https://one.newrelic.com/logger?account=1747307&begin=1662023777172&end=1663578980554&state=60c1b56e-b7af-cb86-1d0d-e1cc9df5b45a) on the 18th Sept

## Post Relies Improvements
- [x] Make the crons log the current index of the entire instead of the number of the lest in queue
	- [x] Implement InfoCodes upgrade
	- [x] Make it so that on the entire number the cron name is visible in the logger context
- [x] Debounce was not working since it needed to be called
	- Caused infinite loop of retries
- [x] Make queue resilient to blocking by single message
	- Group messages
		- Only grouped messages are blocked
- [ ] Fix long receive message times
- [x] Add metadata to entries
	- [x] Add date spans
	- [x] Add total number of entries for that date span
- [x] Make the service log the invoice number
- [x] Make it so that it is indicated what number is added to the cron counter
- [x] Add the ability to actively use DLQ
	- Preparation
		- [x] See if it is possible to locally simulate the use of [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]]
			- **Yes**, by adding additional command to queue [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|setup]] shell file
		- [x] See if it is possible to read messages from [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]]
			- **Yes**
		- [ ] Is it possible to make a Lambda function that would trigger reading of [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]] messages
		- [x] Check if [[SQS]] returns info about deduplication through deduplicationId
			- **Not possible**
	- Goals:
		- [x] Add logging so we can better understand why [[SQS]] doesn't pick up some of the messages
		- [ ] Modify V2 so it pulls messages from [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]] and reprocesses them
			- Not needed since `maxReceive` is set to 5
				- Doesn't make sense since queue has attribute that allows messages to be received up to 5 times before being moved into [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]]
		- [x] Add logging of messages pushed into [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]]
			- Implementations Options:
				1) Add a cron to check the [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]] every minute
					- Would result in large amount of calls
				2) Set up a Lambda function on the queue that would call the method to pool messages from [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|DLQ]]
					- Question if this service is payed for and available for use?
- [ ] Add tracking of duplicated messages
	- **Not doable**
	- [[AWS]] doesn't provide any signal or event that would tell us that duplication occurred
	- The only other ways of implementation are:
		- A DB table that would store some identifier (conted digest) that would be checked
			- Would result in a lot of calls to and from DB
			- Would bring throughput down
		- A hash map that does the same think only it's not scalable
- [x] Check for skip feature flag before running the cron
	- Requires FEATURE_FLAG_ALWAYS_ENABLED to be `false`
	- [ ] Automate this latter
- [x] Add logging of message on delete and send message catch
- [x] Add error throwing in delete message
- [ ] Fix delete message method
- [ ] Fix receive message method
- [ ] Fix send message method
- [x] Fix `LEFT OF CURRENT`
- [x] Add delete message for DLQ messages
- [ ] Add a route for the upcoming RaaS to retrieve invoices based on invoice IDs
	- This will be only for `clientBillPaidStatus`
	- Will it be able to update multiple invoices in one go
	- RaaS can only receive one `invoiceId`
	- [x] Add payload validation
		- [ ] Make custom error messages
	- [ ] Add response validation
	- [ ] Create a service method to handle the requests
		- Should be similar to `queueClientBillPaidStatus`
		- [x] Add short circuting if invoices are empy
		- [x] Remove skip cron condition
			- Not needed since it won't be cron job
		- [x] Remove `calculateDates`
		- [ ] Call workdayApiReportService
			- [ ] Create new a URL in `WorkdayReportUrl` for new Raas
		- [ ] Remove cron counter
		- [ ] Create a mapper for new RaaS
		- [ ] Schedule the callback to [[Classic]]
		- [ ] Remove date iteration
		- [ ] Remove `readQueue`
	- [ ] Create unit tests
- [ ] ---
- [ ] Run cron locally with `--prof` to gather analitics form node
- [ ] Add Joi validation to cron job controller
- [ ] Add response validation to cron job crontroller
- [ ] Add the use of batchSend and batchReceive

## Runs
- [[24.9. Run]]
- [[28.9 Run Analitics]]
- [[4.10 Run Analitics]]
- [[5-6. 10 Manual Run]]
- [[7-8-9. 10 Manula Run]]

## Robustness Criteria
- [x] Handle the long execution that goes into the next execution run
	- Make it so that the cron counter is not set to new number, but rather the new number is added to the current cron counter number
		- If there are no errors all the messages will eventually be processed as long as we ask for message
