[[RaaS Cron Jobs Rework Implementation]], [[RaaS Cron Jobs Rework Learned]]

# RaaS Cron Jobs Rework Learned

## Tags:
#learning , #crons, #sqs, #envs, #testing, #optimization

## Links:

---

## Description[[Programing Learned#Environment Testing|**]]
- **Whatever can be tested locally, test it locally, only things that can not be locally tested should be tested on the env**
	- In advance find out what is necessary to be in place to facilitated the testing and ask for it to be in palce
		- Anything and everything around the environment
			- Env vars
		- Devops stuff like pipelines, trigerring git branch
		- When testing in envs where changes can't be made frequently make **as much of it customizable** and by things user can change on the fly
			- Like pulling data from a **requests** to be used as config parameters for things and services
- This task show the **importance of monitoring** the servers in regards to processed entries, timeout times and memory usage