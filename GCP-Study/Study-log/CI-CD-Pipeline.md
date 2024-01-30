### [Source of this study material : Google Cloud Professional DevOps Engineer Certification by Ankit Mistry](https://www.udemy.com/course/gcp-google-cloud-professional-devops-engineer-certification/)


## How to create  a CI/CD pipeline using Cloud Source Repository and Cloud Run


- First, go to Cloud Source Repository and create a repository.


![cloud-source-repo](/GCP_pictures/Study-logs/CI-CD-Pipeline/cloud-source-repository.PNG "Cloud Source Repository - repository creation")


- After creating a repo, you will get this screen giving command instructions on how to clone the git repo to your Google Cloud SDK. 


![after-repo-creation](/GCP_pictures/Study-logs/CI-CD-Pipeline/after-repo-creation.PNG "After repo creation")


- Go back to your Cloud Shell and create 3 files inside the proper folder. (make a folder to clone your repo to!)


- Then, prepare 3 files:

  - **main.py**

```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Welcome to Python Flask world v2.0'


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```


  - **Dockerfile**

```
FROM python:3.9-slim
RUN pip install flask
WORKDIR /myapp
COPY main.py /myapp/main.py
CMD ["python", "/myapp/main.py"]
```


  - **cloudbuild.yaml**

```
steps:
#Build the container image
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/my-vpn-router-project/yejin-test', '.']
#Push the container image to Artifact Registry
- name: 'gcr.io/cloud-builders/docker'
  args: ['push', 'gcr.io/my-vpn-router-project/yejin-test']
#Deploy container image to cloud run
- name: 'gcr.io/google.com/cloudsdktool/cloud-sdk'
  entrypoint: gcloud
  args: ['run', 'deploy', 'yejin-test-run', '--image', 'gcr.io/my-vpn-router-project/yejin-test', '--region', 'us-central1', '--allow-unauthenticated']
- name: 'gcr.io/google.com/cloudsdktool/cloud-sdk'
  entrypoint: gcloud
  args: ['beta', 'run', 'services', 'add-iam-policy-binding', '--region', 'us-central1', '--member', 'allUsers', '--role', 'roles/run.invoker', 'yejin-test-run']
images:
- gcr.io/my-vpn-router-project/yejin-test
```


- Now, grab the 'clone code' we've seen in the Cloud Source Repository and run that on the Cloud Shell:


![clone-command](/GCP_pictures/Study-logs/CI-CD-Pipeline/clone-command.PNG "Clone command")


- In my case, the 3 files are in the other folder. So I'll copy the files to the repo-5 which we intend to push our code to.


![cp-files](/GCP_pictures/Study-logs/CI-CD-Pipeline/cp-files.PNG "Copy files to the directory")


```
cp *.* /home/roinashin/devops/cicd-pipeline/repo-5

cp Dockerfile /home/roinashin/devops/cicd-pipeline/repo-5
```

- We have 3 files in repo-5. Now run the git commands to add and commit all the files to the remote repo.


![git-commands-shell](/GCP_pictures/Study-logs/CI-CD-Pipeline/git-command-shell.PNG "Git commands in the Cloud Shell")


```
git status

git add --all

git commit -m "your message"

git push origin master
```


- Go back to your Cloud Source Repository and refresh. You will see all 3 files pushed to the remote repo.


![git-remote-repo](/GCP_pictures/Study-logs/CI-CD-Pipeline/git-remote-repo.PNG "Cloud Source Repository with 3 files pushed")


- Now, go to Cloud Build and click Create Trigger. There, choose the repo you want to connect your trigger with, and go with the cloudbuild.yaml method.


![cloud-build-trigger](/GCP_pictures/Study-logs/CI-CD-Pipeline/cloud-build-trigger.PNG "Cloud Build Trigger creation")


- First, you need to manually run the trigger to see if it's working. Otherwise, you will have to push some code changes to your repo first. That will only automatically run the trigger and eventually create Cloud Run service.


![manual-run-trigger](/GCP_pictures/Study-logs/CI-CD-Pipeline/manual-trigger-run.PNG "Manually run the trigger")


- Go to Cloud Build History to see how the cloud build is running. Go inside the particular build you are interested in.


![cloud-build-history](/GCP_pictures/Study-logs/CI-CD-Pipeline/cloud-build-history.PNG "Cloud Build History")


- If an error occurs, look for the error inside the Build Details. Try to debug it by following the instructions the error messages give.


![error-debugging](/GCP_pictures/Study-logs/CI-CD-Pipeline/error-debugging.PNG "Error debugging")



- After debugging, you have to go through the same process of git commit and push to the remote repo. This time, the change will trigger the Cloud Build to process the change automatically.


![build-in-process](/GCP_pictures/Study-logs/CI-CD-Pipeline/build-processing.PNG "Build in process")


- This time, it is done successfully.


![successful-build](/GCP_pictures/Study-logs/CI-CD-Pipeline/successful-build.PNG "Successful build")


- Other bugs can happen with the permission settings of Cloud Build. If anything comes up in relation to permissions, look for the issues in the Cloud Build Settings as well.


![debugging](/GCP_pictures/Study-logs/CI-CD-Pipeline/other-debugging-issue.PNG "Other debugging method")


- Finally, go to Cloud Run section and also check if the Cloud Run service is working fine.


![check-cloud-run](/GCP_pictures/Study-logs/CI-CD-Pipeline/cloud-run-check.PNG "Cloud Run check")


- It's working fine. :)


![working-fine](/GCP_pictures/Study-logs/CI-CD-Pipeline/working-fine.PNG "Working fine!")



