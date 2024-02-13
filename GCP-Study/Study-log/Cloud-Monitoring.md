### [Source of this study material : Google Cloud Professional DevOps Engineer Certification by Ankit Mistry](https://www.udemy.com/course/gcp-google-cloud-professional-devops-engineer-certification/)


## Cloud Monitoring

- Monitors various cloud resources


- Different metrics can be measured


- Monitors one or more GCP project or AWS account


## Cloud Monitoring Demo

- In Monitor Settings, you can add other projects to a metrics scope to share their data with the scoping project.


![add-more-projects](/GCP_pictures/Study-logs/cloud-monitoring/add-more-projects.PNG "Add more projects")


- When we go to Dashboards, there is no **compute engine** monitoring available. Maybe it's because we don't have any VM yet. 


![dashboards](/GCP_pictures/Study-logs/cloud-monitoring/dashboards.PNG "Dashboards")


- Let's go to Compute Engine and create one.


- When a VM is being created, refresh the monitoring page.


- Now, we have various VM related monitoring metrics available in our dashboards.


![vm-related-metrics](/GCP_pictures/Study-logs/cloud-monitoring/vm-related-logs.PNG "VM related metrics")


- When we go to VM instance metrics, we can see that no agent is installed yet.


![no-agent-detected](/GCP_pictures/Study-logs/cloud-monitoring/no-agent-detected.PNG "No agent detected")


- Go to far right side of the panel and SSH into the VM.


![ssh-into-vm](/GCP_pictures/Study-logs/cloud-monitoring/ssh-into-vm.PNG "SSH into VM")


- The installation method for individual VMs can be found in the Google documentation:


[google documentation](https://cloud.google.com/stackdriver/docs/solutions/agents/ops-agent/installation)


- Download and run the agent-installation script by:


```
curl -sSO https://dl.google.com/cloudagents/add-google-cloud-ops-agent-repo.sh
```

```
ls
```

```
sudo bash add-google-cloud-ops-agent-repo.sh --also-install
```


![ops-agent-installed](/GCP_pictures/Study-logs/cloud-monitoring/ops-agent-installed.PNG "ops agent installed")


- You can verify the installation in the Monitoring page as well:


![verify-installation](/GCP_pictures/Study-logs/cloud-monitoring/verify-ops-agent.PNG "Verify installation")


- If you see on the VM page, the ops agent started collecting various logs and metrics on the VM instance.


![vm-logs-metrics](/GCP_pictures/Study-logs/cloud-monitoring/metrics-available.PNG "VM logs and metrics")


- Now, to test **uptime check**, go to VM instance and SSH into it.


```
sudo apt install apache2
```

- When you enter the external IP of the VM on the browser, you can see the Apache is installed.


- Go to uptime check and set up some protocol and external IP address for that.


![uptime-check](/GCP_pictures/Study-logs/cloud-monitoring/uptime-check.PNG "Uptime check")


- After some time, if you check again, the uptime check shows if the VM is up and running ok.


![vm-is-up](/GCP_pictures/Study-logs/cloud-monitoring/vm-is-up.PNG "VM is up")


- If you stop your machine and try the uptime check, then all the check marks will be red.


![all-red](/GCP_pictures/Study-logs/cloud-monitoring/all-red.PNG "All red")


