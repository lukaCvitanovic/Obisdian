[[Project WP]]

# Create Project WP

## Tags:
#job, #payload

## Links:
- [Docimentation](https://community.workday.com/sites/default/files/file-hosting/productionapi/Resource_Management/v37.2/Submit_Project.html#Accounting_Worktag_and_Aggregation_DimensionObjectType)

---

```xml
<?xml version="1.0" encoding="UTF-8"?>

<env:Envelope

xmlns:env="http://schemas.xmlsoap.org/soap/envelope/"

xmlns:xsd="http://www.w3.org/2001/XMLSchema">

  

<env:Header>

<wsse:Security

env:mustUnderstand="1"

xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"

xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">

<wsse:UsernameToken wsu:Id="UsernameToken-86F2FCCEFFBB80C4CD14820998755791">

<wsse:Username>ISU_FINT002_GPP_Project@globalizationpartners3</wsse:Username>

<wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">Welcome@123</wsse:Password>

<wsse:Nonce

EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">asdfwrqwarqwr1+oA==

</wsse:Nonce>

<wsu:Created>2016-12-18T22:24:30.575Z</wsu:Created>

</wsse:UsernameToken>

</wsse:Security>

</env:Header>

  

<env:Body>

<wd:Submit_Project_Request xmlns:wd="urn:com.workday/bsvc" wd:Add_Only="true" wd:version="v37.2">

<wd:Business_Process_Parameters>

<wd:Auto_Complete>true</wd:Auto_Complete>

</wd:Business_Process_Parameters>

<wd:Project_Data>
<!-- empty string --> 
<wd:Workday_Project_ID></wd:Workday_Project_ID>

<wd:Locked_in_Workday>false</wd:Locked_in_Workday>

<wd:Project_Hierarchy_Reference>
	<!-- For now hardcoded Professionals_PH --> 
	<wd:ID wd:type="Project_Hierarchy_ID">Professionals_PH</wd:ID>

</wd:Project_Hierarchy_Reference>
<!-- GPP profesional name = first name + last name --> 
<wd:Project_Name>PROJ-TEST050420220950</wd:Project_Name>
<!-- GPP start date --> 
<wd:Start_Date>2022-02-17</wd:Start_Date>

<wd:Project_State_Reference>
	<!-- For now hardcoded PROJECT_STATE_PROJECT --> 
	<wd:ID wd:type="Project_State_ID">PROJECT_STATE_PROJECT</wd:ID>

</wd:Project_State_Reference>

<wd:Customer_Reference>

<wd:ID wd:type="Customer_ID">000056</wd:ID>

</wd:Customer_Reference>

  
  

<wd:Worktags_Data wd:Replace_All="true">

<wd:Related_Worktags_by_Type_Data>

<wd:Worktag_Type_Reference>

<wd:ID wd:type="Accounting_Worktag_Type_ID">BUSINESS_SITE</wd:ID>

<wd:ID wd:type="Worktag_Type_ID">BUSINESS_SITE</wd:ID>

</wd:Worktag_Type_Reference>

<wd:Required_On_Transaction>0</wd:Required_On_Transaction>

<wd:Required_On_Transaction_For_Validation>0</wd:Required_On_Transaction_For_Validation>

<wd:Default_Worktag_Data>

<wd:Default_Worktag_Reference>

<!-- Changed the format to LOC_XX_YY -->

<wd:ID wd:type="Location_ID">LOC_US_MA</wd:ID>

</wd:Default_Worktag_Reference>

</wd:Default_Worktag_Data>

<wd:Replace_All_Allowed_Values>true</wd:Replace_All_Allowed_Values>

</wd:Related_Worktags_by_Type_Data>

</wd:Worktags_Data>

  
  

</wd:Project_Data>

</wd:Submit_Project_Request>

</env:Body>

</env:Envelope>
```

### Unkwnon Mapping
- Project_Hierarchy_ID inside Project_Hierarchy_Reference
	- for now hadrcoded Professional_PH
- 