# Basic Azure Hardening 

Please create a report upon completion.

## Task 1 - Create a test tenant
- Create the a new tenant with a unique name:
	- Entra ID > Manage Tenants > Microsoft Entra ID 
	- organization name: ```<YOURNAME>lab<RANDOMNUMBER>```
	- initial domain name: ```<YOURNAME>lab<RANDOMNUMBER>```

- Switch to that tenant
	- Using "switch directory"

- Create a new random user (standard user, no specific role assigned)
	- Log as this user
	- Try to list the users

 - Switch back to the admin user

## Task 2 - Enforce basic AD security

- Enforce Azure best practices for users
	- Entra ID > User settings
		- Users can register applications: NO
		- Restrict non-admin users from creating tenants: YES
		- Users can create security groups: NO
		- Guest user access restrictions: Guest user access is restricted... (most restrictive)
		- Restrict access to Microsoft Entra ID administration portal: YES
		- Allow users to connect their work or school account with LinkedIn: NO
		- **Save**
		
		- External users:
			- Guest user access restrictions: Guest user access is restricted... objects (most restrictive)
			- Guest invite restrictions: No one in the organization can invite guest users including admins (most restrictive)
			- Collaboration restrictions: Deny invitations to the specified domains, write ```*``` in the target domains
			- **Save**

- Enforce group settings
	- Entra ID > Groups > General
		- Owners can manage group membership requests in My Groups: NO
		- Restrict user ability to access groups features in My Groups. Group and User Admin will have read-only access when the value of this setting is 'Yes' : YES
		- Users can create security groups in Azure portals, API or PowerShell: NO
		- Users can create Microsoft 365 groups in Azure portals, API or PowerShell: NO
		- **Save**

- Enforce devices settings 
	- Entra ID > Devices > Device settings
		- Users may join devices to Microsoft Entra: None
		- Users may register their devices with Microsoft Entra: None
		- Maximum number of devices per user: 5
		- **Save**

- Enforce Entreprise applications settings
	- Entra ID > Entreprise Applications > Consent settings 
		- Do not allow user consent. 
		-   Do not allow group owner consent
		- **Save**
	- Entra ID > Entreprise Applications > Consent settings > Admin consent settings
		- Users can request admin consent to apps they are unable to consent to​: YES
		- **Save**

- Using the previously created standard account
	- Log as this user
	- Try to list the users

## Task 3 - Streaming sign-in logs

- What are the logging limitations of Entra ID ? 

- Where do you find sign-in logs?

- How to send those logs to an external SIEM?
	- Create an Event Hub
	- Go to Entra > Sign-in Logs > Export Data Settings
	- Create a Splunk instance
		- Get Splunk .deb 
			- https://www.splunk.com/fr_fr/download/splunk-enterprise.html
		- Install it in a VM
		- Install the Splunk Add-on for MS Cloud Services
			- https://splunkbase.splunk.com/app/3110#/details
	- Tips: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-stream-logs-to-event-hub?tabs=splunk

- Using the previously created standard account
	- Log as this user

- Search Splunk to identify the sign-in request
