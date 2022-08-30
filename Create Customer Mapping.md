[[Customer Mapping]]

# Create Customer Mapping

## Tags:
#job, #mappings, #possible_bug 

---

 Mapping is done based on [[Create Customer WP]] and [[Create Customer CP]]

## Details
- There is added clientProvince in [[Create Customer CP]]
- Emails separeted by colon are mapped to [Email_Address_Data](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Email_Address_Information_DataType)
	- First emial has [Primary](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Communication_Usage_Type_DataType) tag set to true, the rest have it set to false
- Payment Methods properties from [[Create Customer CP]] are not mapped
- Issue ocured regarding workdat response
	- Response returns only customer id
	- [[Classic]] needs all the properties from sent with the request to be returned
		- Current solution is to merge workdat response with the data from the request to create [[Accounting Service]] response that satisfies [[Classic]]
		- **Potencialy problematic and bug prone**