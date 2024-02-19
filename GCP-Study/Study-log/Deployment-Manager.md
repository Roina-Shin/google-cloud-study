### [Source of this study material : Google Cloud Deployment Mnager by Jose Portilla](https://www.udemy.com/course/google-cloud-deployment-manager/)


## Deployment Manager Demo

- Create a new project which you can use for Deployment Manager demo and delete after using it.


- Enable Compute Engine API and Deployments API.


- Then activate the Cloud Shell.


- First, configure the environment:


```
gcloud config set project [project id]
```


![gcloud-config-set](/GCP_pictures/Study-logs/deployment-manager2/gcloud-config-set.PNG "gcloud config set")


- Then, clcik Open Editor.


- In the editor, create a new file named **vm.yaml**. Just make sure that the file lives in the **/home/[username]/** directory.


![editor-yaml](/GCP_pictures/Study-logs/deployment-manager2/editor-yaml.PNG "yaml file for vm")


- If you set up this yaml file, you won't need to run a bunch of commands individually to create some environment you want to set up.


- And enter the snippet of code inside the yaml file:


```
resources:
resources:
  - type: compute.v1.instance
    name: quickstart-deployment-vm
    properties:
      zone: us-central1-f
      machineType: https://www.googleapis.com/compute/v1/projects/service-project-2-414510/zones/us-central1-f/machineTypes/f1-micro
      disks:
        - deviceName: boot
          type: PERSISTENT
          boot: true
          autoDelete: true
          initializeParams:
            sourceImage: https://www.googleapis.com/compute/v1/projects/debian-cloud/global/images/family/debian-11
      networkInterfaces:
        - network: https://www.googleapis.com/compute/v1/projects/service-project-2-414510/global/networks/default
          accessConfigs:
            - name: External NAT
              type: ONE_TO_ONE_NAT
```


![yaml-example](/GCP_pictures/Study-logs/deployment-manager2/yaml-example.PNG "yaml example")


- Shirink the editor a bit and go to Deployments in the cloud console.


![deployment-on-console](/GCP_pictures/Study-logs/deployment-manager2/deployment-console.PNG "Deployments on console")



- Also go to cloud shell and run **ls** to see the yaml file we just created:


![ls-command](/GCP_pictures/Study-logs/deployment-manager2/ls-command.PNG "ls command")


- Then we will **create a deployment** to actually **run this configuration yaml file** with:


```
gcloud deployment-manager deployments create myfirst-deployment --config vm.yaml 
```


![gcloud-deployment-manager](/GCP_pictures/Study-logs/deployment-manager2/gcloud-deployment-manager.PNG "gcloud deployment manager")


- The deployment is created according to the configuration. You can check the deployment by running:


```
gcloud deployment-manager deployments describe [deployment-name]
```


![deployment-manager-describe](/GCP_pictures/Study-logs/deployment-manager2/deployment-manager-describe.PNG "gcloud deployment-manager describe")



- And you can check that the VM is created.


![vm-created](/GCP_pictures/Study-logs/deployment-manager2/vm-created.PNG "vm created")


- You can simply delete the machine. But what if you spun off a lot of machines from the deployment? You can delete all the machines associated with the deployment by:


- Go to Deployments on the console and hit delete.


![delete-deployment](/GCP_pictures/Study-logs/deployment-manager2/delete-deployment.PNG "Delete deployment")


- Or, go to the cloud shell and run:


```
gcloud deployment-manager deployments delete [deployment-name]
```


## Configurations Overview

- Configuration

  - A configuration is a blueprint for your deployment, detailing the types and properties of resources involved.

  - It includes resources, templates, and subfiles to form the complete deployment structure.

  - A configuration is mandatory for creating any deployment.


- Resource in Configuration

  - Supports a wide range of Google Cloud resources within a single file.

  - Examples include Compute Engine resources (like autoscalers, instance groups), Kubernetes engine, BigQuery, Cloud Storage, Cloud SQL.


- Configuration Language

  - Configurations are written in YAML syntax.

  - Later on we will see about **templates** which are different than configurations and can be written in Jinja or Python.


- Template in Configurations

  - Configurations can include Jinja or Python templates, or a mix of both.

  - Templates can be sourced locally or from third-party URLs.



## Creating Configuration YAML File

- Configuration files are at the core of Google Cloud Deployment Mnager.


- Configuration File Structure

  - It consists of 2 main sections:

    - **Imports**: imports are paths relative to the configuration files.

    - Imports section lists template files used in the configuration.

    - Includes paths to Jinja or Python templates.

    - Deployment Manager expands these templates to form the final configuration.

    - **Resources**: central part of the deployment, listing all resources.

    - Resources can be:

      - Google-managed base types (e.g. Compute Engine VM instances)

      - Imported templates

      - Composite types

      - Type providers


### Resource type - Google-managed base type

- These are direct references to Google Cloud resources.

- Examples: Cloud SQL instance, Cloud Storage bucket

- Syntax: 

  - **type: <api>.<api-version>.<resource-type>**

  - **type: bigquery.v2.dataset**

- To see the list of all supported types:

```
gcloud deployment-manager types list
```

- After specifying the resource type, it's essential to **name the resource** and **define the properties**.

- These properties instruct Deployment Manager on how to create the resource with desired characteristics.



## Configuration Previews

- After you have written a configuration file, you can preview the configuration before you create a deployment.


- Previewing a configuration lets you see the resources that Deployment Manager would create but does not actually **instantiate any actual resources**.


- You can run this command for **preview**:


```
gcloud deployment-manager deployments create [deployment name] --config configuration-file.yaml --preview
```

- If you want to move forward with the deployment after preview:


```
gcloud deployment-manager deployments update [deployment name]
```


- If you don't want to move forward with the deployment after preview: **(cancle and delete)**


```
gcloud deployment-manager deployments cancel-preview [deployment name]
```


## Configuration Creation and Preview Demo

- Assume that you want to create a configuration yaml file for creating a **Storage Bucket**.


- Then, search for **google cloud storage api** on Google.


- Explore some pages after pages until you see the page that is actually linked to **creating a bucket**.


![API for creating a bucket](https://cloud.google.com/storage/docs/json_api/v1/buckets)


- And then compare the GCP console bucket creation page and the documentation so that what configuration elements you need to define in your file:


![api-page](/GCP_pictures/Study-logs/deployment-manager2/api-page.PNG "API page")


![bucket-creation-gui](/GCP_pictures/Study-logs/deployment-manager2/bucket-creation-gui.PNG "Bucket creation GUI")


- Now, we will start to create a configuration yaml file by opening up the Editor on the GCP console.


![bucket-yaml-file](/GCP_pictures/Study-logs/deployment-manager2/bucket-yaml-file.PNG "Bucket YAML file")


```
resources:
  - name: yejin-deployment-manager-demo-bucket
    type: storage.v1.bucket
    properties:
      location: us
      storageClass: STANDARD
```


- Save the file and preview this:


![bucket-yaml-saved](/GCP_pictures/Study-logs/deployment-manager2/bucket-yaml-saved.PNG "Bucket YAML saved")


- Then go to the Cloud Shell and run the command:


```
gcloud deployment-manager deployments create [deployment name] --config [config file name] --preview
```

- If you want to actually create the deployments:


```
gcloud deployment-manager deployments update [deployment name]
```


![deployment-preview-run](/GCP_pictures/Study-logs/deployment-manager2/deployment-preview-run.PNG "deployment preview run")


- You can see the deployment on the console and check the bucket as well.


![bucket-deployment-console](/GCP_pictures/Study-logs/deployment-manager2/bucket-deployment-console.PNG "Bucket deployment on console")


![actual-bucket](/GCP_pictures/Study-logs/deployment-manager2/actual-bucket.PNG "Bucket created")



## Understanding Templates

- For basic needs, a simple configuration file suffices.


- For complex systems or reusable configurations, break the setup into multiple templates to save yourself time and create more repeatable deployments.


- A template is an independent file, used as a type within a configuration.


- Multiple templates can be integrated into a single configuration.


- They enable segmentation of configurations into reusable components.


- Templates language choices : they support either Jinja or Python.


- Jinja aligns closely with YAML making it easier for YAML users.


- Python templates enable programmatic template generation and formatting using Python libraries.


- Can mix both types in a configuration.


- After creating a template, import it into your configuration file to use it.


- To import the template, add an **imports** section in your configuration, followed by the relative or absolute path from the current directory.


- **Imports** Example:


```
imports:
  - path: path/to/my_vm_template.jinja
    name: my_renamed_template.jinja
  - path: special_vm.py
```


- **Deploying the template in configuration**. Once you imported the templates, you simply provide them as the **type** for a resource.


```
imports:
  - path: vm-template.jinja

resources:
  - name: my-vm
    type: vm-template.jinja
```

- For reusability purposes, you can set the value of properties inside the template:


```
imports:
  - path: vm_template.jinja

resources:
  - name: my-vm
    type: vm_template.jinja
    properties:
      zone: us-central1-a
```



### Available environment variables


| Environment variable | Value |
| ------ | ----------- |
| deployment  | The name of the deployment |
| name | The name declared in the configuration that is using the template. This can be useful if you want the name you declare in the configuration to be the name of the resource in the underlying templates. |
| project    | The project ID for this deployment. |
| project_number | The project number for this deployment. |
| current_time | The UTC time stamp when expansion started for the deployment. |
| type   | The resource type declared in the top-level configuration. |
| username    | The current Deployment Manager user. |


- Use the following syntax to use an environment variable inside a template file:


```
{{  env["deployment"]  }}  # jinja

context.env["deployment"]  # python
```


- Using an environment variables in a Jinja template


```
- type: compute.v1.instance
  name: vm-{{  env["deployment]  }}
  properties:
    machineType: zones/us-central1-a/machineTypes/f1-micro
    serviceAccounts:
      - email: {{  env["project_number"]  }}-compute@developer.gserviceaccount.com
        scopes:
          - ...
```



## Understanding Schemas

- Schemas are blueprints that outline the specifications for Deployment Manager templates.


- Schemas simplify user interaction with complex templates.


- Users don't need to understand every detail of the template layers.


- They provide a clear guide on what properties are adjustable or mandatory.


- A schema can mandate certain properties to be always present in the template:

  - One property might be required to be a string.

  - Another might need to be an integer less than 100.


- Users review the schema to understand how to configure the template correctly.


- They set the appropriate properties in their configurations based on the schema's guidelines.


- If a user wishes to use a specific template, they consult the schema to determine the necessary properties and their format.


- This ensures that the configuration aligns with the template's requirements and functions as intended.


- A schema file contains fiels:

  - info, imports, required, properties


- **Info**: it contains meta information about the schema. This includes info such as title, a version number, a description, and so on.


- At a minimal, provide a **title** and **description** in this property.


- **Imports**: it contains a list of corresponding files that are required for templates that use this schema.


- When you upload a template with a schema that has a list of imports, Deployment Manager checks that all of the files in the imports property were uploaded along with the template.


- **Required**: the required field contains a list of elements from the properties field that are required in the template that uses the schema.


- Any elements not specified in this required field are considered optional.


- Example schema:


```
info:
  title: VM Template
  author: Yejin
  description: Creates a new network and instance
  version: 1.0

imports:
  - path: vm-instance.jinja # must be a relative path


required:
  - IPv4Range

properties:
  IPv4Range:
    type: string
    description: Range of the network

  description:
    type: string
    default: "My super great network"
    description: Description of network
```


- So, this schema can be applied to this template.


```
resources:
  - name: vm-1
    type: vm-instance.jinja

  - name: a-new-network
    type: compute.v1.network
    properties:
      IPv4Range: {{  properties['IPv4Range']  }}
      description: {{  properties['description']  }}
```


- A user can create a configuration file from this like below:


```
imports:
  - path: vm-instance-with-network.jinja

resources:
  - name: vm-1
    type: vm-instance-with-network.jinja
    properties:
      IPv4Range: 10.0.0.1/16
```


- A schema is a separate document that is named after the template for which it describes. 


- Schemas must be named with the same name as the corresponding template, with **.schema** appended to the end:

  - **TEMPLATE_NAME.EXTENSION.schema**

  - **vm-instance.py.schema**

  - **vm_template.jinja.schema**


- If there are any schema files, identified by the appended **.schema** format, Deployment Manager will upload the schema and validate the deployment against the schema, before it attempts to create any resources.


- To use this schema, just include it in the same local directory as your templates and configuration, and create your deployment as you would normally.



## Deployment Lifecycle Demo

- Let's head over to cloud console and go through the lifecycle of a deployment, including a configuration file that uses a template.


- We will start up by creating a **template**.


- Create a new file called **bucket_template.jinja**.


```
resources:
- type: storage.v1.bucket
  name: bucket--{{  env['project_number']  }}
  properties:
    location: US
    storageClass: STANDARD
```


![bucket-template](/GCP_pictures/Study-logs/deployment-manager2/bucket-template.PNG "Bucket template")


- Then we will create a configuration file called **bucket_config.yaml**.


```
imports:
- path: bucket_template.jinja

resources:
  - name: bucket_config_name # It's just placeholder name. We know that the template will use the project_num for this.
    type: bucket_template.jinja
```


![bucket-config-file](/GCP_pictures/Study-logs/deployment-manager2/bucket-config-file.PNG "Bucket configuration file")


- Then we will go to the cloud shell and run a preview first:


```
gcloud deployment-manager deployments create demo-deployment --config bucket_config.yaml --preview
```


![run-final-preview](/GCP_pictures/Study-logs/deployment-manager2/run-final-preview.PNG "Run preview")


- And move forward with this deployment:


```
gcloud deployment-manager deployments update demo-deployment
```


![demo-final-run](/GCP_pictures/Study-logs/deployment-manager2/demo-final-run.PNG "Go with deployment")


- Also, verify that the bucket is created accordingly:


![bucket-verification](/GCP_pictures/Study-logs/deployment-manager2/bucket-name-verify.PNG "Verify bucket")


- Now we can delete the deployment by:


```
gcloud deployment-manager deployments delete demo-deployment
```


![final-deployment-deletion](/GCP_pictures/Study-logs/deployment-manager2/final-deployment-deletion.PNG "Final deployment deletion")


