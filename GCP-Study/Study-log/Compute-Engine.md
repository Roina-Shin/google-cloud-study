### [Source of this study material : Google Cloud Platform from Zero to Hero by Memi Lavi](https://www.udemy.com/course/google-cloud-platform-from-zero-to-hero-the-complete-guide/)


## Compute Engine


![VM-architecture](/GCP_pictures/Study-logs/VM/vm-architecture.PNG "VM architecture")


- At the bottom, we have a physical server which is the host of virtual machines.

- Host is a physical server and guests are virtual machines.

- Above the host, we have a Hypervisor which is a piece of software that manages the virtual machines.

- Host OS/Hypervisor belongs to a physical server.

- Then, inside these servers we have the guest OS of virtual machines.

- Bins/Libs and Code are also living inside the virtual machines.

- We can have more than one virtual machines on a single physical server.

- **VM density = the number of VMs per host**

- In GCP, the host OS and Hypervisor are managed by Google and we have no control or access to them.

- The virtual machines themselves are managed by us. We have full control and access to them.


## How to create a compute engine

- First, select the location.

- Select the image (OS + pre-installed software)

- Select the size of the vm

- Also, check the price of the vm.


## GCP VM families

- VM families are classified to the following workload types:

| **General Purpose**   | Web servers, microservices, virtual desktops, databases, etc. |
| **Compute Optimized** | High performance computing, game servers, media transcoding, etc. |
| **Memory Optimized**   | SAP HANA databases, in-memory data stores (Redis), etc. |
| **Accelerator Optimized**   | Machine Learning training, massively parallelized computation, Deep Learning, etc. |


### General Purpose

| VM series | characteristics |
| ------ | ----------- |
| E2   | Low traffic web server, back office apps, virtual desktops |
| N2, N2D, N1 | Medium traffic web servers, microserivces, BI |
| C3    | High traffic web servers, databases, in-memory cache |
| TAU T2D, T2A    | ARM architecture, cost effective, scale out workloads |


### Compute Optimized

| VM series | characteristics |
| ------ | ----------- |
| H3   | High Performance Computing workload, scientific and engineering computing |
| C2, C2D | Gaming, ad serving, media serving, AI/ML |


### Meomory Optimized

| VM series | characteristics |
| ------ | ----------- |
| M1, M2, M3   | SAP HANA, MS SQL, memory intensive apps |


### Accelerator Optimized

| VM series | characteristics |
| ------ | ----------- |
| A2, A3   | High Performance Computing, ML training |
| G2 | Video transcoding, remote visualization |



## GPU

- Some VM series can use GPU in addition to CPU.

- A2 and G2 series have built-in support for GPU and no need to add it later.

- GPU can also be added to N1 machines.

- All GPUs are NVIDIA based.



## Connecting with your VM instance

- When you created a VM instance, click SSH button in its details page.

- Run the following command to see the details of your vm:

```
uname -a
```

![VM-uname-a](/GCP_pictures/Study-logs/VM/VM-uname-a.PNG "To see your VM details")


## 4 aspects to consider to reduce the cost of VM

 1. Scheduled Shutdown

 2. Spot Instances

 3. Commited Use Discounts

 4. Disky Types


### Scheduled Shutdown

- VM operations can be scheduled.

- This is useful for VMs that are not needed for 24/7.

  - Test / Dev

  - Batch processing

- Instances can be shut down when not in use, thus reducing cost.

- Click Instance Schedules and then Create Schedule.


![VM-instance-schedules](/GCP_pictures/Study-logs/VM/VM-instance-schedules.PNG "Create instance schedule")



- Put in some details to your schedule.



![VM-schedule-instance](/GCP_pictures/Study-logs/VM/VM-schedule-instance.PNG "Schedule your instance")



- To actually connect this schedule to your VM:


![VM-click-new-schedule](/GCP_pictures/Study-logs/VM/VM-click-new-schedule.PNG "Click your new schedule")


- Then click Add your instances to schedule.


![VM-add-instances-to-schedule](/GCP_pictures/Study-logs/VM/VM-add-instance-to-schedule.PNG "Add your instances to the schedule")


- Select your VM and add it to your schedule.


![VM-select-vm-and-add](/GCP_pictures/Study-logs/VM/VM-select-vm-and-add.PNG "Select your VM and add it to your schedule")


- If you got an permission error message like this,


![VM-permission-error](/GCP_pictures/Study-logs/VM/VM-permission-error.PNG "Permission error message")



- To resolve the issue, you need to run the following command:


```
gcloud projects add-iam-policy-binding REPLACE_WITH_PROJECT_ID \
--member "serviceAccount:service-xxxxxx@compute-system.iam.gserviceaccount.com" \
--role "roles/compute.instanceAdmin.v1"
```


- Within the 'xxxxxx' above in the code, you need to copy the number of your compute service account in the error message, and paste it there.


![VM-number-of-error-message](/GCP_pictures/Study-logs/VM/VM-copy-the-number.PNG "Copy the number")


- Also replace your Project ID in the code. Then, open your cloud shell.


- Copy and paste your code in the cloud shell and run it.


- Try to add your instance to your schedule again. Then it will be successful this time. :)


![VM-add-instance-to-schedule-success](/GCP_pictures/Study-logs/VM/VM-add-schedule-success.PNG "Adding instance to schedule, successful!")


- Again, if your instance is not needed 24/7, it's a good idea to set a schedule for your vm to shut down when it's in no use.


### Spot Instances

- This is a great way to save costs, up to 91% discount.

- Spot Instance is a special type of instance that can be stopped and removed by Google at any time.

- Spot Instances are great for batch processing, data analytics, etc.

- Don't use them for web apps and systems that need to be accessible.

- You can opt for spot instance in the VM creation page.


![VM-spot-instance](/GCP_pictures/Study-logs/VM/VM-spot-instance-option.PNG "Spot Instance option")


- You can also set the time limit for your VM and what happens to the VM when the time limit ends.


![VM-instance-set-time-limit](/GCP_pictures/Study-logs/VM/VM-set-time-for-spot.PNG "Set a time limit on your spot VM")


- If it is just a one-time task, then you can go for a 'Delete' option so that your VM will be deleted after the time limit.


### Commited Use Discounts

- You can get a big discount for commiting to use specific resources.

- Using this technique, you can get up to 70% discount.

- You pay the commited price regardless of the actual use.

- Commitment is either for 1 or 3 years.


![VM-commited-use-discounts](/GCP_pictures/Study-logs/VM/VM-commited-use.PNG "Where to find Commited Use Discounts")


- This is how you commit your usage to a specific hardware or license.


![VM-how-to-commit-use](/GCP_pictures/Study-logs/VM/VM-how-to-commit-use.PNG)


### Disk Types

- When creating VM instance, it's important to select the best disk type for it.

- Disk type affects the reliability, speed, and cost.

- There are 2 families of Disk Types:

  - Local SSD

  - Persistent disk


| Local SSD | Persistent disk |
| ------ | ----------- |
| Attached to the physical host of the VM   | Durable network storage |
| Provides the best performance | Can either be zonal and regional - replicated across zones |
| Ephemeral disk - when the VM shuts down data is lost    | Can be detached and moved from VM |
| Size is always 375GB    | Auto scalable |


| Persistent Disk Types | Characteristics |
| ------ | ----------- |
| Balanced   | As SSD disk, balances performance and cost. Best for general purpose systems. |
| Performance | As SSD disk, it's for high-performance databases. Designed for single-digit millisecond latencies. |
| Standard    | As HDD disk, it's for large data processing. |
| Extreme    | As SSD disk, it's for consistent high performance. |


- The default Boot Disk Type is **Balanced Persistent Disk**.


## VM Metadata

- Every VM stores metadata in a special metadata server.

- Metadata can be accessed using specialized HTTP requests from the VM.

- Metadata contains various data about the VM and the project.

- Metadata is useful for:

  - Get data about the VM e.g. external IP

  - Use data in startup script

  - Learn about maintenance schedule

- From within the VM:

  - Access this root URL:

      http://metadata.google.internal/computeMetadata/v1/

  - This is always **the same URL** regardless of your VM.

  - Also, specify this header:

      Metadata-Flavor: Google


  -  Connect to your VM via SSH and run the following command:

  ```
  curl "http://metadata.google.internal/computeMetadata/v1/" -H "Metadata-Flavor: Google"
  ```

  - To change directory inside the metadata, simply add the metadata directory after the url like below:


  ![VM-change-directory-in-metadata](/GCP_pictures/Study-logs/VM/VM-metadata-in-SSH.PNG "Change directory in metadata in SSH")



  - Also, if you want to return all the data inside the directory, you can simply add a parameter right after the url again.


  ![VM-recursive-metadata](/GCP_pictures/Study-logs/VM/VM-recursive-metadata.PNG "Obtain recursive metadata")


  - To read the data in a more human readable way, copy and paste the data into the VS Code (or your preferred editor) to format it.


  - If you **alt + shift + f**, it will automatically format the JSON data neatly.


  ![VM-format-json-file](/GCP_pictures/Study-logs/VM/VM-format-json-shortcut.PNG "Format JSON data using the shortcut key")


  - Now, you can scan the metadata a lot more easily. 



## Sole Tenancy

- By default, VM instances are placed on physical servers that host VM instances of other GCP customers

- If you feel uncomfortable with this, then you can have a dedicated physical server for your VMs.

- This is called 'Sole Tenant Nodes".

- But the cost is very expensive.


![VM-how-sole-tenancy-works](/GCP_pictures/Study-logs/VM/VM-how-sole-tenanccy-works.PNG "How Sole Tenant Node works")


## Instance Template

- Creating instances manually is error prone and slow.

- Instance Templates define a VM configuration that can be used to create instances quickly and easily.

- Once you create an Instance Template, you cannot change it as it is immutable.


![immutable-instance-template](/GCP_pictures/Study-logs/VM/VM-example-template.PNG "Instance Templates are immutable")


- You can create a new VM right from the Instance Template page or in the dedicated VM instances page.

- Instance Template is a very convenient way to create multiple identical VMs.


## Instance Group

- You can create an Instance group from the Instance Template you created.

- Go to Instance Group and click Create Instance Group.


![create-instance-group](/GCP_pictures/Study-logs/VM/VM-instance-group.PNG "Create an Instance Group")




