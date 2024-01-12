## How to set a connection between your GCP and GitHub repository

1. First, head over to Cloud Build on your GCP console.

2. Click on Repositories.


![Cloud-Run-Cloud-Build](/GCP_pictures/Cloud-Run-Cloud-Build.PNG "Select 2nd gen to create your repository")


3. Click on Create Host Connection.


![Cloud-Run-Configure-Connection](/GCP_pictures/Cloud-Run-Configure-Connection.PNG "Select region and enter a name that corresponds to your GitHub repo")


4. After selecting a region and entering a name, you will be prompted with an authentication window. Proceed with that and select the GitHub repo you want to connect with GCP.


![Cloud-Run-Select-Repo](/GCP_pictures/Cloud-Run-Select-Repo.PNG "Select only the repo that you want to connect with the GCP")


5. If everything goes fine, you will see the status window like this.


![Cloud-Run-Repo-Connected](/GCP_pictures/Cloud-Run-Repo-Connected.PNG "Connection created")


6. Now, let's link the repository. Click Link Repository and select the connection you created.


![Cloud-Run-Link-Repo](/GCP_pictures/Cloud-Run-Link-Repo.PNG "Link repository")


7. If all is fine, you should see your repository under your connection here.


![Cloud-Run-Repo-Linked](/GCP_pictures/Cloud-Run-Repo-Linked.PNG "Repo linked under your connection")