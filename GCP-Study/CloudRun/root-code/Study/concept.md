### [Source of this study material : Google Cloud Run by Cloud Monkey](https://www.udemy.com/course/google-cloud-run-hands-on-technical-deep-dive/)

## What is Google Cloud Run?

- Cloud Run is a managed compute platform that lets you run containers
directly on top of Google's scalable infrastructure.

- You can deploy code written in any programming language on Cloud Run
if you can build a container image from it.

- Building container images is optional if you're using Go, Node.js,
Python, Java, .NET Core, or Ruby.

- You can use the source-based deployment option that builds the container for you.

## How to run your code on Cloud Run

- On Cloud Run, your code can either run continuously as a service or as a job.

- Cloud Run Service is designed to run indefinately, listening to HTTP requests, etc.

- Cloud Run Job is used to run a code to completion as a one-time task.

## Cloud Run Service

- Cloud Run Service is a stateless container that is invocable via HTTP requests.

- It is a fully managed compute platform that lets you run your code without having to
manage servers or infrastructure.

- Your responsibility is to make sure your code listens on a TCP port and handles HTTP requests.

- Every deployment in Cloud Run Service creates a new revision.
A revision is a snapshot of your container image and its environment at the time of its deployment.

Keep in mind that revisions are immutable so that they cannot be modified once created.

- You can route incoming traffic to the latest revision or roll back to the previous revision,
or split the traffic to multiple revisions.

It is useful if you want to reduce the risk of deploying a new revision.

For example, you can start by sending only 1% of your requests to a new revision,
and increase that percentage while monitoring the telemetry of that particular revision.

If you see any problems with that revision, you can roll it back to the previous revision without affecting your users.

- Cloud Run Service can be reachable from the Internet or you can restrict access in 3 ways:

1. Specify an access policy using Cloud IAM. -> This is the most granular way to control access.
2. Use ingress settings to restric network access. -> This is useful if you want to allow only internal traffic from the VPC or internal services.
3. Allow only authenticated users with Cloud Identity-Aware Proxy(IAP).

## Cloud Run Job

- If your code performs a one-time task and then stops, Cloud Run Job is a good option to run your code.

- A job can start one instance to run your code or you can also start many identical,
independent instances in parallel, that is, an array job.

- Array job is a faster way to process jobs that can be split into multiple independent tasks.

- You can schedule a job and execute it at whatever time you defined.
That is one of the purposes of running a Cloud Run Job.

## Cloud Run integrations

- Data Storage
  - Cloud Run integrates with Cloud SQL (managed MySQL, PostgreSQL, and SQL Server), Memorystore (managed Redis and Memcached), Firestore, Cloud Spanner, Cloud Storage, and more.

- Logging and error reporting
  - Container logs are automatically ingested by Cloud Logging. If there are exceptions in the logs, Error Reporting aggregates them, and then notifies you.

- Service Identity
  - Every Cloud Run revision is linked to a service account, and the Google Cloud client libraries transparently use this service account to authenticate with Google Cloud APIs.

- Continuous delivery
  - If you store your source code in GitHub, Bitbucket, or Cloud Source Repositories, you can configure Cloud Run to automatcially deploy new commits.

- Private networking
  - Cloud Run instances can reach resources in the VPC network through the serverless VPC access connector. 
