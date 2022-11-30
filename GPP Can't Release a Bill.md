[[Accounting Service Post Release]]

## Tags:
#job #bug

## Links:
- [NG-29637](https://globalization-partners.atlassian.net/browse/NG-29637)

## Steps:
```memaid
graph TD
	1[Trying to reproduce locally] --> 2[Searching the NewRelic logs - 15.11.2022]
	2 --> 3[Functionality is again working as intended - 16.11.2022]
	3 --> 4[Left a comment for Irvin to confirm my findings - 16.11.2022]
	4 --> 5[Irvin closed the ticket - 17.11.2022]
```
---

## Description
- When a bill that has VAT fees is released to accv2 it throws the error `_Failed to send Invoice #263509 to ERP. Critical error occurred when interacting with the ERP. Moved to ‘ERP ERROR’ status. Stopping processing_`

## Progress
- The bills are passing successful
	- Work-Uat billing successfully sent ![[Screenshot 2022-11-16 at 11.40.31.png]]
	- [NewRelic logs](https://one.newrelic.com/logger?account=1747307&begin=1668591754226&end=1668593239171&state=6081099f-986f-83a6-1ef1-f9cbe97e629b)