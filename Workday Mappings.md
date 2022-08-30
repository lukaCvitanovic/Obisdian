[[Workday intergration]]

# Workday Mappings MOC

## Tags:
#job

## Links:
[SharePoint](https://globalizationpartners.sharepoint.com/fs-pwc/Shared%20Documents/Forms/AllItems.aspx?id=%2Ffs%2Dpwc%2FShared%20Documents%2F2%2E%20Technical%2FIntegration%2FGP%20Platform&viewid=1635602a%2Dec26%2D4e46%2Daa9e%2D2f4bb80858b2), [Workday Documentation](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Customer_WWS_DataType)

- Mappings are based on [[Workday Payloads]] and [[Classic Payloads]]
- [[Mapping Pattern]]


---
- [ ] [[Customer Mapping]]
- [ ] [[Project Mapping]]
---

## Generic Mapping
- Create mapper methods to transform classic payload to workday one
	- These only work with JS
- Create [[Shema Serializer]] that will convert from Classic schema to Workday schema and back
	- Base on this use case eg.
	```ts
	async postCustomer(payload: OnDemandPriorityRequestPayload) {
	  // this will convert gp property names to workday property names
	  const workDayPayload = new CustomerWorkdaySchemaSerializer(payload.data);
	  // this will be xml
	  const workDayXml = this.parserService.convertJsToXml({ username: '', tenant: payload.context.company, data: workDayPayload });
	  // this will be some XML workDayResponse
	  const workDayResponse = await this.workdayApiService.post({ xml: workdayXml });
	  // converts the XML response to JS to get mapped back to GP Schema
	  const workDayResponseJs = this.parserService.convertXmlToJs(workDayResponse);
	  // this will transform workday property names back to gp property names
	  const res = new CustomerGppSchemaSerializer(workDayResponseJs); 
	  return res;
	}
	```