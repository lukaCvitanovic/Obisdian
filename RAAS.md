[[Workday intergration]]

# RAAS

## Tags:
#job #intergration 

## Links:
- [[RAAS bugs]]
- [[RAAS Cron Jobs Rework]]

---

## ASV1 Flow
- **How are cron jobs triggered?**
	- triggered by [[Classic]]
- **From where are cron jobs fiered? (classic or AS)**
	- Fiered from [[Accounting Service]]
	- Also called bulk job and found in something.bulk.service
	- ![[CRONv1.drawio.svg|900]]

## ASV2 Implementation
- **Will there be need for sqs ?**
	- sqs was used to handle the work with queues and messages
- Crons can be run from ASV2 with @nestjs/schedule
	- Eliminats the need to run the crons from [[Classic]]
- After the Crons are done, data is returned to [[Classic]] via sendToCallbackUrl in ar-invoice.bulk.service.ts
- ![[CRON.drawio.png|1300]]

## New Crons
- [x] [[Cron Job Testing Endpoint]]
- [x] [[LSP Bill Update Status]]
- [x] [[Client Bill Paid Status]]

## Old Crons
- [ ] [[Credit Memo - Historyc Data]]