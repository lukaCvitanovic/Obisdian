[[Customer Invoice Intergration Bugs]]

# Customer Invoice Null Bug

## Tags:
#job #intergration #bugs 

---

## Description
- When trying to send Customer Invoice an error message pops up saying:
	- *1 of 1 bills failed to be sent to Acumatica  
		Reason(s)  
		Failed to send Invoice #236858 to Acumatica - null*
- [[Classic]] is correctly sending the payload
- [[Accounting Service]] is receiving the payload, forwarding it to [[Workday]] and sending back a response
- [[Clasic]] is not receiving the response from [[Accounting Service]]

## Workings Out
- Client invoice didn't have `@UseInterceptors(TransformInterceptor)`
	- **This results in correct response when sending the payloads from Postman, but wasn't being received on [[Classic]]**

## Fix
- Add `@UseInterceptors(TransformInterceptor)` to client invoice controller