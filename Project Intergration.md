[[Workday intergration]]

# Project Intergration

## Tags:
#job, #intergration 

## Links:
- [[Project Intergration Bugs]]

---

## Questions
- Do we need to implement doesProjectExist route
	- **Most likely we do**
- How are we going to handle get payloads
	- Do we send a payload with id of an entety
	- Do we send the entety id via param
- Are the bulk requests handeled the same way as the on demand ones
- Into what properties shoul we return the project ID

## Notes
- project.workday.service.spec will change after the Thans PR merges
	- pull new main
- 

## Progress

- [ ] Project Payload Classes
	- [x] Create Project Payload
	- [x] Update Project Payload
	- [ ] Get Project Payload
- [ ] [[Project Mapping]]
	- [x] Project Minimal Mapping
- [ ] Project Serialization
	- [x] Create Project Serialization
	- [ ] Update Project Serialization
	- [x] Get Project Serialization
- [ ] Project Workday Service
	- [x] Create Project Route
	- [ ] Update Project Route
	- [x] Get Project Route
- [ ] Project Validation
	- [x] Create Project Validation
	- [ ] Update Project Validation
	- [ ] Get Project Validation

## To FIx In Accounting Service
- Create mocks for getProject in project folder
	- Replace getProjectResponseMock.ts with .json
- Modified project.service to use. throttler instead of unrestricted requests
- follow Thans instructions for changes
- Add a test for when the doesProfessionalExist is returing false