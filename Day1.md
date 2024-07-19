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

## installation of awscli 

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## how to setup communication b/w aws and terraform

### Create an AWS IAM User:

Log in to the AWS Management Console and navigate to the IAM dashboard.

Create a new IAM user with programmatic access. This user will be used by Terraform to authenticate with AWS.

Make sure to note the Access Key ID and Secret Access Key.

Terraform can infer the following environment variables for AWS

```
export AWS_ACCESS_KEY_ID="anaccesskey"
export AWS_SECRET_ACCESS_KEY="asecretkey"
```
Ref: https://www.terraform.io/docs/providers/aws/#environment-variables

But I would suggest trying the AWS Profile. You can add credentials to ~/.aws/credentials file like

```
[myprofile]
aws_access_key_id     = anaccesskey
aws_secret_access_key = asecretkey
```
## Terraform Lifecycle

![image](https://github.com/user-attachments/assets/d5611e27-afc8-439b-b462-a6a03393abd9)

# Getting started using Terraform

To get started building infrastructure resources using Terraform, there are few things that you should take care of. The general steps to deploy a resource(s) in the cloud are:

Set up a Cloud Account on any cloud provider (AWS, Azure, OCI)

Install Terraform

Add a provider – AWS, Azure, OCI, GCP, or others

Write configuration files

Initialize Terraform Providers

PLAN (DRY RUN) using terraform plan

APPLY (Create a Resource) using terraform apply

DESTROY (Delete a Resource) using terraform destroy






