### [Source of this study material : Google Cloud Professional Security Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-cloud-security-engineer-certification/)


## Resource Hierarchy in GCP


![resource-hierarchy](/GCP_pictures/Study-logs/resource-hierarchy/resource-hierearchy.PNG "Resource hierarchy")



## Resource Hierarchy Demo


- Go to GCP console and click IAM. Go to **Manage Resources**.


![iam-manage-resources](/GCP_pictures/Study-logs/resource-hierarchy/iam-manage-resources.PNG "IAM Manage Resources")


- And important thing here is, you **should log in** the GCP at the organization level, not the project level.


- Or, you don't have sufficient permission to assign a **Folder admin** role to you, even as an owner.


- So before proceeding with the folder creation, be sure to give the **Folder Admin** role to your account.


![folder-admin](/GCP_pictures/Study-logs/resource-hierarchy/folder-admin-role.PNG "Folder Admin role")


- Now, you have sufficient permission to create a folder within your organization. Go ahead and create it.


![folder-creation](/GCP_pictures/Study-logs/resource-hierarchy/folder-creation.PNG "Folder creation")


- A new folder is created.


![new-folder](/GCP_pictures/Study-logs/resource-hierarchy/devops-folder.PNG "Devops folder")


- Also, you can move projects under the folder by clicking three dots.


![move-projects](/GCP_pictures/Study-logs/resource-hierarchy/move-projects.PNG "Move projects")


- Now, everything is organized in this organization hierarchy.


![organized-hierarchy](/GCP_pictures/Study-logs/resource-hierarchy/organized-hierarchy.PNG "Organized hierarchy")


