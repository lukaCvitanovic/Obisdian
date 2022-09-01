[[RaaS Cron Jobs Rework Implementation]], [[RaaS Cron Jobs Rework Learned]]

# RaaS Cron Jobs Rework Learned

## Tags:
#learning , #crons, #sqs, #envs, #testing, #optimization, #envs

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
- All envs have NODE_ENV set to production[[GP Environments#Misc|**]]
- An env automatically has access to the queue and possibly some other AWS resources[[GP Environments#Misc|**]]