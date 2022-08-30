[[Submit Project Bugs]]

# doesProjectExist Throwing An Error

## Tags:
#job #intergration #bugs 

---

# Description
- WorkdayApiService throws the validation error for the provided professional
	- The error indicates that the professional doesn't exist which is expected and should be cought
		- but results is being logged in new relic (expected)
- [[Classic]] displays following error
	- ![[image.png]]
	- This error is also logged in new relic

## Workings Out
1) workday getProject is sent with `professionalId` = `000029-AR-101` to [[Workday]]
	- **Assumption: doseProjectExist is being called**
	- This is evident from the error
	- Means that the `doesProjectExist` method is called with `professionalId` = `000029-AR-101`
		- `noProjectErrorMessage` is then =`'000029-AR-101' is not a valid ID value for type = 'Project_ID'`
		- This string is found in the error message that should be cought
		- The error message is categorized as `Validation` error by `workday-api.error`
2) **getProject is called instead of the doesProjectExist** 
	- Would result in the same workday request
		- Explaines the **same error message** and why it is **not being cought**
	- Reason for happeing is if the `IFeatureService.ACUMATICA_UPGRADE_21R1` is disabled
	- **Does not explain the other requests that have passed sucessfuly**
	- **Enviroment has the neccessary flag set so the doesProjectExsit is called**
3) doesProjectExist pefromed as expected, bug is in the payload that is being send
	- Since the JS to XML conversion is failing
		- Need to see the payload (NewRelic logs)
	- **This would explain why previous fixes didn't have an effect**
		- Was trying to fix the wrong thing
		- NewRelic logs show that `doesProejctExist` enpoint worked as expected
			- The `postProject` method was started and created JS to XML conversion error
		- **Error repoduces locally**
	- Mapping for `Location_ID` was wrong
		- value: `LOC_undefiend`
			- issue with mapping the country or province
		- GPP payload has `Work Country`: `Hong Kong (China)`
			- i18n-iso-countries couldnt map to 2-letter ISO country code
				- **CAUSE OF THE BUG**

## Fix
- Get country code from professionalAccountingId
	- Do the mapping since some of the gp country codes are not the ones from the ISO alpha 2 codes
		- Since `home_address` is sayed to be the real address of the professional modify the `generateAccountingId` method in [[Classic]] to that ti pulls the country code from the `home_address`
			- To prevent the repeting of the [[Location Province Mismatch]] bug
				- **This effects the above mentioned bug in a way of fix implementation**
			- **Make sure this change is approved**
	- FYI there is **Caribbean Netherlands, code: AN** that doesn't have and ISO country code, but does have it in GP platform