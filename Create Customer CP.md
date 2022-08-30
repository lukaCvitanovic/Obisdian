# Classic Create Customer Payload

## Tags:
#job, #payload 

---

```js 
{

"context": {

	"company": "Globalization Partners",
	
	"priority": "ON_DEMAND",
	
	"callbackUrl": null,
	
	"context": null

},

"data": {
	
	"id": null,
	// ?
	"clientTermCalendar": "S",
	
	"clientLegalEntityName": "Company 1",
	
	"customerID": null,
	// ?
	"clientTermDays": "NET10",
	// ?
	"preferringBillingCurrencyCode": "USD",
	
	"mainContact": {
		
		"primaryEmail": "MagdaleneLaquay42@anonymized.com;AlbaSchuett48@anonymized.com;ArceliaGladle1793@anonymized.com",
		
		"clientLegalEntityName": "Company 1",
		// ?
		"contactName": "Magdalene Laquay (Magdalene)",
		// not neaded
		"web": "https://www.anonymized.com",
		// ?
		"busPhone": null,
		
		"mobilePhone": "3109648444",
		
		"address": {
			
			"clientBillingAddress1": "test st 123",
			// ?
			"clientBillingAddress2": null,
			
			"clientCity": "Los Angeles",
			
			"clientProvince": "California",
			
			"clientProvinceCode": "CA",
			
			"clientPostalCode": "90210",
			
			"clientCountryCode": "US"
		
		}
	
	},
	// ?
	"paymentMethods": [
			// mapp only the one with isClientDefaultPaymentMethod: true
			{
				
				"active": true,
				
				"description": "GP ACH",
				
				"isClientDefaultPaymentMethod": false,
				
				"paymentMethod": "GP ACH"
			
			},
		
			{
			
				"active": true,
				
				"description": "GP Wire",
				
				"isClientDefaultPaymentMethod": true,
				
				"paymentMethod": "GP WIRE"
			
			}
		
		]
	
	}

}
```

### Unknown Mapping
- Do we need the context property
	- Maybe only the **company** property
- **clientTermCalendar**
- **clientTermDays**
- **preferringBillingCurrencyCode**
	- Maybe  [Business_Entity_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Customer_Business_Entity_WWS_DataType).[CurrencyObject](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#CurrencyObjectType)
- **web**
	- may be [Business_Entity_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Customer_Business_Entity_WWS_DataType).[Contact_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Contact_Information_DataType).[Web_Address_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Web_Address_Information_DataType).Web_Address
- **busPhone**
- **clientBillingAddress2**
	- maybe [Address_Line_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Address_Information_DataType)
- 


