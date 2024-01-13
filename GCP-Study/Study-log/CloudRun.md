### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


Cloud Run is a serverless compute platform that allows us to test and deploy containers
and containerized applications effortlessly.

It's a fully managed service that abstracts away the underlying infrastructure so
you can focus on developing your applications.

Another significant advantage of Cloud Run is its portability.
As applications are packaged as containers, developers can develop and test locally,
and deploy them consistently across multiple environments from development to production.

Oftentimes, you should help your company to choose the right compute service in the cloud.

Choosing the right service is the most important thing to get the most out of the cloud.

With Cloud Run, you are only charged for your actual compute resources consumed.

Cloud Run is a versatile serverless platform that can be used for a variety of use cases in application deployment.

Here are some common use cases for Cloud Run:

1) Cloud Run is ideal for hosting web applications including single page applications,
and traditional server rendered applications.

It automatically handles scaling based on incoming requests.

You can deploy APIs and microservices as Docker containers on Cloud Run.

You can deploy containerized data processing tasks and ETL jobs on cloud Run,
allowing you to process data in scalable and cost-efficient manner.

2) Build event-driven applications by deploying functions as containers on Cloud Run.

Trigger these functions in response to events from various sources like Pub/Sub,
Cloud Storage, or Fire Store.


* How to get started with Cloud Run service

1) Go to Cloud Run by using the search bar on console.

2) Click Create Service and from the Deploy one revision from an existing container image,
select TEST WITH A SAMPLE CONTAINER option.

3) Leave other options as default except for the last:

Click on Allow authenticated invocations in Authentication section.

4) That's how simple it is to create a Cloud Run service.

----------------------------------------

5) Get the GitHub clone url, go to the terminal, and create a directory:

https://github.com/LinkedInLearning/learning-google-cloud-run-4480368.git

mkdir docker-scripts
cd docker-scripts
git clone https://github.com/LinkedInLearning/learning-google-cloud-run-4480368.git

6) Git checkout 03_02 or git switch 03_02.

There you will see a docker file among many.

A command to create a new docker image is the following:

docker build -t nginx-demo .


7) Once done, go to Google Cloud console and go to Artifact Registry.

Click on the + plus icon and create a new repository.

Name: cloudrun-demo
Format : Docker

You can leave any other option as they are.
But select the region of your choice.

Leave all the other settings as default and click create.

8) Click on the repo and click on the 'SET UP INSTRUCTIONS' above and copy the code.

Go back to your terminal and run this.

After running this successfully, go back to your console and copy the artifact repository, the whole part that you see when you click on the repo.
(Including location, project ID, and the actual repository name.)


9) Go to console and run this:

docker images

You may check nginx-demo that you have created.

To tag that with the repository name, the command is:

docker tag nginx-demo [the whole info you copied + / your new docker image name]

10) To push this newly created docker image to the remote artifact repository:

docker images

Check the image name.

Copy the the image name.

docker push [image repository/project ID/docker image name]


11) Once done, you will see a new sha-.... and get the prompt back.

In the console, you will see the image pushed to the remote Artifact Repository.

With the docker image pushed to the Artifact Repository, now you can deploy that into the Cloud Run service.

12) Go to the console and to the Cloud Run service.

Click Create service and, for the existing container image, select the one you previously created.

Change the Container Port from 8080 to 80 as nginx runs by default on port 80.

Allow unauthenticated invocations and leave the rest of the fields as default.
 
13) Once the green tick appears, your service is up and running, ready to take the traffic.

14) For every service you created, you get the unique url.

15) Open an incognito window and paste the url.



Here are some key settings you might adjust when deploying a service on Cloud Run.

You need a container image url that specifies the docker container image
that contains your application code and dependencies and it should be hosted in the Artifact Registry,
which is accessible to Cloud Run.

So always push the docker image to the Artifact Registry so that it is easily accessible to select the url
when creating a service on Cloud Run.














