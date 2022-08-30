[[Customer WP]]

# Workday Create Customer Payload

## Tags:
#job, #payload

## Links:
- [Documentation](https://community.workday.com/sites/default/files/file-hosting/productionapi/Revenue_Management/v38.0/Submit_Customer.html#Communication_Usage_Type_DataType)

 ---


```xml 
<?xml version="1.0" encoding="UTF-8"?>
<env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <env:Header>
        <wsse:Security env:mustUnderstand="1" xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
            <wsse:UsernameToken wsu:Id="UsernameToken-86F2FCCEFFBB80C4CD14820998755791">
                <wsse:Username>ISU_FINT001_GPP_Customer@globalizationpartners3</wsse:Username>
                <wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">Welcome@123
                </wsse:Password>
                <wsse:Nonce EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">asdfwrqwarqwr1+oA==
                </wsse:Nonce>
                <wsu:Created>2016-12-18T22:24:30.575Z</wsu:Created>
            </wsse:UsernameToken>
        </wsse:Security>
    </env:Header>
    <env:Body>
        <wd:Submit_Customer_Request xmlns:wd="urn:com.workday/bsvc" wd:version="v36.1">
            <wd:Add_Only>true</wd:Add_Only>
            <!-- <wd:Customer_Reference>
                <wd:ID wd:type="Customer_ID"></wd:ID>
            </wd:Customer_Reference> -->
            
            <wd:Business_Process_Parameters>
                <wd:Auto_Complete>true</wd:Auto_Complete>
            </wd:Business_Process_Parameters>
            <wd:Customer_Data>
                <!-- <wd:Customer_ID></wd:Customer_ID>
                <wd:Customer_Reference_ID></wd:Customer_Reference_ID> -->
                <wd:Customer_Name>AP-test</wd:Customer_Name>
                <wd:Worktag_Only>0</wd:Worktag_Only>
                <wd:Submit>true</wd:Submit>
                <wd:Customer_Category_Reference>
                    <wd:ID wd:type="Customer_Category_ID">Business_Services</wd:ID>
                </wd:Customer_Category_Reference>
                <wd:Business_Entity_Data>
                    <wd:Business_Entity_Name>AP-test</wd:Business_Entity_Name>
                    <wd:Contact_Data>
                        <wd:Address_Data wd:Effective_Date="2022-01-21">
                            <wd:Country_Reference>
                                <wd:ID wd:type="ISO_3166-1_Alpha-2_Code">US</wd:ID>
                            </wd:Country_Reference>
                            <wd:Address_Line_Data wd:Type="ADDRESS_LINE_1">test st 123</wd:Address_Line_Data>
                            <wd:Municipality>Los Angles</wd:Municipality>
                            <wd:Country_Region_Reference>
                                <wd:ID wd:type="Country_Region_ID">USA-CA</wd:ID>
                            </wd:Country_Region_Reference>
                            <wd:Country_Region_Descriptor>California</wd:Country_Region_Descriptor>
                            <wd:Postal_Code>90210</wd:Postal_Code>
                            <wd:Usage_Data wd:Public="true">
                                <wd:Type_Data wd:Primary="true">
                                    <wd:Type_Reference>
                                        <wd:ID wd:type="Communication_Usage_Type_ID">BUSINESS</wd:ID>
                                    </wd:Type_Reference>
                                </wd:Type_Data>
                                <wd:Use_For_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_ID">BILLING</wd:ID>
                                </wd:Use_For_Reference>
                                <wd:Use_For_Tenanted_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_Tenanted_ID">Billing</wd:ID>
                                </wd:Use_For_Tenanted_Reference>
                                <wd:Comments>test</wd:Comments>
                            </wd:Usage_Data>
                        </wd:Address_Data>
                        <wd:Phone_Data>
                            <wd:Country_ISO_Code>USA</wd:Country_ISO_Code>
                            <wd:International_Phone_Code>1</wd:International_Phone_Code>
                            <wd:Phone_Number>3109648444</wd:Phone_Number>
                            <wd:Phone_Extension>111</wd:Phone_Extension>
                            <wd:Phone_Device_Type_Reference>
                                <wd:ID wd:type="Phone_Device_Type_ID">Mobile</wd:ID>
                            </wd:Phone_Device_Type_Reference>
                            <wd:Usage_Data wd:Public="true">
                                <wd:Type_Data wd:Primary="true">
                                    <wd:Type_Reference>
                                        <wd:ID wd:type="Communication_Usage_Type_ID">BUSINESS</wd:ID>
                                    </wd:Type_Reference>
                                </wd:Type_Data>
                                <wd:Use_For_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_ID">BILLING</wd:ID>
                                </wd:Use_For_Reference>
                                <wd:Use_For_Tenanted_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_Tenanted_ID">Billing</wd:ID>
                                </wd:Use_For_Tenanted_Reference>
                            </wd:Usage_Data>
                        </wd:Phone_Data>
                        <wd:Email_Address_Data wd:Do_Not_Replace_All="true">
                            <wd:Email_Address>test12@gp.com</wd:Email_Address>
                            <wd:Email_Comment>testing</wd:Email_Comment>
                            <wd:Usage_Data wd:Public="true">
                                <wd:Type_Data wd:Primary="true">
                                    <wd:Type_Reference>
                                        <wd:ID wd:type="Communication_Usage_Type_ID">BUSINESS</wd:ID>
                                    </wd:Type_Reference>
                                </wd:Type_Data>
                                <wd:Use_For_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_ID">BILLING</wd:ID>
                                </wd:Use_For_Reference>
                                <wd:Use_For_Tenanted_Reference>
                                    <wd:ID wd:type="Communication_Usage_Behavior_Tenanted_ID">Billing</wd:ID>
                                </wd:Use_For_Tenanted_Reference>
                            </wd:Usage_Data>
                        </wd:Email_Address_Data>
                    </wd:Contact_Data>
                </wd:Business_Entity_Data>
            </wd:Customer_Data>
        </wd:Submit_Customer_Request>
    </env:Body>
</env:Envelope>```

### Unknown Mapping
- Customer_Refernce
- Customer_Name
	- maybe business name
- Customer_Category_Reference
	- is this just hardcoded value
- Effective_Date  
	- is this the date of the request
- Usage_Data
	- Do these values need to change
- International_Phone_Code
	- not neaded if Country_ISO_Code is present
- Phone_Extension
	- not neaded if Country_ISO_Code is present
- 