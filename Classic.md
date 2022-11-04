# Classic

## Tags:
#gp-service, #microservice, #monolith, #legacy, #job, #fullstack

## Links:
[[Classic Errors]]

## About
Legacy Goglobal or classic is the [[monolith]] software solution for [[GP]] that was initialy made. As the name suggests it is [[Legacy code]]. Classic is written in [[Java]]. All other [[GP Service]]s are implemented to serve the classic as it is the main application and the starting point of many of the user flows.

Since all other services are there to support this application, the goal is to make minimal changes to it and migrate all the changes into surounding [[GP Service]]s.

## How Its Made
- There is a Java app that serves as a backend
- There is web app inside the Classic that serves as a frontend
	- Wirtten someting that looks like JS and uses js libs
	- Web app uses [[amplifyjs]]
		- Using the amplifies publish and subscribe the comunication between the web app and Java app is done
		- Comunication relies on events with names stored in enum strictures
			- Each enum property serves as method proxy RSC(Remote Service Call)
			- eg. `amplify.publish(AppEvents.CLIENT_PERSON.SET_TO_MAIN_ACUMATICA_CONTACT, new UiActionEvent(this, ${m.id}));` in the web app
			-  ![[Screenshot 2022-04-15 at 16.53.46.png]]
		- Events are picked up by Java app and mapped to appropriate services

## Migrations
- Migrations are SQL scripts
- They can have execution preconditions
	- Preconditions are SQL that if true runs the migrations otherwise it skips it
	- Preconditions syntax:
		- `--precondition-sql-check expectedResult:<something> <SQL>`
	- There is a migrations command that defines how the migrations is treated if it's not executed
		- `--preconditions onFail:MARK_RAN`
- For migration files to be executed they need to be referenced in corresponding `db.changelog` which itself is referenced in`db.changelog-master`
- Migration files must not be modified or removed in any way
	- **How to make changes to a migration file**
		1) Create a new migration file
		2) Remove original migration reference from `db.changelog` 
		3) Add a reference to a new migration file in `db.changelog`
### Locally Run Migrations
	1) Start the local [[Classic]] instance
	2) Have the `mysql-db` Docker container running
	3) Sync [[Classic]] Java dependencies
	4) Run `mvn liquibase:update -Dliquibase.url="jdbc:mysql://localhost:3306/goglobal?useSSL=false&serverTimezone=America/New_York" -Dliquibase.promptOnNonLocalDatabase=false`
		- If the DB is in container
	- If the command is waiting endlessly for DATABASECHANGELOGLOC then:
		1) Delete all migrations from DATABASECHANGELOG table
		2) Delete corresponding locking in DATABASECHANGELOGLOC table
		
