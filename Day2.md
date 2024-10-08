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

Configuration file (*.tf files): Here we declare the provider and resources to be deployed along with the type of resource and all resources specific settings

=================================================================

URL to check list of all terraform supported providers https://registry.terraform.io/browse/providers

create a file name extension with .tf

exmaple: main.tf

edit file main.tf then add following code, following example for aws provider

```
provider "aws" {
 region = "us-east-1"
}
```
==========================================================================

### Versioning
The required_version setting can be used to constrain which version of the Terraform CLI can be used with your configuration. 

If the running version of Terraform doesn't match the constraints specified, Terraform will produce an error and exit without taking any further actions.

```
terraform {
 required_version = ">= 0.12"
}
```
The value for required_version is a string containing a comma-separated list of constraints.
Each constraint is an operator followed by a version number, such as > 0.12.0. 

The following constraint operators are allowed:

• = (or no operator): exact version equality !=: version not equal

• >, >=, <, <=: version comparison, where “greater than” is a larger versionnumber

• ~>: pessimistic constraint operator, constraining both the oldest and newest version allowed. 

For example, ~> 0.9 is equivalent to >= 0.9, < 1.0, and ~> 0.8.4, is equivalent to >= 0.8.4, < 0.9

==> We can also specify a provider version requirement

```
provider "aws" {
region = "us-east-1"
version = ">= 2.9.0"
}
```
==================================================================

## Resources

Terraform resource syntax

The syntax for defining a resource in Terraform typically follows this pattern:

```
resource "resource_type" "resource_name" {
  # Configuration settings for the resource
  attribute1 = value1
  attribute2 = value2
  # ...
}
```

1.resource: This keyword is used to declare a resource block.

2."resource_type": This is the type of resource you want to create. For example, if you’re creating an AWS EC2 instance with Terraform, the resource type would be "aws_instance".

3."resource_name": This is a user-defined name for the resource block. It must be unique within your Terraform configuration. It’s used as a reference to the resource elsewhere in your configuration.

4.{}: The opening and closing curly braces enclose the configuration settings for the resource. Inside the block, you define the attributes and their values for the resource.

#### Example:

```
resource "aws_instance" "myec2" {
 ami = "8bc8989"
 instance_type = "t2.micro"
 count = 3
}
```
==================================================================

## Terraform Init

The terraform init command is used to initialise a working directory containing Terraform configuration files.

Terraform must initialize the provider before it can be used.

Initialization downloads and installs the provider’s plugin so that it can later be executed.

Initializes the backend configuration.

```
terraform init
ls -la
```

## Terraform plan

The terraform plan command is used to create an execution plan.

It will not modify things in infrastructure.

Terraform performs a refresh, unless explicitly disabled, and then determines what actions are necessary to achieve the desired state specified in the configuration files.

This command is a convenient way to check whether the execution plan for a set of changes matches your expectations without making any changes to real resources or to the state.

```
$ terraform plan
```

## Terraform Apply

The terraform apply command is used to apply the changes required to reach the desired state of the configuration.

Terraform apply will also write data to the terraform.tfstate file.

Once the application is completed, resources are immediately available.

```
$ terraform apply

Apply and auto approve

$ terraform apply -auto-approve
```
## Terraform Refresh

The terraform refresh command is used to reconcile the state Terraform knows about (via its state file) with the real-world infrastructure.

This does not modify infrastructure but does modify the state file

## Terraform Destroy

The terraform destroy command is used to destroy the Terraform-managed infrastructure.

terraform destroy command is not the only command through which infrastructure can be destroyed.

```
$ terraform destroy
```

## Terraform Validate

The terraform validate command validates the configuration files in a directory.

Validate runs checks that verify whether a configuration is syntactically valid

```
$ terraform validate
```
