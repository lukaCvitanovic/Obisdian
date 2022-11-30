[[Customer Payment GPP Pending In Workday Approved in Platform]]

## Tags:
#job #payload 

## Links:
- [NewRelic](https://one.newrelic.com/logger?account=1747307&begin=1667428800000&end=1667429340000&state=548bdc6d-35b5-3668-c350-0c0d4d108576)
---

```json
{
    "context": {
        "company": "Globalization Partners",
        "priority": "ON_DEMAND",
        "callbackUrl": null,
        "context": null
    },
    "data": {
        "id": "100932",
        "clientLegalEntityName": "Inari Medical",
        "customerID": "100932",
        "clientTermDays": "NET3",
        "preferringBillingCurrencyCode": "USD",
        "mainContact": {
            "primaryEmail": "danielle.braga@inarimedical.com;glebbp@inarimedical.com",
            "clientLegalEntityName": "Inari Medical",
            "contactName": "Danielle++Braga",
            "web": "https://www.inarimedical.com/",
            "busPhone": null,
            "mobilePhone": null,
            "address": {
                "clientBillingAddress1": "Level 19, 181 William Street",
                "clientBillingAddress2": null,
                "clientCity": "Melbourne",
                "clientProvince": "Victoria",
                "clientProvinceCode": "VIC",
                "clientPostalCode": "3000",
                "clientCountryCode": "AU"
            }
        },
        "paymentMethods": [
            {
                "id": null,
                "active": true,
                "description": "GP WIRE",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "GP WIRE",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            },
            {
                "id": null,
                "active": true,
                "description": "GP ACH",
                "isClientDefaultPaymentMethod": true,
                "paymentMethod": "GP ACH",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": true
            },
            {
                "id": null,
                "active": true,
                "description": "HSBCBACS",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "HSBCBACS",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            },
            {
                "id": null,
                "active": true,
                "description": "GPIAT",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "GPIAT",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            },
            {
                "id": null,
                "active": true,
                "description": "HSBCSEPADD",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "HSBCSEPADD",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            },
            {
                "id": null,
                "active": true,
                "description": "MAXQACH",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "MAXQACH",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            },
            {
                "id": null,
                "active": true,
                "description": "DIR DEBIT",
                "isClientDefaultPaymentMethod": false,
                "paymentMethod": "DIR DEBIT",
                "pmInstanceId": null,
                "clientDefaultPaymentMethod": false
            }
        ],
        "industry": "Medical Devices",
        "vatRegistrationNumber": null,
        "siloMsaCountryCode": "US",
        "campaignCode": null,
        "isPartner": true
    }
}
```