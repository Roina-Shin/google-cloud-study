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




