[[Workday intergration]]

# Schema Validation

## Tags:
#job

---

- Will be done using [[Joi]] in combination with [[nestjs-joi]]
- [ ] Add validation on accounting v2 API to ensure Customer/Client format and Project/Professional format are correct:
	- Do validations need separete unit tests?
	- [x] Customer - 6 numeric
		- [X] Patch for Customer
		- [x] At least one payment methods is set as default
	- [ ] Project - XXXXXX-YY-ZZZ alphanumeric
	- Acceptance Criteria:
		- [X] When accountingv2 customer endpoint invoked Then Validation of schema performed