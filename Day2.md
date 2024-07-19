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

## Terraform Providers

A provider is responsible for understanding API interactions and exposing resources. 

It is an executable plug-in that contains code necessary to interact with the API of the service. 

Terraform configurations must declare which providers they require so that Terraform can install and use them.


![image](https://github.com/user-attachments/assets/9578aa17-4c1f-4e97-adca-ecb40526a612)

erraform has over a hundred providers for different technologies, and each provider then gives terraform user access to its resources.

So through AWS provider, for example, you have access to hundreds of AWS resources like EC2 instances, the AWS users, etc.

## Terraform Configuration Files

Configuration files are a set of files used to describe infrastructure in Terraform and have the file extensions .tf and .tf.json.

Terraform uses a declarative model for defining infrastructure. 

Configuration files let you write a configuration that declares your desired state. 

Configuration files are made up of resources with settings and values representing the desired state of your infrastructure.


![image](https://github.com/user-attachments/assets/24f958fa-df66-4d47-9fee-a2bd29952d4e)

A Terraform configuration is made up of one or more files in a directory, provider binaries, plan files, and state files once Terraform has run the configuration.

1. Configuration file (*.tf files): Here we declare the provider and resources to be deployed along with the type of resource and all resources specific settings

2. Variable declaration file (variables.tf or variables.tf.json): Here we declare the input variables required to provision resources

3. Variable definition files (terraform.tfvars): Here we assign values to the input variables

4. State file (terraform.tfstate): a state file is created once after Terraform is run. It stores state about our managed infrastructure.

=================================================================

create a file name extension with .tf

exmaple: main.tf

edit file main.tf then add following code, following example for aws provider

```
provider "aws" {
 region = "us-east-1"
}
```

URL to check list of all terraform supported providers https://registry.terraform.io/browse/providers
