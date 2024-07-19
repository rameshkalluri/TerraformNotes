## What is IaC?

Infrastructure as code (IaC) means to manage your IT infrastructure using configurationfiles.

## Why IaC?

Historically, managing IT infrastructure was a manual process. People would physically put servers in place and configure them.

Only after the machines were configured to the correct settings required by the OS and dependencies would those people deploy the application.

Businesses are making a transition where traditionally managed infrastructure can no longer meet the demands of today’s businesses. 

IT organizations are quickly adopting the public cloud, which is predominantly API-driven

To meet customer demands and save costs, application teams are architecting their applications to support a much higher level of elasticity, supporting technology like containers and public cloud resources.

## Benefits of IaC

### Speed

IaC benefits a company’s IT architecture and workflow as it uses automation to substantially increase the provisioning speed of the infrastructure’s development,testing, and production.

### Consistency

Since it is code, it generates the same result every time. It provisioned the same environment every time, enabling improved infrastructure consistency at all times.

### Cost

One of the main benefits of IaC is, without a doubt, lowering the costs of infrastructure management. With everything automated and organized, engineers save up on time and cost which can be wisely invested in performing other manual tasks and higher-value jobs.

### Version Controlled, Integrated

Since the infrastructure configurations are codified, we can check-in into version control like GitHub and start versioning it.

IaC allows you to track and give insight on what, who, when, and why anything changed in the process of deployment. This has more transparency which we lack in traditional infrastructure management.

Now, we know what Infrastructure as Code is means, now let’s deep dive into Terraform...

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




