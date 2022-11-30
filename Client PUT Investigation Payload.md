[[Customer Payment GPP Pending In Workday Approved in Platform]]

## Tags:
#job #payload 

## Links:

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
        "id": "000229",
        "clientLegalEntityName": "VAT Sudafrica",
        "customerID": "000229",
        "clientTermDays": "NET3",
        "industry": "Consumer Products",
        "preferringBillingCurrencyCode": "EUR",
        "mainContact": {
            "primaryEmail": "maignantest@test.com",
            "clientLegalEntityName": "VAT Sudafrica",
            "contactName": "Mike Maignan",
            "web": null,
            "address": {
                "clientBillingAddress1": "Address test",
                "clientBillingAddress2": null,
                "clientCity": "city test",
                "clientProvince": null,
                "clientProvinceCode": null,
                "clientPostalCode": "2899",
                "clientCountryCode": "ZA"
            }
        },
        "region": "CWV_EMEA",
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
        "vatRegistrationNumber": null,
        "siloMsaCountryCode": "US",
        "campaignCode": null,
        "isPartner": false
    }
}
```