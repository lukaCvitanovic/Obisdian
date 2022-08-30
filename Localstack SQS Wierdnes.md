[[SQS]]

# Localstack SQS Wierdness

## Tags:
#guidelines, #wierd

## Links:

---

### Messages are not received even thou they are in the queue
- The rule that is followed with the [[SQS]] is the the message is read from the queue, after the worker is done performing, the message should be **removed** from the queue
	- This is done automatically if the worker finishes as intended
	- If worker incounters an error, the message needs to be deleted manualy for other messages in the queue to be processed

