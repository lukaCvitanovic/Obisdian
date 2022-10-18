[[Accounting Service Post Release]]

## Tags:
#job 

## Links:
- [NG-28095](https://globalization-partners.atlassian.net/browse/NG-28095)

## Status
```mermaid
graph TD
	A[Started - 14.10.2022] --> B[No Action on ??? Provinces]
	B --> C[Found all province codes]
```

---

## Describe
- Update countries in [[Classic]] DB that have no provinces with provinces used in [[Workday]]

## Progress
- [x] Create countries JSON with alpha2 code and GP countryId
- [x] Find the ISO province codes
	- Using the [iso-3166-2](https://www.npmjs.com/package/iso-3166-2) npm package
	- For some provinces the ISO code was not found do to non eng. characters in the names
		- [x] Find the correct names for the these provinces
			- Added `name` property for real province name
			- Added code for provinces that are not available with [iso-3166-2](https://www.npmjs.com/package/iso-3166-2) package
- [ ] Extract province codes from Workday
- [ ] Compare Workday province codes with generated ones
- [ ] Test SLQ structure for one province
- [ ] Create a SQL that will be run by migration and will add missing [[Workday]] provinces
	- Would need country code that missing provinces belong to
	- Province code and name of the missing provinces

## Territories
- These territories are associated with existing countries
	- For now they will not be added to the associated countries
	- ``` 
		{ code3: '???', name: 'French Polynesia' }
		{ code3: '???', name: 'Guadeloupe' }
		{ code3: '???', name: 'Guam' }
		{ code3: '???', name: 'Macao' }
		{ code3: '???', name: 'Martinique' }
		{ code3: '???', name: 'Mayotte' }
		{ code3: '???', name: 'New Caledonia' }
		{ code3: '???', name: 'Northern Mariana Islands' }
		{ code3: '???', name: 'La Réunion' }
		{ code3: '???', name: 'Saint Barthelemy' }
		{ code3: '???', name: 'Svalbard' }
- Obsolete
	- No Əli Bayramlı (obsolete) for Azerbaijan
	- No Dəvəçi (obsolete) for Azerbaijan
	- No Xanlar (obsolete) for Azerbaijan
	- Bujumbura (obsolete) for Burundi
	- São Nicolau (obsolete) for Cape Verde
	- Calheta de São Miguel (obsolete) for Cape Verde
	- Nana-Grébizi (obsolete) for Central African Republic
	- Sangha-Mbaéré (obsolete) for Central African Republic
	- Borkou-Ennedi-Tibesti (obsolete) for Chad
	- Ādīs Ābeba (Addis Ababa) for Ethiopia
	- Ash Shāţi' (obsolete) for Libya
	- Yafran-Jādū (obsolete) for Libya
	- Mizdah (obsolete) for Libya
	- Ait Baha (obsolete) for Morocco
	- Ait Melloul (obsolete) for Morocco
	- Rabat Sale (obsolete) for Morocco
	- Comarca de San Blas (obsolete) for Panama
	- Al Ghuwariyah (obsolete) for Qatar
	- Jariyan al Batnah (obsolete) for Qatar
	- Al Jumaliyah (obsolete) for Qatar
	- Chişinău (obsolete) for Moldova, Republic of
	- Lăpuşna (obsolete) for Moldova, Republic of
	- Tighina (Bender) (obsolete) for Moldova, Republic of
	- Kaesong (obsolete) for North Korea
	- Nampho (obsolete) for North Korea
	- Agin-Buryat Autonomous Okrug (obsolete) for Russian Federation
	- Chita Oblast (obsolete) for Russian Federation
	- Ust'-Ordynskiy Buryatskiy (obsolete) for Russian Federation
