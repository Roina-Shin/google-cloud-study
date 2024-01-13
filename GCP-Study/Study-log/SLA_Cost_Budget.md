### [Source of this study material : Google Cloud Platform from Zero to Hero by Memi Lavi](https://www.udemy.com/course/google-cloud-platform-from-zero-to-hero-the-complete-guide/)


## What is SLA?

- SLA stands for Service Level Agreement.

- It basically defines the uptime % of a cloud service.


 | SLA (%)  | Yearly Downtime Allowed  |
 | ------  | -----------  |
 | 95  | 18d 6h 17m 27s  |
 | 99  | 3d 15h 39m 29s  |
 | 99.9  | 8h 25m 56s  |
 | 99.99  | 52m 35s  |


## SLA Pro Tips

- Always check the SLA of the service used.

- Looking at the SLA of a standalone service is not always enough.

- To get the actual system SLA, multiply the SLAs of the participating services:

  - App Engine SLA = 99.95%

  - Regional Spanner SLA = 99.99%

  - Actual SLA = 99.95% * 99.99% = 99.94% (5h 15m 34s annual downtime)

  - SLA calculator : [uptime.is](https://uptime.is/)



## Cost

- Almost everything in the cloud costs money.

- Pricing model:

  - Per resource (e.g. VM instance)

  - Per consumption (e.g. CLoud functions)


## SLA Pro Tips

- Always check the resources' cost before provisioning.

- Check for more cost-effective alternatives.

- Google Cloud's pricing calculator : [Google Cloud Calculator](https://cloud.google.com/products/calculator/)

- Use this calculator so that you have a general idea of how much the service is going to cost you.


## Budgets

- Budgets help you avoid surprises with cloud cost.

- Monitor the ongoing costs and send alerts.

- Budgets do not cap the actual cost, just monitor and alert.

- Whenever your cost arrives at one of the threshold rules, you will get Email alerts. 

  - e.g. Percent of Budget: 50%, 90%, 100%, etc.


## If you are aspiring to become a cloud architenct...

- Cloud-based system requires:

  - Infrastructure knowledge

    - You need to design networking, firewalls, application gateways, VPNs, load balancers, etc.

    - Also, security is an integral part of cloud architect role.

    - Hands on experience on cloud


