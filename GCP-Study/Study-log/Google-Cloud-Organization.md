### [Source of this study material : Google Cloud Professional Security Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-cloud-security-engineer-certification/)


## Google Cloud Identity setup and create GCP free account

- For Cloud Identity Free, you need company's domain name: 


[Cloud Identity Free](https://workspace.google.com/gcpidentity/signup?sku=identitybasic)


- Follow the guided instructions. When you are all done with the domain registration and verification, you will see this UI:


![cloud-identity](/GCP_pictures/Study-logs/GCP-organization/cloud-identity.PNG "Cloud Identity UI")


- When you go to the Users section, you will see that your account is not with the personal email but with the business email.


![company-email](/GCP_pictures/Study-logs/GCP-organization/company-email.PNG "Business email")


- To start using Cloud Identity, now go to GCP console and start creating the account. After sigining in with a new account and setting up the billing account, you are good to go.


![organizational-gcp-account](/GCP_pictures/Study-logs/GCP-organization/organization-gcp-account.PNG "Organizational GCP account")


- The difference is, when you select a project, you will see at the top level your organization.


![organization-level](/GCP_pictures/Study-logs/GCP-organization/organization-level.PNG "Organizational level")



## Add users and create a group

- After successfully attaching our Cloud Identity with the GCP account, go back to the Google Admin page. Here only, you can add users to the group and then, in Google Cloud console, you can assign roles to the group.


![admin-add-users](/GCP_pictures/Study-logs/GCP-organization/add-users.PNG "Add users in Admin page")


- You can add user by clicking the **add new user** button.


![add-new-user](/GCP_pictures/Study-logs/GCP-organization/add-new-user.PNG "Add new user")


- Now, Gatsby is added as a new user. You can **copy the password** for sign-in later.


![gatsby-added](/GCP_pictures/Study-logs/GCP-organization/gatsby-added.PNG "Gatsby added")


- Also, inside the Directory, you can see that the organizational unit can be added like below:


![organizational-unit](/GCP_pictures/Study-logs/GCP-organization/organizational-unit.PNG "Organizational unit")


- You can then go to Users again and select the users per organizational unit.


![select-user-per-unit](/GCP_pictures/Study-logs/GCP-organization/select-user-per-unit.PNG "Select user per organizational unit")


- You can create a group like below:


![create-group](/GCP_pictures/Study-logs/GCP-organization/create-group.PNG "Create a group")


- After creating the group, go to Google Cloud console.


- Go to IAM and click Grant Access.


- Instead of adding individual user emails, you can add the **group email** and provide some roles to the group.


![group-role-assignment](/GCP_pictures/Study-logs/GCP-organization/group-role-assignment.PNG "Group role assignment")


- This way, all members in the group is assigned with the same roles.



## Google Cloud Directory Sync

- Google Cloud Directory Sync helps you synchronize the data in your Google Account with your Microsoft Active Directory or LDAP server.



## SSO with SAML

- SAML: Security Assertion Markup Language


- Generally, Google acts as a **service provider** and **identity provider**.

  - When a user signs in, Google stores credentials on their servers

  - The information includes password, user info, etc.


- But some organizations do not want to use Google authentication. They have their own services for employee identity.


- In that case, the organizations can use SAML (SSO based authentication).


- SSO (Single Sign On) works this way:

  - There is an organization user and identity provider. 

  - When user logs in with the identity provider, only then the user can use the services from the Google Cloud.

  - To implement this, SAML needs to be configured.



