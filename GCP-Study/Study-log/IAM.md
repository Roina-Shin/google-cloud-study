### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)

## Identity and Access Management (IAM)

- IAM is all about **authentication** and **authorization**.

- Authentication: is it the right user?

- Authorization: do they have the right access?

- **Identities** can be:

  - A GCP user (Google account or externally authenticated user)

  - A group of GCP users

  - An application running in GCP

  - An application running in your data center

- IAM provides very granular control:

  - Limit a single user:

    - to perform a single action

    - on a specific cloud resource

    - from a specific IP address

    - during a specific time window


## Cloud IAM Example

- I want to provide access to manage a specific cloud storage bucket to a colleague of mine:

  - **Member**: my colleague

  - **Resource**: specific cloud storage bucket

  - **Action**: upload/delete obejcts

- Google Cloud IAM

  - **Roles**: a set of permissions (to perform specific actions on specific resources)

  - How do you assign permissions to member?

    - **Policy**: a policy is something you would use to assign (or bind) a role to a member

  - **Members**: members are also called as **principal**



- Choose a role with the right permissions (e.g. Storage Object Admin)

- Once you choose the role, create a policy to bind the member with the role


## IAM - Roles

- Roles are permissions:

  - Perform some set of actions on some set of resources.

- 3 Types of Roles

  - **Basic roles** (or Primitive roles): Owner/Editor/Viewer

    - Viewer(roles.viewer): you can do read-only actions on all the resources

    - Editor(roles.editor): viewer + edit actions

    - Owner(roles.owner): editor + manage roles and permissions + billing

    - Not recommended: Don't use in production


  - **Predefined roles**: fine grained roles managed by Google

    - e.g.: Storage Admin, Storage Object Admin, Storage Object Viewer, Storage Object Creator


  - **Custom roles**: when predefined roles are not sufficient, you can create your own custom roles


![role-and-permissions](/GCP_pictures/Study-logs/IAM/role-permissions.PNG "Role and its permissions")


- Pick up a role and see what permissions it has.


 ### Important Cloud Storage Roles:

  - **Storage Admin** (roles/storage.admin)

    - storage.buckets

    - storage.objects

  - **Storage Object Admin** (roles/storage.objectAdmin)

    - Sotrage.objects

  - **Storage Object Creator** (roles/storage.obejctCreator)

    - storage.objects.create


## Playing with IAM

- Go to the cloud shell and run:

```
gcloud config set project [project-id]
```

- To list active accounts:

```
gcloud auth list
```

- To see a member and a role in a specific project:

```
gcloud projects get-iam-policy [project-id]
```

- To give a user a specific role:

```
gcloud projects add-iam-policy-binding [project-id] --member=user:gatsbyflight@gmail.com --role=roles/objectAdmin
```


![add-member-assign-role](/GCP_pictures/Study-logs/IAM/add-member-assign-role.PNG "Add a member and assign a role to him/her")


- To remove the IAM policy binding you just assigned:

```
gcloud projects remove-iam-policy-binding [project-id] --member=user:gatsbyflight@gmail.com --role=roles/storage.objectAdmin
```

- To see the permissions a specific role has:

```
gcloud iam roles describe roles/storage.objectAdmin
```


![describe-iam-role](/GCP_pictures/Study-logs/IAM/describe-role.PNG "Describe an IAM role")


- To copy a role to the other custom role in another project:

```
gcloud iam roles copy --source=roles/storage.objectAdmin --destination=my.custom.role --dest-project=[another project id]
```

## Getting started with Service Accounts

- Scenario: an application on a VM needs access to cloud storage.

- You don't want to use personal credentials to allow access.

- The recommended approach is using a **service account**.

- A service account is identified by an email address (e.g. id-compute@depveloper.gserviceaccount.com)

- When we created App Engine or Compute Engine services, service accounts are automatically created.

- There's no password associated with the service account. Service accounts use a **private/public RSA key-pairs**.

- You have to assign a service account to a machine to use it. Then the machine will make a call to the appropriate service.


 ### The types of service accounts

 - **Default accounts**: automatically created when some services are used.

   - Not recommended as it has an editor role by default.

 - **User managed**: User created service accounts.

   - Recommended as it provides fine grained access control.


## Playing with Service Accounts

- This time, we wil create a service account to be assigned to a VM so that the VM can create a bucket in Cloud Storage.


![create-a-service-account](/GCP_pictures/Study-logs/IAM/create-service-account.PNG "Create a service account")


- Go to Service Accounts tab and click Create Service Account.

- Select the roles that the service account needs to be assigned with:


![service-account-roles](/GCP_pictures/Study-logs/IAM/service-account-role.PNG "Assign roles to the service account")


- Grant users access to the service account. This is important as this allows a user to create a VM using this service account. In other words, to be able to create a VM using the service account, you need to have at least a **service account user's role**.


![grant-service-account-user-role](/GCP_pictures/Study-logs/IAM/grant-users-access.PNG "Grand a user access to the service account")


- We are using a free tier account which gives us an owner role. So we don't need to give ourselves a service account user's role or admin's role in this particular case.

- Once done, create a VM. When creating it, use the service account you created with the right permissions (e.g. bucket creation, compute instance admin, etc.)


![vm-creation-service-account](/GCP_pictures/Study-logs/IAM/vm-creation-service-account.PNG "A VM created using the service account")


- Once created, SSH into the VM.

- From the VM instance, we want to create a bucket.

- We can make use of the command:

```
gsutil mb gs://yejin-bucket-1
```

![create-bucket-with-vm](/GCP_pictures/Study-logs/IAM/create-bucket-in-vm.PNG "Create a bucket with a VM")


- When you go to Cloud Storage, you can check if the bucket is created.


![bucket-created](/GCP_pictures/Study-logs/IAM/bucket-created.PNG "Bucket created")


 ### Service Account Scenarios

| Scenario | Solution |
| ------ | ----------- |
| Application on a VM wants to talk to a Cloud Storage bucket   | Configure the VM to use a Service Account with right permissions |
| Application on a VM wants to put a message on a Pub Sub topic | Configure the VM to use a Service Account with right permissions |
| Is service account an identity or a resource?    | It is both. You can attach roles with service account (identity). You can also let other members access a SA by granting them a role on the service account (resource). |
| VM instance with default service account in Project A needs to access Cloud Storage bucket in Project B    | In Project B, add the service account from Project A and assign Storage Object Viewer permission on the bucket. |

