[[Accounting Service Post Release]],

# Info And Error Codes Rework

## Tags:
#backlog, #job

## Links:
- [[Info And Error Codes Rework Learned]]
---

Rework the codes in similar style to HTTP status codes

## Motivation
- To add aditional structure to the naming convention of the codes
- To enable easy addition of new codes

## InfoCodes
- Current state:
	- **ASI000 - ASI013** -> general info and info related to local or DB CRUD operations
	- **ASI018 - ASI033** -> Cron job status information
	- ASI034 - ASI038 -> Report information
- New state:
	- **ASI0XX** -> General info and info related to local or DB CRUD operations
	- **ASI1XX** -> Cron job status information
		- Add cron job titles
	- **ASI2XX** -> Report Information

## ErrorCodes
- Current state:
	- **ASE001 - ASE012** -> general errors
	- **ASE020 - ASE028** -> RaaS cron job erros
	- **ASE040 - ASE041** -> aws S3 errors
- New state:
	- **ASE0XX** -> General errors
	- **ASE1XX** -> RaaS cron job errors
	- **ASE2XX** -> aws S3 errors

## Progress
- [x] Modify InfoCodes
	- [x] Replace info codes in the codebase
	- [x] Replace running cron job codes with cron job name codes
	- [x] Add cron job names title into logs
- [x] Modify ErrorCodes
	- [x] Replace error codes in the codebase
