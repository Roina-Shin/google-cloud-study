### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)


## App Engine

- App Engine is the simplest way to deploy and scale your applications in GCP.

- It supports Go, Java, .NET, Node.js, PHP, Python, Ruby using pre-configured runtimes.

- App Engine has very good connectivvity with other Google Cloud services including:

  - Google Cloud Storage products (Cloud SQL etc)

- App Engine supports automatic load balancing & auto scaling.

- App Engine provides **versioning of your application** - so you can have traffic splitting.


## App Engine Environments

- Standard App Engine

  - In Standard App Engine, applications run in language-specific sandboxes.

  - V1: Java, Python, PHP, Go (older version)

  - V2: Java, Python, PHP, Node.js, Ruby, Go (newer version - Google recommended)

- Flexible App Engine

  - In Flexible App Engine, application instances run within Docker containers.
  
  - Supports ANY runtime for Python, Java, Node.js, Go, Ruby, PHP, or .NET.


## App Engine Structrue


![app-engine-structure](/GCP_pictures/Study-logs/AppEngine/Structure-of-App-Engine.PNG "App Engine Structure")


- You can create only one App Engine application per project.

- Underneath your application, you can have multiple microservices.

- Within a service, you can have multiple versions. Version is nothing but a different set of code and configuration.

- Each version can run in one or more instances.


## Deploy an App Engine Service


- To deploy an App Engine app, you need some service and configuration files.


- Find the App-Engine folder inside the Study-log and put these files inside your App Engine project's (You need a dedicated project for App Engine to delete immediately after the demo finished) Cloud Shell Editor folder like below:


![app-engine-files](/GCP_pictures/Study-logs/AppEngine/app-engine-files.PNG "Files required for App Engine Demo")


- In the Cloud Shell terminal, cd into the directory where your App Engine files are.

```
/home/roinashin/Ranga/app-engine/default-service
```

- Once done, run the commands:

```
gcloud config set project [project-ID]

gcloud app deploy
```

- 'gcloud app deploy': As all the files including *app.yaml* are on the present folder, you don't need to worry about adding the file names.


![gcloud-app-deploy](/GCP_pictures/Study-logs/AppEngine/gcloud-app-deploy.PNG "gcloud app deploy")


 ### What happens in the background while deploying App Engine?

  - When you 'gcloud app deploy', a deployment package is created.

  - The deployment package is stored in the Cloud Storage buckets.

  - The C/I C/D tool, **the Cloud Build** needs to access the package in the Cloud Storage.

  - When the deployment is successful, you will see the uri in the Cloud Shell message that says the service is deployed to that uri.


  ![app-engine-service-deployed](/GCP_pictures/Study-logs/AppEngine/app-engine-service-deployed.PNG "App Engine Service deployed!")



 ### To see the app version in Cloud Shell terminal


  ![see-app-version](/GCP_pictures/Study-logs/AppEngine/gcloud-app-list-commands.PNG "See App service and version list in Cloud Shell terminal")


  - To create a new version of the service, modify your main.py file like below so that we can test it.


  ![make-change-so-version-changes](/GCP_pictures/Study-logs/AppEngine/make-change-so-version-changes.PNG "Make a change so that the version changes")


  - Then run the command like below:

  ```
  gcloud app deploy --version=v2
  ```

  - If you deploy without the version name, the version label will be automatically assigned. But you can take control of it by specifying the version as 'v2'.


  ![now-version-changed](/GCP_pictures/Study-logs/AppEngine/now-version-changed.PNG "The version changed when we refresh the page")


  - Then when you run 'gcloud app versions list' again, you will see 2 versions available.


  ![gcloud-app-versions-list](/GCP_pictures/Study-logs/AppEngine/gcloud-app-versions-list.PNG "Run gcloud app versions list")


  - To see the URI of your app, you typically run this:

  ```
  gcloud app browse
  ```  

  - But this will give you only active version which gets all the traffic now. To see the previous version of your app, you need to specify the version as well:

  ```
  gcloud app browse --verion=20240115t010018
  ```

  - Then you are going back to the older version of your service.


 ### Split traffic into multiple versions

  - Sometimes, you want to slowly move the traffic to a newer version while maintaining certain amount of traffic to the older version.

  - Go back to the Cloud Shell Editor and make a new change. Only change the version of your app like below and save.


  ![create-app-v3](/GCP_pictures/Study-logs/AppEngine/make-app-v3.PNG "Create an app v3 for splitting test")


  - Because we are NOT ready to give all the traffic to the version3, we will just deploy it without sending any traffic to it:

  ```
  gcloud app deploy --version=v3 --no-promote
  ```

  - **'--no-promote'** is the option where you deploy a new version without switching traffic to it.


  - You can test your v3 by running this:

  ```
  gcloud app browse --version=v3
  ```

  - To send some traffic to each version of the service:

  ```
  gcloud app services set-traffic --splits=v3=.5,v2=.5
  ```


  ![gcloud-app-services-set-traffic-splits](/GCP_pictures/Study-logs/AppEngine/gcloud-app-services-set-traffic-splits.PNG "gcloud app services set-traffic --splits=v3=.5,v2=.5")


  - And you will see in the Cloud Shell message above, that the **'Splitting traffic by ip'**. As we are sending the requests to the page using the same IP, it will only show the same version of the app in the uri we are testing.

  - So run this again:

  ```
  gcloud app services set-traffic --splits=v3=.5,v2-.5 --split-by=random
  ```

  - And refresh the **v2** page multiple times, and you see the versions change each time.

  - If you are done with your test and ready to send all the traffic to v3, then run this command:

  ```
  gcloud app services set-traffic --splits=v3=1
  ```

  - You can see the split test result in the Versions panel of App Engine.


  ![version-panel](/GCP_pictures/Study-logs/AppEngine/app-engine-version-panel.PNG "App Engine Versions panel")


 ### Create a new service name


  - This demo works with the folder 'App-Engine-My-First-Service'.

  - In the Cloud Shell terminal, cd into that folder.

  - As we have a service name included in the app.yaml file like below:


  ![service-name-included](/GCP_pictures/Study-logs/AppEngine/service-name-included.PNG "Service name included in app.yaml file")


  - We can then deploy the app. Run the following:

  ```
  gcloud app deploy
  ``` 

  - You can see 'my first service' is deployed by entering the uri in the browser.


  ![my-first-service-deployed](/GCP_pictures/Study-logs/AppEngine/my-first-service-deployed.PNG "My first service is dployed")


  - If you go to Services panel of App Engine, you will see 2 services available.


  ![services-panel](/GCP_pictures/Study-logs/AppEngine/app-engine-services-panel.PNG "Services panel of App Engine")


  - This command would do the same to list the services:

  ```
  gcloud app services list
  ```

  - In the Cloud Shell terminal, you can browse the uri of my first service by specifying the service:


  ```
  gcloud app browse --service=my-first-service
  ```

  ![app-browse-my-first-service](/GCP_pictures/Study-logs/AppEngine/app-browse-my-first-service.PNG "gcloud app browse --service=my-first-service")


 
 ### Attach a custom domain to your App Engine service


  - If you want to attach a custom domain to your service, go to App Engine Settings and click Custom Domains. Google will provide a **managed auto-renewing SSL certificate** for security.


  ![custom-domain-app-engine](/GCP_pictures/Study-logs/AppEngine/attach-custom-domain.PNG "Custom domain for App Engine service")


 ### Create a Cron Job at App Engine

  - App Engine allows you to run scheduled jobs at regular intervals.

  - This is usually configured using *cron.yaml*.    


 ### App Engine dispatch.yaml file

  - dispatch.yaml : override routing rules

  ```
  dispatch:
    - url: "*/mobile/*"
      service: mobile-frontend
    - url: "*/work/*"
      service: static-backend
  ```


## Important things to remember

- App Engine is **regional**. You CANNOT change an application's region.

- App Engine is a good option for simple microservices.

- However, App Engine is not as powerful as Kubernetes.

- App Engine Flexible will not scale down to 0 instance. So there will be always one container running when there is no load.

- Go for App Engine Standard if you want to scale down to 0 instance.

- If you want to move your App Engine to a different region, then create a new project and create a new App Engine in that region.

- You can perform canary deployments. Deploy v2 without shifting traffic to it:

```
gcloud app deploy --no-promote
```

- And shift some traffic to v2:

```
gcloud app services set-traffic --splits=v1=.9,v2-.1
```