[[AWS]]

# SNS

## Tags:
#aws, #infrastructure 

## Links:
- [Docs](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
---

## Description
- Provides message delivery from publisher to subscriber
- Enables asynchronous communication
	- Messages are sent to **topic**
		- Topics function like channels
- Subscriber receives messages from the topic using one of possible [[SNS#Communication Pathways|communication pathways]]
	
## Communication Pathways
- Amazon Kinesis Data Firehose
- [[SQS]]
- [[Lambda]]
- HTTP
- email
- mobile push notifications
- SMS

## Features
- A2A messaging
- A2P messaging
- Standard and FIFO
- Message filtering
	- Filter messages based on message attributes