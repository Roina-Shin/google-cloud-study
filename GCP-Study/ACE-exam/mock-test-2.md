### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -2

### 1. Send transactions to Pub/Sub and use MIG to process them

- CASE: Your game generates millions of events every minute. All these events need to be processed as transactions The amount of computation required to process the transactions is way more than the processing capabilities of a single VM. How can you spread these transactions across multiple VMs in real-time in a cost-effective manner?


- Solution: 

1. Send all the transatcions to Pub/Sub.

2. Use a managed instance group to process them in VMs. 


- Pub/Sub can effectively distribute a large number of tasks among multiple servers at a low cost. Sending all transactions to Pub/Sub and using a managed instance group to process them in VMs in a scalable and cost-effective solution. Pub/Sub allows for real-time data streaming and the managed instance group ensures that the transactions are spread across multiple VMs to handle the high volume of events.


### 2. Send transactions to Pub/Sub and use MIG to process them

- CASE: Your 