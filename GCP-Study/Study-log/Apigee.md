### [Source of this study material : API Development with Apigee by Prashant Naik](https://www.udemy.com/course/api-development-with-apigee-x)


## What is API?

- API (Application Programming Interface) makes the developer job easier as he can get the ready made functionality.


- Consider you want to build a map in your website for easy navigation. If you really start building this from scratch, it will take a lot of time.


- In this case, API helps the website developer. He just calls the API which is exposed by other organizations like Google. 


- The proper data is passed like message body, header, etc. while calling the API. These details are defined in the API specification.


- For each API call, the organization charges certain amount of money. And this is defined in the contract betweem API consumer and the provider.


## API Lifecycle

- **These are the lifecycle steps in Apigee**

  - Design

  - Develop

  - Secure

  - Publish

  - Scale

  - Monitor

  - Analytics


## What is Apigee?

- It is a platform to develop and manage APIs.


- It creates a **proxy layer** between backend service and client.


- Client has to call the proxy service to get the services from backend.


- Client is not exposed to backend directly for security reasons.


- Once the proxy receives the request, it validates before passing it to backend service.


![what-is-apigee](/GCP_pictures/Study-logs/Apigee/what-is-apigee.PNG "What is Apigee")


- All the security features are applied at the proxy layer. It will protect backend service from security attacks.


- Apigee makes it easy for developers to consume their APIs.


- Backend service implementation changes will not affect the calling application.


- It provides monitoring, alaytics, and developer portal features.


## Apigee Provisioning

- **Steps to provision Apigee**

  1. Enable the necessary APIs.


  2. Create networks.


  3. Create organization.


  4. Enable access routing.


1. Enable the necessary APIs

- Apigee.googleapis.com (Apigee API)

- Servicenetworking.googleapis.com (Service Network API)

- Compute.googleapis.com (Compute Engine API)


2. Create service networks

- It configures the connection between cloud network and google service (e.g. Apigee)


3. Create organization

- It creates an eval organization and associated runtime instance.

- Organization name should be the same as **Project ID**. (This is to maintain unique name across globe)

- The projects and services are deployed in runtime instance.

- The runtime instance provides the endpoint for the services deployed here.


4. Access routing

- There are 2 options:

  - External access to API proxies

  - Allow requests only within the VPC


- The first option creates an **external static IP** and this can be accessed from outside VPC.

- The second option gives only internal access to the API proxies.

- If access type is **internal**, you can access API proxies by creating a VM insdie the VPC. And from this VM, we can send the requests to the API proxy.


- **These are artifacts created after the Apigee provisioning is done**

  - Organization name

    - It is the same as *Project ID*

  - Instance

    - eval-instance

  - Environment

    - eval

  - Environment group

    - eval-group

  - Hostnames

    - *<Project Name>.eval.apigee.net*

  - IP address

    - It is internal load balancer IP address



## Create Project and Apigee Service

- In the browser, enter **apigee.google.com/setup**.


![apigee-setup](/GCP_pictures/Study-logs/Apigee/apigee-setup.PNG "Apigee setup")


- As it prompts us to enter a project ID, we will first create a project on GCP console.


![create-new-project](/GCP_pictures/Study-logs/Apigee/create-new-project.PNG "Create a new project")


- Copy the project ID and enter it into the apigee setup page. (I changed the project to another one because of a quota error)


![click-evaluation](/GCP_pictures/Study-logs/Apigee/click-evaluation.PNG "Click evaluation")


- As I already enabled the 3 necessary APIs, I'll start with the Networking.


![set-up-apigee-eval](/GCP_pictures/Study-logs/Apigee/set-up-apigee-eval.PNG "Set up Apigee evaluation")


- For network, choose **default** VPC. And go with **automatically allocate IP range** for reserving peering ranges.


![set-up-networking](/GCP_pictures/Study-logs/Apigee/set-up-networking.PNG "Set up networking")


- Then create an Apigee evaluation organization by entering region.


![create-apigee-evaluation-organization](/GCP_pictures/Study-logs/Apigee/create-apigee-evaluation-organization.PNG "Create an Apigee evaluation organization")


- After 30-40 min, the organization is created. Now, configure **Access routing**. Go with **enable Internet access** and use **wildcard DNS service**. 


![access-routing](/GCP_pictures/Study-logs/Apigee/access-routing.PNG "Access routing")


- Then choose default network and click set access.


![choose-default-network](/GCP_pictures/Study-logs/Apigee/choose-default-network.PNG "Choose default network")


- Now, **Access routing** step is also complete. Click continue.


![step-complete](/GCP_pictures/Study-logs/Apigee/step-complete.PNG "Step complete")


- Then if you click apigee console, you will be taken to this page.


![apigee-console](/GCP_pictures/Study-logs/Apigee/apigee-console.PNG "apigee console")


- If you go to Admin - Environment - Groups, you can see the domain address and the hostnames.


![admin-environment-groups](/GCP_pictures/Study-logs/Apigee/admin-environment-groups.PNG "Admin - Environment - Groups")


- The domain address here is **proxy endpoint**, and when you enter the [domain address]/hello-world, it will show the **hello, guest** message in the browser.


![domain-address](/GCP_pictures/Study-logs/Apigee/domain-address.PNG "Domain address")


- And when you see the hello-world revision 1 endpoints, it shows that the [domain address]/hello-world is proxy endpoint and the **https://mocktarget.apigee.net/user** is the target endpoint.


![revision1-endpoints](/GCP_pictures/Study-logs/Apigee/revision1-endpoints.PNG "Revision1 endpoints")


- When you open the mocktarget page, it shows the same page as our [domain address]/hello-world page.


![mocktarget](/GCP_pictures/Study-logs/Apigee/mocktarget.PNG "Mocktarget page")


- So, the API proxy (domain address/hello-world) called the target endpoint and it responded with **hello, guest** message. The target endpoint is a backend service.


## Components of Apigee

### Environment

- Environment is the **runtime context** to deploy API proxies.


- API proxies are in running state once it is deployed to environment.


- Once deployed, it is available to **accept requests** from users.


- API proxy can be deployed in multiple environments.


- Maximum **60 deployments** can be performed in a single environment.


- You can go to Environments - Overview and click create new environment.


![create-new-env](/GCP_pictures/Study-logs/Apigee/create-new-env.PNG "Create a new env")


- Once you created the environment, you can add group. I'll cancel the add so that we can test something in Environment Group section.


![add-group](/GCP_pictures/Study-logs/Apigee/add-group.PNG "Add group to environment")



### Environment Group

- Environments are **grouped** together in Environment Group.


- Hostnames are defined on Environment Groups (Not on Environment).


- It can have multiple Hostnames.


- Hostnames assigned to one Group cannot be assigned to other Groups.


- Apigee **routes** requests to **Environment** (within Group) based on this **Hostname definitions**.


- Users cannot access resources from Environment if it is **not part of Environment Group**.


- So, Environment should be a part of at least **one Environment Group**.


- Grouping the Environments will have the below listed benefits:

  - **Centralized** place to manage Hostnames

  - Help to analyze the report for entire Environment Group

  - Help to avoid **Base path for Environment** to be duplicated for the same Hostname.


- If you go to Environment - Groups, you can see that the environment **development** is not assgined to any group now.


![unassigned-env](/GCP_pictures/Study-logs/Apigee/unassigned-env.PNG "Unassigned env")


- But if we go back to Environment - Overview and add the Eval Group to the Environment, we can see that the both environments are now in Eval Group.


![both-envs-in-group](/GCP_pictures/Study-logs/Apigee/both-envs-in-group.PNG "Both envs are in the same group")


- You can also add a new Environment Group.


![add-env-group](/GCP_pictures/Study-logs/Apigee/add-env-group.PNG "Add a new Environment Group")


![dev-group-created](/GCP_pictures/Study-logs/Apigee/dev-group-created.PNG "Dev group created")



### API Proxy

- API proxies act as **interface** to the developers to access backend services.


- Backend services are secured by using API proxy.


- All the **security and rate limiting** policies are applied to the API proxy before passing it to Backend.


- In this type of architecture, the backend service URL is not shared with the consumers and consumers must **hit the API proxy** to get the service from the backend.


- Any changes to the backend service will not affect the consumers as the services are exposed through **proxy endpoints**.


- Consumers are unaware of the backend service changes, for example, changes in the database.


- API tools provide **out of the box policies** to apply on the API proxies. e.g. Authentication



### API Product

- It is a **collection** of API proxies and with quota settings.


- It helps to bundle **related API proxies** in one API product.


- The developer can subscribe to required **API product** and the **plan**.


- The developer **should create an app** to subscribe to the product.


- Developers can subscribe to **multiple products** using the same App.


- Apigee has provided **Developer portal** to register and create App for the developers.



### Developer

- Developer is an entity which is uniquely identified by **email address**.


- Apigee provides 2 types of solutions to the developers:

  - Self service:

    - Here the developer **register himself** in the developer portal

    - Create an App

    - Subscribe to the API products with the suitable rate plan

  - Manual service:

    - Here the API team creates the Developer and Apps in the Apigee management UI



### Developer Portal

- In Developer Portal, API developers list their APIs, and the same can be utilized by App developers.


- These are the details available in the portal:

  - API documentation

  - What kind of data the API receives, and what kind of data it responds back

  - What are the operations (GET, POST, PUT, DELETE) supported

  - Sample data to test and analyze the API

  - OpenAPI specification details

  - Rate plan to use the APIs


- Apigee provides these 3 developer portal solutions:

  - Apigee integrated portal

  - Drupal 9 modules

  - Do-it-yourself


- For our demo, we will use Apigee integrated portal.


- In Apigee main page, click Portals.


![apigee-main-portals](/GCP_pictures/Study-logs/Apigee/apigee-main-portals.PNG "Apigee main portals")


- Click get started.


![get-started](/GCP_pictures/Study-logs/Apigee/click-get-started.PNG "Click get started")


![create-portal](/GCP_pictures/Study-logs/Apigee/create-portal.PNG "Create a portal")


- Now, you can see the Devportal is created. This is the admin UI where you can manage tasks.


![devportal-created](/GCP_pictures/Study-logs/Apigee/devportal-created.PNG "Devportal created")


- Click Live Portal and you will see this page. 


![live-portal](/GCP_pictures/Study-logs/Apigee/live-portal.PNG "Live Portal")


- To sign in the **Live Portal**, you need to create an account. Click **Sign In** at the top right side of the page and click create account.


![sigin-in-live-portal](/GCP_pictures/Study-logs/Apigee/sign-in-live-portal.PNG "Sign in Live Portal")


- Create an account.


![create-account](/GCP_pictures/Study-logs/Apigee/create-account.PNG "Create an account")


- Check your inbox to complete the sign up process.


![check-inbox](/GCP_pictures/Study-logs/Apigee/check-inbox.PNG "Check inbox")


- Once done, activate the Live Portal again. And sign in.


![sign-in-again](/GCP_pictures/Study-logs/Apigee/sign-in-again.PNG "Sign in again")


- Now, you are logged in as a developer.


![log-in-complete](/GCP_pictures/Study-logs/Apigee/log-in-complete.PNG "Log in complete")


- If you check the Apigee Devportal - Accounts, you will see that the user is registered.


![devportal-account-user](/GCP_pictures/Study-logs/Apigee/devportal-accounts-users.PNG "Devportal account user")


### Understand the Flows in API Proxy

- **Flows** are the major part of the API proxies.


- Using Flows, you can configure the **behavior of the API** by applying **policies** at the right place.


- During processing of requests, different kinds of **Flows** execute with **policies** attached to it.


- Following are the different types of Flows:

  - Pre Flow

  - Conditional Flow

  - Post Flow

  - Post Client Flow


- When we are working with API proxy, let's divide API proxy into 2 parts:

  - One part is the API proxy which is exposed to client

  - Other part is to connect to the backend service and get the required data/information


- The first part is called **Proxy Endpoint**.

- The second part is called **Target Endpoint**.


- **Proxy Endpoint**

  - It can have below list of Flows:

    - Pre Flow

    - Conditional Flow

    - Post Flow

    - Post Client Flow


- **Target Endpoint**

  - It can have below list of Flows:

    - Pre Flow

    - Conditional Flow

    - Post Flow


- When a client request comes, it hits the **Proxy Endpoint**. Then, it goes to **Pre Flow > Conditional Flow > Post Flow**. Once done, it will go to the **Target Endpoint** and executes **Pre Flow > Conditional Flow > Post Flow**. After that, the Target Endpoint send the request to the Backend service. Every time, **Pre Flow** and **Post Flow** are mandatory, but the **Conditional Flow** is optional.Backend service then replies back to the **Target Endpoint** and starts the **Pre Flow > Conditional Flow > Post Flow** process again. Then it will go to the **Proxy Endpoint** and start the **Pre Flow > Conditional Flow > Post Flow** and return to the client.


- **Pre Flow** Sample


```
<PreFlow name="PreFlow">
    <Request>
        <Step>
            <Name>Assign-Message-3</Name>
        </Step>
    </Request>
    <Response/>
</PreFlow>
```

- In this example, the **Assign-Message-3** policy applies to all the requests. It doesn't check any condition.


- **Conditional Flow** Sample


```
<Flow name="getGetCustomerById1">
    <Description>Retrieve getCustomerById</Description>
    <Request/>
    <Response/>
    <Condition>(proxy.pathsuffix MatchesPath "/getCustomerById") and (request.verb = "GET")</Condition>
</Flow>
```

- This Flow executes only when the URI path matches /getCustomerById and the HTTP method is GET.


- **Post Flow** Sample


```
<PostFlow name="PostFlow">
    <Request/>
    <Response/>
</PostFlow>
```


- In this example none of the policies are added to the Post Flow.


- When you check the example hello-world API proxies, you can see the flow structure in the code:


![hello-world-flow](/GCP_pictures/Study-logs/Apigee/hello-world-flow.PNG "Hello world flow")


- And you can see there's no Conditional Flow here. You can check in the Postman website that you get the same **hello, guest** result whether you put GET or POST request. HTTP method is defined in Conditional Flow.


![GET-request-result](/GCP_pictures/Study-logs/Apigee/GET-request-result.PNG "GET request result")


![POST-request-result](/GCP_pictures/Study-logs/Apigee/POST-request-result.PNG "POST request result")



### Create an API Proxy

- Let's understand a few terminologies before creating an API proxy.


- **Base path**

- It is the initial URL segment of the API.


- It is a URL prefix for all API paths relative to host.


- It must start with a leading /.


- If the base path not specified, it default to /.


- Valid base paths:

  - /v1

  - /version/v1

  - /v1/department/getname

  - /v1/*/getname


http://www.nkptech.com/v1/technology/findjobs?skill=apigee


/v1 - base path


- **Operation/Scheme/BaseURL/Paths/Parameters**


GET http://wwww.nkptech.com/v1/technology/findjobs?skill=apigee


**GET** - operation


**http** - scheme


**www.nkptech.com** - host


**/technology/findjobs** - path or it can be just /


**skill=apigee** - query parameters


**Sample base URL**: http://www.nkptech.com/v1


- Let's create an API now. Go to Apigee console and click API Proxies. Then click Create New.


![create-new-api](/GCP_pictures/Study-logs/Apigee/create-new-api.PNG "Create new API")


- Then choose **Reverse Proxy** as a proxy type:


![create-reverse-proxy](/GCP_pictures/Study-logs/Apigee/create-reverse-proxy.PNG "Create reverse proxy")


- Here, give the Name and base path. Also, we will use the existing GitHub API that gives **random zen words**.


![proxy-details](/GCP_pictures/Study-logs/Apigee/proxy-details.PNG "Proxy details")


- Click next and let's not select anything in the Policies section. Go to next.


![no-policies](/GCP_pictures/Study-logs/Apigee/no-policies.PNG "No policies")


- Here, we can choose the environment. But we will choose nothing and just create.


![just-create](/GCP_pictures/Study-logs/Apigee/just-create.PNG "Just create")


- Go to the newly created sample API details and click Develop.


![sample-api-develop](/GCP_pictures/Study-logs/Apigee/sample-api-develop.PNG "Sample API develop")


- Now, we will add a new **conditional flow** here. Click on the plus sign. Choose Path and Verb as Condition Type and go with GET.


![add-conditional-flow](/GCP_pictures/Study-logs/Apigee/add-conditional-flow.PNG "Add conditional flow")


![add-conditional-flow](/GCP_pictures/Study-logs/Apigee/add-conditional-flow-2.PNG "Add conditional flow-2")


- Now you added a new conditional flow.


![new-conditional-flow](/GCP_pictures/Study-logs/Apigee/conditional-flow-added.PNG "Conditoinal flow added")


- Just save this API proxy.


![save-proxy](/GCP_pictures/Study-logs/Apigee/save-api-proxy.PNG "Save API proxy")


- Now, click **Deploy** next to the save button. Deploy the API proxy to the eval environment.


![deploy-api](/GCP_pictures/Study-logs/Apigee/deploy-api-proxy.PNG "Deploy API proxy")


- Remember, we deployed it to eval environment in eval group. 


![remember-eval-group](/GCP_pictures/Study-logs/Apigee/remember-eval-group.PNG "Remember eval group")


- And the sample API base path was /sample-api-1. As the eval group host name is **34.36.128.129.nip.io**, we need to append the **/sample-api-1** base path to it to see our API proxy.


![api-proxy-works](/GCP_pictures/Study-logs/Apigee/api-proxy-works.PNG "API proxy works")


- And still, the existing hello-world proxy still works.


![existing-proxy-works](/GCP_pictures/Study-logs/Apigee/existing-api-proxy.PNG "Existing API proxy")



## Flow Configuration

- API Proxy flows are represented in XML format.


- Following are the XML elements to define Flows in Apigee.

  - ProxyEndpoint

  - PreFlow

  - Flows/Flow

  - PostFlow

  - Request

  - Response

  - HTTPProxyConnection

  - BasePath

  - RouteRule

  - TargetEndpoint

  - HTTPTargetConnection

  - URL

  - ProxyClientFlow


```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ProxyEndpoint name="default">
  <PreFlow name="PreFlow">
    <Request/>
    <Response/>
  </PreFlow>
  <Flows>
    <Flow name="getCustomer">
      <Description/>
      <Request/>
      <Response/>
      <Condition>(proxy.pathsuffix MatchesPath "/") and (request.verb = "GET")</Condition>
    </Flow>
  </Flows>
  <PostFlow name="PostFlow">
    <Request/>
    <Response/>
  </PostFlow>
  <HTTPProxyConnection>
    <BasePath>/sample-api-1</BasePath>
  </HTTPProxyConnection>
  <RouteRule name="default">
    <TargetEndpoint>default</TargetEndpoint>
  </RouteRule>
</ProxyEndpoint>
```


```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<TargetEndpoint name="default">
  <PreFlow name="PreFlow">
    <Request/>
    <Response/>
  </PreFlow>
  <Flows/>
  <PostFlow name="PostFlow">
    <Request/>
    <Response/>
  </PostFlow>
  <HTTPTargetConnection>
    <URL>https://api.github.com/zen</URL>
  </HTTPTargetConnection>
</TargetEndpoint>
```

**<ProxyEndpoint>**

- It is the root element of the Proxy Endpoint flow configuration file.


**<TargetEndpoint>**

- It is the root element of the Target Endpoint flow configuration file.


**<PreFlow>**

- It is having <Request> and <Response> as its child elements.


**<Request>**

- It holds the policies to execute during the Request's Preflow.


**<Response>**

- It holds the policies to execute during the Response's Preflow.


**<Flow>**

- The default flow will not have any conditions.


**<Condition>**

- Inside Flow, we have Condition. If condition is satisfied, we will go to the **Flow** that defines the steps.


**Operators**

| Symbol | Words |
| ------:| -----------:|
| !   | Not |
| = | Equals |
| !=    | NotEquals |
| :=    | EqualsCaseInsensitive |
| > or <&gt;>    | GreaterThan |
| >= or <&gt;=>    | GreaterThanOrEquals |
| <&lt;>    | LesserThan |
| <&lt;=>    | LesserThanOrEquals |
| &&    | And, and |
| ||    | Or |
| ~    | Matches, Like |
| ~/    | MatchesPath, LikePath |
| =|    | StartsWith |


- Operators and operands should be used with space.


