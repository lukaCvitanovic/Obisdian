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