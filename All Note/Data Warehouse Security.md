# Data warehouse Security with 4 Simple Roles

## 1. User Overview

	4 roles for Database Security
	- Developers
	- Analysts
	- Loaders
	- Automation
	  
	  ![[Pasted image 20240530141524.png]]
	  
## 2. Analyst Role

	- Only have select permission the marts
	
	![[Pasted image 20240530141734.png]]
	
## 3. Developers Role

	- Select permission from RAW data, read only, not creating or droping tables
	- In the dev environments, they will have ability to deploy and test, create or drop what ever they want in their own test schema or database
	- Give permission to read production, not every developer should have permission to create, drop, insert data into production

![[Pasted image 20240530142541.png]]


## 4. Automation Role

	- Automation role will handel the production, this role will inherit all of the developer permission and also going to have build and deploy for everything else in production environments
	- If you want certain people to have this admin permission and to do ad-hoc, grant the user permission to this role rather than just giving individual user access. It keeps thins conntrolled for yourself and for your team.
	- Automation role isn't going to have the ability to create or drop RAW data but it can deploy and basically do everthing else

![[Pasted image 20240530143506.png]]


## 5. Loader Role

	- Loader role is going to have full permissions to do everthing in the RAW layer.
	- This helps you make sure that any third party tools or whatever processes you're building won't be able to impact anything in the ANALYTICS layer

![[Pasted image 20240530144010.png]]

