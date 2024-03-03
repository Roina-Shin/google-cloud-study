### [Source of this study material : GCP Professional Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)


## Caching

- How can you reduce the load on:

  - Your data stores

  - Your servers


- The solution is to use **caching**


- Questions to ask when caching?

  - **How often** does the data change?

    - Caching is amazing if the data does not change frequently


  - Am I ok with some **stale data**?

    - Caching might return some older versions of data

    - You can configure TTL (Time To Live) on data

    - Then, the data will be store on the cache for that specific time period


  - Caching Use Cases

    - Caching **infrequently changing data** in Database

    - Caching **user sessions** from applications

    - Caching static content

    - Caching infrequently changing dynamic content


## Memorystore

- **Memorystore** is **in-memory datastore service**: reduces access time


- Fully managed: Provisioning, Replication, Failover & Patching


- Support for **Redis and Memcached**:

  - Use Memcached for caching

    - Store user sessions, database query caching

  - Use Redis for low latency access with persistence and high availability

    - Gaming leader boards, etc.

- Can be accessed from:

  - Compute Engine

  - App Engine Flexible and Standard

  - Google Kubernetes Engine

  - Cloud Functions


## Cloud CDN - Content Delivery Network

- Use Google's global edge network to serve global content with low latency


- Integrates with **External HTTP(S) Load Balancing**

  - Load Balancing provides frontend IP address and port


- Backends can be:

  - Cloud Storage buckets, Instance groups, App Engine, Cloud Run or Cloud Functions

  - Endpoints outside of Google Cloud 


- How Cloud CDN works?

  - External HTTP(S) Load Balancing uses proxies - Google Front Ends (GFEs)

    - Request from user arrives at a Google Front End (GFE)

    - If URL maps to the backend with Cloud CDN configured:

      - If content is found in cache(cache hit), GFE sends cached response

      - If the content is not found in cache(cache miss), request is forwarded to backend (origin server)

        - Response is sent to user and cached

    - Using TTL settings to control cache duration 



## Cloud CDN Best Practices

- **Cache static content**

  - Example: Cache-Control: public, max-age=259200 (72 hours)


- Be careful with expiring **time-sensitive (or dynamic) content**

  - Smaller cache periods. Example: Cache-Control: public, max-age=300 (5 minutes)


- Use **custom cache keys** to improve cache hit ratio

  - By default, the cache key includes the entire URL (e.g. https://yourwebsite.com/my-image/1.jpg)

  - You can customize **cache key** by using any combination of protocol, host, or query string


- Example configuration of a cache key:


```
gcloud compute backend-services update BACKEND_SERVICE --enable-cdn --no-cache-key-include-protocol --no-cache-key-include-host --no-cache-key-include-query-string
```