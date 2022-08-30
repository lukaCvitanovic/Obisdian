[[Project CP]]

# Create Project CP

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
    "id": "6e62b738-e02a-ec11-8181-0e5cac5097ed",
    // no
    //"projectDetailBillingPeriod": "On Demand",
    // Done
    "clientAccountingId": "108040",
    // Maybe -> 
    "description": "Company 164 - CA - Adelaide Hatada AS (Adelaide)",
    // no mapping
    //"hold": false,
    // -> Project_Name
    "professionalAccountingId": "108040CA460",
    // Done
    "startDate": "2021-10-12T10:55:58-04:00",
    // Inactive ->
    "status": "Active",
    /** No + 9
    "defaultAccount": "40000",
    "defaultSubAccount": "US00000",
    "costAccount": "40000",
    "costSubAccount": "US00000",
    "defaultAccrualAccount": null,
    "defaultAccrualSubAccount": null,
    "clientLocation": null,
    "billingRule": "MULTISILO",
    "allocationRule": null,
    "proFormaInvoice": true,
    */
    // get from the customer - requires the customer request
    "currency": null,
    // NEW
    "pricingModel": "ENTERPRISE",
    // NEW
    "professionalClassType": "EOR",
    /*
    "apDetail": true,
    "arDetail": true,
    "caDetail": true,
    "crDetail": true,
    // Does it need to be null
    "teDetail": null,
    "glDetail": false,
    "inDetail": false,
    "poDetail": false,
    "soDetail": false,
    "glAccountId": "cf68e58d-a7aa-4e6f-844d-9cead08d3179",
    "tasks": [
      {
        "id": "8a62b738-e02a-ec11-8181-0e5cac5097ed",
        "allocationRule": null,
        "billingOption": "By Billing Period",
        "billingRule": "MULTISILO",
        "description": "Task Description",
        "status": "Active",
        "taskID": "00"
      }
    ],
    "attributes": [
      {
        "attribute": "ClientPO",
        "value": ""
      },
      {
        "attribute": "Contract End Date",
        "value": null
      },
      {
        "attribute": "Contract Start Date",
        "value": "05/07/2021"
      },
      {
        "attribute": "First Name",
        "value": "Adelaide"
      },
      {
        "attribute": "Funded LSP",
        "value": "Gateway Computers 56 - Canada"
      },
      {
        "attribute": "Legal Invoice Header",
        "value": null
      },
      // maybe
      {
        "attribute": "Legal Entity Company Name",
        "value": "Company 164"
      },
      {
        "attribute": "Last Name",
        "value": "Hatada AS"
      },
      {
        "attribute": "Minimum Total Value",
        "value": null
      },
      {
        "attribute": "Payroll End Date",
        "value": null
      },
      {
        "attribute": "Payroll Start Date",
        "value": null
      },
      {
        "attribute": "Related LSP",
        "value": "Gateway Computers 56 - Canada"
      },
      {
        "attribute": "Status",
        "value": "Onboarding"
      },
      {
        "attribute": "VAT Percent",
        "value": null
      },
      */
      // maybe
      {
        "attribute": "Work Country",
        "value": "Canada"
      },
      {
        "attribute": "Work Province",
        "value": "AB"
      }
    ],
    /**
    "accountTaskMappings": [
      {
        "account": "11000",
        "defaultTask": "00"
      }
    ],
    // Maybe
    "files": [],
    "balances": null
    */
  }
}
```

### Required to be mapped


### Mapped
- data
	- clientAccountingId -> Customer_ID
	- startDate -> Start_Date
	- status -> Inactive
	- professionalAccoiuntingId -> Workday_Project_ID
	- courency -> Courency_Reference
	- description -> Description
	- attributes
		- work country -> Region_Reference_ID
								  -> Location_ID
		- work province -> Location_ID

### Unknown Mapping
- **To Generate**
	- [x] Project_Gourp_Reference <-
		- [x] figure out is it enterprise, standard or contractor
			- [x] Added to CP payload
			- Accepted values
				- Professional - Enterprise <- Enterprise
				- Professional - Standard <- Standard
			- **NEW**
				- Based on thans suggestion we can add `getIsProfessional` and `getIsContractor` methods to the `Professional` model in [[Classic]]
					- ![[Pasted image 20220413134504.png]]
					- Just like some similar existing methods in `Professional`
					- ![[Screenshot 2022-04-13 at 13.50.52.png]]
					- From that we can add the a property to the payload to accounting service that denotes if the professional is contractor or professional
					- **Edge case**
						- what value to mapp to if the type is not contractor or professional?
	- [x] Add professionalClassType to CP payload
	- [x] Project_Hierarhy
		- Depends on whatever the professionalClassType value
		- Accepted Values:
			- Professional_PH <- EOR
			- Contractor_PH <- Contractor
	- [x] LSP type
		- Depends on whatever the professionalClassType value
		- type : CUSTOM_WORKTAG_1
		- Accepted values:
			- CWV_GP_Entity <- EOR
			- CWV_Third_Party_LSP <- Contractor
	- [x] Business Unit
		- Depends on whatever the professionalClassType value
		- Reference_ID and Business_Unit_Name pairs
			- BU1: EOR
			- BU2: Recruiting
			- BU3: Contractors
			- BU4: Insurance
			- BU5: Shared Resources
		- Will there be a problem with the business unit worktag mapping since the values that it is mapped from can only be EOR or CONTRACTOR?
	- [x] Region <- from project id X, work province ?
		- two letters
		- **project id doesn't have province ?** 
	- [x] Location
		- for US/Canada
			- state or teritory
				- not available
					- **Maybe if attributes has Work Province ?**
		- other just Country

### Backwards Mapping
- Into what property do we mapp the professionalID/projectID from the WD response
	- data.professionalAccountingId ?
		- return professional id and professional country id
			- acumatica id <- professional_id from workday
			- country acumatica id <- the same
		- in [[Classic]] for createProfessional in AccountingProjectService the acumaticaId and countryAcumaticaId is not derived from accounting service response
- In [[Classic]] make the country accunting id map back into classic
	- this disables the "Send to Acumatica" button and request


## Notes
- Worktags
	- location, business unit, region, custome worktag are in default worktags object
		- 
		- each of these is in a seperate wd:Related_Worktags_by_Type_Data object
