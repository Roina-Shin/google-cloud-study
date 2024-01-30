### [Source of this study material : Google Cloud Professional DevOps Engineer Certification by Ankit Mistry](https://www.udemy.com/course/gcp-google-cloud-professional-devops-engineer-certification/)


## How to Push a Docker image to Artifact Registry

- First, we need an application file and a Dockerfile to create a Docker image.

  - server.js

  - Dockerfile


- **server.js**

```
var http = require('http');
var handleRequest = function(request, response) {
  response.writeHead(200);
  response.end("<h1>Hello world from yejin</h1>");
}
var www = http.createServer(handleRequest);
www.listen(8080);
```

- **Dockerfile**

```
FROM node:21-alpine2.18
EXPOSE 8080
COPY server.js
CMD node server.js
```  

- To create a Docker image, run the command:


```
docker build -t myfirstapp:v1.0 .
```


![docker-image-build](/GCP_pictures/Study-logs/artifact-registry/docker-image-build.PNG "Docker image building command")


- Run 'docker images' to see the image you created.

```
docker images
```


- After that, you need to create an Artifact Registry repository before proceeding with the push of the image to the repo. Go to Artifact Registry and click create repository.


![artifact-repo-creation](/GCP_pictures/Study-logs/artifact-registry/artifact-repo-creation.PNG "Artifact Registry repository creation")


- Go inside the repository you created and copy the route. The format is like this:


```
us-central1-docker.pkg.dev/my-vpn-router-project/myapp
```

And this should also be the image tag name to actually push your image to the Artifact Registry.


- Go back to your Cloud Shell and run the command to actually tag your original image (myfirstapp) to the **repository + imagename:version**. This will make sure to push the image to the right Artifact Registry repository:


```
docker tag myfirstapp:v1.0 us-central1-docker.pkg.dev/my-vpn-router-project/myapp/myfirstapp:v1.0
```


![docker-image-tagging](/GCP_pictures/Study-logs/artifact-registry/docker-image-tagging.PNG "Docker image tagging")


- Then, run the command to push your image to the Artifact Registry:


```
docker push us-central1-docker.pkg.dev/my-vpn-router-project/myapp/myfirstapp:v1.0
```


![docker-image-pushed](/GCP_pictures/Study-logs/artifact-registry/docker-image-pushed.PNG "Docker image pushed")


- If you go to Artifact Registry and look inside the repo, you will see that the image is pushed to the repo:


![image-pushed-to-AR](/GCP_pictures/Study-logs/artifact-registry/image-pushed-to-ar.PNG "Image pushed to the Artifact Registry")


- If you are getting an error with the above commands, first proceed with this configuration command:


```
gcloud auth configure-docker us-central1-docker.pkg.dev
```

