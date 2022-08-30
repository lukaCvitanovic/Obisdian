[[GP]]

# How To Access Deployed Envs

## Tags:
#job #gp #env

## Links:

---

1) Opden [AWS](https://globalization-partners.awsapps.com/start#/) console with Default accoun
2) Open **Session Manager**
3) **Start** a new session
4) **Filter** for the instance
	- For the shared dev we need **shared-dev_bastion** 
		- Console to that instance is opened

## Access The DB
1) enter `mysql -h <host> -u <user> -p`
	- Find the password in the **Parameter Store**
	- `mysql -h work-uat-gg-classic-db.cqpxjt9uv9fs.us-east-1.rds.amazonaws.com -u sys_goglobal -p`
1) Enter the DB password
2) Enter `use <table_name>` to use the DB table
