[[Accounting Service Post Release]], [[RAAS]]

# RAAS Cron Jobs Rework

## Tags:
#job, #raas, #cron

## Links:
- [NG-21424](https://globalization-partners.atlassian.net/browse/NG-21424)
- [[RaaS Cron Jobs Rework Implementation]]
- [[RaaS Cron Jobs Long Term Solution]]
---

## Description
- App crashes when running the **client deposit cron**
	- The cron generates up to 8k callback requests
		- This results in memory issues
	- Trafic spikes usually happen at the end of the mounth

## Fixes
- Cron job service needs to **fire-and-forget** the callback requests
- Solutions:
	- [?] Refactor callbacks to use SQS to insure that the callbacks are done completly asynchronously
		- [[RaaS Cron Jobs Rework Implementation]]
		- Possible problem is that the worker should be implemented on [[Classic]] side
			- [?] SQS worker implemented in [[Accounting Service]]
				- Based on implementation pattern in [[accounting-serivce-v1]]
				- **New** SQS queue will created just for processing the RaaS cron jobs
					- **New** env variable pointing to that queue **SQS_ACCOUNTINGV2_BULK_QUEUE_URL**
						- Locally set it to point to the Bulk queue
				- Results ![[Screenshot 2022-08-19 at 16.35.36.png]]
					- Results on 5k sample
					- took upwards of 20min to execute
			- [ ] SQS worker implemented in [[Classic]]
				- Question is if the sqs worker should even be implemented on [[Classic]] instead of [[Accounting Service]]
		- Figure out how in this imeplementation would we know that the RaaS was processed successfully?
			- What does it mean that the RaaS is executed successfully?:
				- [?] Does it mean that for each entries the callback has been made, regardless of the way the way the request was resolved
					- [[RaaS Cron Jobs Rework Implementation]]
					- Possible solution is to log out different states the process is in
						- Log out when all the entries are **pushed onto the queue**, which whould signify that all the entries have been fetched
						- Log out when the **queue becomes empty** again, which would signify that all of the entries have been processed also signiying that the cron-job is finished
							- Possible issue whith using this condition to determine if the cron-job is finished is if some other cron-job is executed concurently, resulting in the wrong finishing time of the first cron
				- [ ] Does it mean that for all entries the callbacks have resolved sucessfully
	- [ ] Refactor the callback by removing the awaits
		- Possible problem is that this could be imposible

## Testing
- Solutions have to be tested on large set, of around 10k requests
	- Testing is based on used memory since this is the issue that happens on the envs
		- Possible way of getting this metric is with `process.memoryUsage`
	- Baseline results to beat
		- ![[Screenshot 2022-08-17 at 16.35.17.png]]