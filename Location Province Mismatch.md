[[Submit Project Bugs]]

# Location Province Mismatch

## Tags:
#job , #intergration , #bugs 

## Links:
- [NG-18068](https://globalization-partners.atlassian.net/browse/NG-18068)

---

# Description
- eg. LOC_CA_NY
	- CA -> form professional.country_id
	- NY -> from client.billing_address_id
- client and a professional don't have the same address

## FIx
- what is the source of the correct professional adderss in DB since
	- **in DB professional has ?**:
		- [x] home_address_id
		- [ ] home_country_id
- Added feature flag behind which the country and province of the professional is pulled from home_address
	- Originaly the professional country was pulled from ClientCountry
		- If the province was pulled from the home_address the countries will mismatch in 190 cases
	- There are no country mismatches


