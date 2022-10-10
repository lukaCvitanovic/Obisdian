[[AWS]]

# SQS

## Tags:
#aws, #infrastructure 

## Links:
- [[Localstack SQS Wierdnes]]
- [[SQS Bugs]]
---

## [DLQ](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html)
- Messages are pushed into DLQ when there are issues consuming them
	- DLQ can be used to debug those troublesome messages to figure why they failed to be processed
- **Redrive Policy** determines the source queue and DLQ and conditions in which messages are pushed from the source to DLQ
- **maxReceiveCount** specifies number of times the consumer retries reading a message from queue, without deleting it, before sending it to the DLQ
	- Low number will result in catching messages that failed doe to the network errors
		- It advises to set a** high enough number** to ensure message processing without such occasional errors
- ### Benefits
	- Can be used to setup an alarm when message is moved to DLQ
	- Analyse contents of messages that have been moved into DLQ
- When performing DLQ redrive into source queue
	- Messages are bing sent `sendMessageBatch`
	- Redriven messages are considered new messages with new messageId
- ## Local Setup
	- Add command below to setup shell file
	- `awslocal sqs set-queue-attributes --queue-url="http://localhost:4566/000000000000/local-accounting-bulk.fifo" --attributes='{"RedrivePolicy": "{\"deadLetterTargetArn\":\"arn:aws:sqs:us-east-1:000000000000:local-accounting-dlq.fifo\",\"maxReceiveCount\":\"3\"}","VisibilityTimeout": "10"}'`

## [Lambda Function With SQS](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html)
- Can be used to process messages from SQS queue
- Pools messages and invokes Lambda function **synchronously** on event that has messages
- Messages are read in batches
	- Default is 10 messages per pool
	- Lambda function is called once per batch
- Once batch is processed, Lambda deletes it from queue
- 