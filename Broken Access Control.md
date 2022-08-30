[[Secure Coding Basics]]

# Broken Access Control

## Tags:
#coding, #security 

---

## Overview
- 94% of sites have broken access controll
- Notable CWEs (Common Weaknes Enumerations):
	- CWE-200: Exposure of sensitive information to unauthorized actor
	- CWE-201: Exposure of Sensitive Information Through Sent Data
	- CWE-352: Cross-Site Request Forgery

## Description
- Access controll enforces rules so that users can't act outside their permissions
- **Failures result in**:
	- Unauthorized info disclosure
	- Modification or destruction of all data
	- Performing business function outside user's limits
- **Common vulnerabilities**:
	- Violation of [Principle of Least Privilege](https://www.cisa.gov/uscert/bsi/articles/knowledge/principles/least-privilege#:~:text=The%20Principle%20of%20Least%20Privilege%20states%20that%20a%20subject%20should,should%20not%20have%20that%20right.) or default access denial
		- Instead available to anyone
	- Bypassing access control checks
		- By modifying:
			- URL
			- Internal application state
			- HTML
		- By using attack tool
	- Allowing viewing or editing somebodies account
	- Elevation of privilege
		- Eg:
			- Acting as a user when logged out
			- Acting as and admin when logged in as a user
	- Metadata manipulation:
		- Replaying or modifying JWT, cookie
		- Hidden field manipulation
		- Abusing JWT invalidation
	- Misconfigured CORS allowes unauthorized/unthrusted origins
	- Force browsing
		- To authenitcated pages as an unauthenticated user
		- To privilaged pages as a standard user

## Prevention
- Access control is only effective on thrusted server-side code or server-less API
	- Metadata or access control checks can't be modified
- **Prevention methods:**
	- Except for public resources, deny by default
	- Implement access controll mechanisms once and reuse them thrughout the site
		- Include minimizing CORS
	- Access controll should enforce record ownership
		- Instead of CRUD privilages for all users
	- Domain models should enforce unique application business limit requirements
	- Disable web server directory listing
		- Ensure file metadata (e.g., .git) and backup files are not present within web roots.
	- Log access control failures, alert admins when appropriate (e.g., repeated failures).
	- Rate limit API and controller access
		-  Mitigate automated attack tooling
	- Stateful session identifiers should be invalidated on the server after logout
		- Stateless JWT tokens should rather be short-lived
			- Minimal window of opportunity for an attacker
		- For longer lived JWTs it's follow the OAuth standards to revoke access.
- Devs and QAs should include access controll unit tests

## Attact Examples
- **Scenario 1**
	- Application uses user supplied unverified info in SQL that is accessing account information
	- ![[Screenshot 2022-04-22 at 11.45.32.png]]
	- By modifying the `acct` parameter it is possible to send any account number
		- If not verified, this will grant access to the account
- **Scenario 2**
	- Force browsing to page that requires admin rights
		- If unauthorized or non-admin user can access the page it is a flaw