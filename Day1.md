## What is IaC?

Infrastructure as Code (IaC) is a widespread terminology among DevOps professionals and a key DevOps practice in the industry. 

It is the process of managing and provisioning the complete IT infrastructure (comprises both physical and virtual machines) using machine-readable definition files. 

It helps in automating the complete data center by using programming scripts.
## Why IaC?


![image](https://github.com/user-attachments/assets/ecf774cd-5ba2-4b06-a78d-dc2ddc4e17e0)


### Terraform

![image](https://github.com/user-attachments/assets/4ae6ad07-fd95-4357-95aa-73c6b18b3ede)


Terraform is one of the most popular Infrastructure-as-code (IaC) tool, used by DevOps teams to automate infrastructure tasks.

It is used to automate the provisioning of your cloud resources.

Terraform is an open-source, cloud-agnostic provisioning tool developed by HashiCorp and written in GO language.

## Benefits of using Terraform:

Does orchestration, not just configuration management

Supports multiple providers such as AWS, Azure, Oracle, GCP, and many more

Uses easy to understand language, HCL (HashiCorp configuration language)


# Installation of Terraform

https://developer.hashicorp.com/terraform/install

## Terraform Lifecycle

![image](https://github.com/user-attachments/assets/d5611e27-afc8-439b-b462-a6a03393abd9)

1. Terraform init initializes the (local) Terraform environment. Usually executed only once per session.

2. Terraform plan compares the Terraform state with the as-is state in the cloud, build and display an
execution plan. This does not change the deployment (read-only).

3. Terraform apply executes the plan. This potentially changes the deployment.

4. Terraform destroy deletes all resources that are governed by this specific terraform environment.


## Terraform Core Concepts

1. Variables: 

Terraform has input and output variables, it is a key-value pair. 

Input variables are used as parameters to input values at run time to customize our deployments. 

Output variables are return values of a terraform module that can be used by other configurations.

2. Provider: 

Terraform users provision their infrastructure on the major cloud providers such as AWS, Azure, OCI, and others.

A provider is a plugin that interacts with the various APIs required to create, update, and delete various resources.


3. State: 

Terraform records information about what infrastructure is created in a Terraform state file. 

With the state file, Terraform is able to find the resources it created previously, supposed to manage and update them accordingly.

4. Resources: 

Cloud Providers provides various services in their offerings, they are referenced as Resources in Terraform. 

Terraform resources can be anything from compute instances, virtual networks to higher-level components such as DNS records. 

Each resource has its own attributes to define that resource.





