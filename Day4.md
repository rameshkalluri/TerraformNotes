## Input Variables

variable "aws_region" {
  description = "Region in which AWS resources to be created"
  type        = string
  default     = "us-east-1"
}

## output Variables

output "ec2_instance_privateip" {
  description = "EC2 Instance Private IP"
  value = aws_instance.my-ec2-vm.private_ip 
}

In Terraform, variable precedence determines the order in which Terraform reads and applies variable values. Here's the order of precedence, from highest to lowest:

1. Terraform Cloud/Enterprise Environment Variables:

TF_VAR_: Environment variables prefixed with TF_VAR_ are the highest precedence. For example, TF_VAR_variable_name.

3. Command-Line Flags:

-var and -var-file: Variables specified directly in the command line using the -var or -var-file options when running terraform plan or terraform apply.

4. Variable Definitions Files:

terraform.tfvars and terraform.tfvars.json: Files named terraform.tfvars or terraform.tfvars.json are automatically loaded if present.

*.auto.tfvars and *.auto.tfvars.json: Any files ending in .auto.tfvars or .auto.tfvars.json are also automatically loaded.

5. Environment Variables:

TF_VAR_: Environment variables prefixed with TF_VAR_ for other variable types.

6. Default Values:

Default values in the variable blocks: If no other value is provided, the default value specified in the variable definition is used.

Detailed Order of Precedence:

Terraform Cloud/Enterprise Environment Variables: Any environment variables set in the Terraform Cloud or Enterprise workspace.

Command-Line Flags:
-var 'variable_name=value': Directly set the variable value.
-var-file=filename: Use a file to specify variable values.
Auto-Loaded Variable Definitions Files:
terraform.tfvars or terraform.tfvars.json
Any files matching *.auto.tfvars or *.auto.tfvars.json
Environment Variables: Set with the TF_VAR_ prefix, e.g., TF_VAR_variable_name=value.
Default Values: Specified in the variable block within the Terraform configuration.
Example:
Given the following variable definition in your Terraform configuration:

hcl
Copy code
variable "example_variable" {
  type    = string
  default = "default_value"
}
The variable example_variable can have its value overridden by (in order of precedence):

Environment Variable:
bash
Copy code
export TF_VAR_example_variable="env_value"
Command-Line Flag:
bash
Copy code
terraform apply -var 'example_variable=cli_value'
Variable Definitions File (terraform.tfvars or *.auto.tfvars):
hcl
Copy code
example_variable = "tfvars_value"
Default Value: "default_value" (if no other value is set).
