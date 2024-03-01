### [Source of this study material : GCP Professional Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)


## Getting started with Identity Aware Proxy (IAP)

- what is the easiest way to implement authentication and authorization for your apps deployed in App Engine, Cloud Run, and GKE?


- The answer to that is **Identity Aware Proxy**.


- IAP simplifies implementation and authentication and authorization for your cloud-based and on-premises applications.


- IAP uses **identity** (credentials) and **context** (from where? using what?) to make your authentication and authorization decisions.


- Simpligied integration with App Engine, Cloud Run and GKE.



## Exploring Identity Aware Proxy with App Engine

- First, we will need to deploy an App Engine application.


- **app.yaml**


```
runtime: python39
```


- **main.py**


```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'My Default Service - V1'
```


- **requirements.txt**


```
Flask==3.0.0
```



- Now, you are ready to deploy your App Engine. Deploy it.


```
gcloud app deploy
```


![gcloud-app-deploy](/GCP_pictures/Study-logs/identity-aware-proxy2/app-engine-deploy.PNG "gcloud app deploy")



- Now, your App Engine is deployed.


![app-engine-deployed](/GCP_pictures/Study-logs/identity-aware-proxy2/app-engine-deployed.PNG "App Engine deployed")


- Let's go to the IAM and enalbe Identity Aware Proxy.


![enable-IAP-API](/GCP_pictures/Study-logs/identity-aware-proxy2/enable-iap-api.PNG "enable IAP API")


- Click Configure Consent Screen before using IAP.


![configure-consent-screen](/GCP_pictures/Study-logs/identity-aware-proxy2/configure-consent-screen.PNG "Configure consent screen")


- We will allow external user with a google account to access our app. Then click Create.


![oauth-consent-screen](/GCP_pictures/Study-logs/identity-aware-proxy2/oauth-consent-screen.PNG "OAuth consent screen")


- After adding app name and support email, go to Scopes screen and click **Add or Remove Scopes**.


![add-scopes](/GCP_pictures/Study-logs/identity-aware-proxy2/add-scopes.PNG "Add scopes")


- Now, your client application is ready. 


![client-application-ready](/GCP_pictures/Study-logs/identity-aware-proxy2/app-oauth-consent-ready.PNG "Client application ready")


- Go back to your IAP screen and toggle to enable IAP for the whole APP Engine apps.


![enable-iap-for-app-engine](/GCP_pictures/Study-logs/identity-aware-proxy2/enable-IAP-for-app-engine.PNG "Enable IAP for App Engine")


- If you click on the App Engine URL, you will now get an authorization window and your access will be denied.


![access-denied](/GCP_pictures/Study-logs/identity-aware-proxy2/access-denied.PNG "Access denied")


- You need to map users to **IAP-secured Web App User** role for the project.


- Go to IAM and click owner email and add the role **IAP-secured Web App User**.


![IAP-secured-web-app-user](/GCP_pictures/Study-logs/identity-aware-proxy2/iap-secured-web-app-user.PNG "IAP secured web app user")


- Now, if you go and test the app again, you can access the app this time.


![access-granted](/GCP_pictures/Study-logs/identity-aware-proxy2/access-granted.PNG "Access granted")


- In summary, if you have other services, you can select the service and configure the IAP secured Web App User role for a specific group or user.


![summary](/GCP_pictures/Study-logs/identity-aware-proxy2/summary.PNG)



## How does IAP work?

### Execution Flow

- When enabled, IAP intercepts calls to applications (sits before App Engine, Cloud Load Balancing, etc.)


- If a user is **unauthenticated**, the user is redirected to **OAuth 2.0 Google Account sign-in** flow.


- If a user is already authenticated (valid OAuth token is present with the request), user authorization is verified. This means that the user's IAM role is checked agaianst configured policy for the resource.


- If successful, the user is allowed access to the resource.


- User identity is passed to **backend service** using HTTP headers.


## Using Identity Aware Proxy (IAP) with Kubernetes

- **GKE Cluster**: traffic comes via HTTP(S) Load Balancing (typically configured using Ingress)


### Steps to setup IAP with GKE

1. Create client secret ID AND key


```
kubectl create secret generic my-client-secret from-literal=client_id=CLIENT_ID_KEY --from-literal=cient_secret=CLIENT_SECRET_KEY
```


- The example client ID and the client secret can be found in **API & Services > Credentials**.


![credentials](/GCP_pictures/Study-logs/identity-aware-proxy2/credentials.PNG "Credentials")



2. Configure **BackendConfig** using secret:


```
apiVersion: cloud.google.com/v1
kind: BackendConfig
metadata:
  name: enable-iap
  namespace: my-namespace
spec:
  iap:
    enabled: true
    oauthclientCredentials:
      secretName: my-client-secret
---
metadata:
  annotations:
    beta.cloud.google.com/backend-config: '{"default": "enable-iap"}'
```


3. Configure the Kubernetes Service to use the **BackendConfig**. You can include the **metadata - annotations** to your service YAML:


```
metadata:
  annotations:
    beta.cloud.google.com/backend-config: '{"default": "enable-iap"}'
```


4. Once you do that, the Kubernetes will know that the service is using IAP. Or, you can configure IAP with Anthos Service Mesh. (also uses BackendConfig)

