[[SQS Bugs]]

# AWS Signature expired Bug

## Tags:
#sqs #aws #bugs 

## Links:

---

## Description
- This Error ocures because the big time difference between timsestamp in token from the message and local time, more [here](https://github.com/aws/aws-sdk-js/issues/1174)

## Reprodiction
- **MUST** use real [[SQS]]
	- Localstack 0.12.20 **doesn't throw this error**
1) Send message to the [[SQS]]
2) Change local time on your machine to 30 min in the past
3) Read the message from [[SQS]]
4) Receive an error![[Screenshot 2022-09-30 at 14.17.04.png]]

## Fix
- Solution is **correctClockSkew** shown [here](https://docs.aws.amazon.com/en_us/AWSJavaScriptSDK/latest/AWS/SQS.html)
	- [x] Apply this to the SQS config
	- [x] Test if it works when the machine time is behind 15 min
	- [x] Make calculateDates is able to generate moment objecst for lsp and other crons that differ in date format