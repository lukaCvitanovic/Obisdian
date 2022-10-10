[[RaaS Cron Jobs Rework Implementation]]

# RaaS Cron Jobs Rework Learned

## Tags:
#learning , #crons, #sqs, #envs, #testing, #optimization, #envs, #job-learning, #spiky-work, #architecture

## Links:

---

## Description[[Programing Learned#Environment Testing|**]]
- **Whatever can be tested locally, test it locally, only things that can not be locally tested should be tested on the env**
	- In advance find out what is necessary to be in place to facilitate the testing and ask for it to be in place
		- Anything and everything around the environment
			- Env vars
		- DevOps stuff like pipelines, triggering git branch
		- When testing in envs where changes can't be made frequently make **as much of it customizable**, so user can change things on the fly
			- Like pulling data from **requests** to be used as config parameters for things and services
- This task show the **importance of monitoring** the servers in regard to processed entries, timeout times and memory usage
- All envs have **NODE_ENV** set to production[[GP Environments#Misc|**]]
- An env automatically **has access** to the queue and possibly some other AWS resources[[GP Environments#Misc|**]]
- **DLQ** can be setup locally as seen [[SQS#DLQ https docs aws amazon com AWSSimpleQueueService latest SQSDeveloperGuide sqs-dead-letter-queues html|here]]
- SQS **doesn't notify** in any way that deduplication occurred
- Service process can be **stalled** because of **excessive use of blocking code** (async-await) when that kind of code is **called loads of times**
	- Event loop gets bogged down
- This kind of spiky work should never be run on the same instance as the normal operation work
	- **Spiky work should be performed on the separate instance** to handle the work and not block the normal operations
		- If this option is not viable then it's best to utilize the serverless architecture which allows the horizontal scaling that is better suited to handling spiky work
			- In this situation a [[Lambda]] could have been used to offload messages from the queue