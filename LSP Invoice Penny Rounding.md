[[Supplier Invoice Integration Bugs]]

# LSP Invoice Penny Rounding

## Tags:
#job #intergration #bugs 

## Links:
[NG-20068](https://globalization-partners.atlassian.net/browse/NG-20068)

---

## Description
- Penny rounding differences between [[Classic]] and [[Workday]]
	- 00000420![[image (4).png|800]]![[image (5).png|1000]]
	- 00000419![[image (6).png]]![[image (7).png]]

## Workings Out
1) Stumbeled upon **getProject errors**
	- Seen in logs and replicated locally
	- Caused **inproper type** definition of payload parameter on getProject method
		- Which let to sending only payload data to getProject method
			- Method **couldn't determine the company** since the payload didn't have context property
2) Sutumbeled upon **company of undefiend** error
3) `iterateAndMapAccountingBillDetails`  was not being awaited
	- Method was resolved after serialization, which is not intended behaviour
/ | **Original Ammount** | **Converted Ammount** | **Rounded** | **Rounded Loss**
:-----------------------|--------------------|-----------------------|-----------------------|-----------------------:
**∑** | 7163.36 | 7163.3599341 | 7163.35 | -0.0099341920004
1 | -- | 5269.495 | 5269.49 | -0.0050000000001
2 | -- | 24.99998985 | 25 | +0.000010150000001
3 | -- | 1499.999391 | 1500 | +0.0006089999999
4 | -- | 368.86465 | 368.86 | -0.0046499999999
5 | -- | 0.000903342 | 0 | -0.000903342
R ∑ | -- | -- | **-0.01** | -0.00993419200013
4) Invoice ammount is rounded at the penny value
	- Classic is sending the correct ammount
		- Seen in logs and **replicated locally**
	- ASV2 is receaving it correctly
		- After the serialization is done the sum of `Extended_Amount` has a difference of 1 penny from the `totalAmountInInvoiceCurrency`
		- Based the rounding loss shown in the table we see that the difference in penny comes from rounding the numbers
			- Solution:
				1) If the difference in the rounding when rounded is equal to 0.01 then add that rounding difference to the rounded value, otherwise return the roundnded value
					- This can be applied to the rounding differenc of the 1st element in which case the rounding difference will disappear
				2) Solution 1) doesn't fix the second example
					- Solution:
						- Calculate the `roundingDifference` and apply the change of 0.01 to each `Extended_Amount` so that the sum of the rounded amounts is the same as the `totalAmountInInvoiceCurrency` that is rounded
				3) Change the code in [[Classic]] that calculates the `totalAmountInInvoiceCurrency` so that it matches how the [[Workday]] calculates the sum
					- Then we are introducing cuppeling between the [[Classic]] and [[Workday]]
						- Should be avoided
/ | **Original Ammount** | **Converted Ammount** | **Rounded** | **Rounded Loss**
:-----------------------|--------------------|-----------------------|-----------------------|-----------------------:
**∑** | 27289.23 | 27289.2324578454 | 27289.24 | +0.007542154602560913
1 | -- | 27289.227 | 27289.23 | +0.0030000000006111804
2 | -- | 0.0054578454 | 0.01 | +0.0045421546
R ∑ | -- | -- | **+0.01** | +0.00754215460061118

## Fix
1)  Fixed by setting proper type definition to getProject method
	- Which requires proper payload to be sent
2) Fixed by fixing 1)
3) Fixed by making the `iterateAndMapAccountingBillDetails` asynchronus
	- Even tho `iterateAndMapAccountingBillDetails` was implementing await to the `mapCompanyReferenceId` method, since it is called inside the `forEach`, the `forEach` method itself is not asynchronus so the undelying asnyc methods are not awaited
		- To solve the issue, we need to use `Promise.all` maethod that can resolve array of promises
			- So the `iterateAndMapAccountingBillDetails` is modified to return promises that can be resolved, inturn the `iterateAndMapAccountingBillDetails` itself can be awaited as intended
4) Fixed by calcualting the rounding difference rounded to the 2nd decimal precision, if that difference is **0.01** then this difference is **added** to the **roundedValue**, otherwise roundedValue is returned
	- We are rounding the roundingDifference because this represents the **rounding mistake** that ocures if it's not corrected