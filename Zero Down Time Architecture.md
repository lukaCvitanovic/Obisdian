[[TO DO]]

# Zero Down Time Architecture

## Tags:
#programing-concept, #deployment_strategy

## Links:
- [Blue/Green Modle](https://globalization-partners.atlassian.net/wiki/spaces/GPDEV/pages/2609872930/Classic+-+Zero+Downtime+Architecture+Review)

---

## Motivation
- All production **changes** (all PRs) to the service require **restarting of the production**
	- Causes bussines **interuptions for rach release**
- Easy solution is to perform the release during the **off hours**
	- Viable, but **not sustainable long term**
	- **Restricts** the frequency of the deployments
- Blue/Green infrastructure deployment strategy
	- Enable **minimal** production **interuptions**
	- Inline with CD methodology
		- Should be used when applcation or services have **high visibility** by the customers
- Final goal of this deployment architecture is to hide deployment steps behind the sceens so that the **customers are not aware** of them

## Description
- This deployment architecture consists of load-balancer infront of **2 identical enviroments** (Blue and Green)
	- Blue has the **current code**
	- Green has the **new changes**
	- Load-balancer **points to Blue**
- Once Green is **tested and verified in isolation**
	- Load-balancer points to Green

## Pros
- Zero down time b/c when load-balancer switches the pointed envrionment it doesn't affect the customer
- Test are performed in production environments
	- May cause garebage data
- Easy rollback to Blue env in case of an issue
- Decrese the blas radius

## Cons
- During the switch, current sessions and transactions will be lost
- Can cause data compability issues
	- Old and new code is using the same DB
		- Some changes may not be supported by older code

