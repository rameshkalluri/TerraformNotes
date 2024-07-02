## Understanding Terraform State File
- What is Terraform State ? 
  - It is the primary core thing for terraform to function
  - In a short way, its the underlying database containing the resources information which are provisioning using Terraform
  - **Primary Purpose:** To store bindings between objects in a remote system and resource instances declared in your configuration. 
  - When Terraform creates a remote object in response to a change of configuration, it will record the identity of that remote object against a particular resource instance, and then potentially update or delete that object in response to future configuration changes.
- Terraform state file created when we first run the `terraform apply`
- Terraform state file is created locally in working directory.
- If required, we can confiure the `backend block` in `terraform block` which will allow us to store state file remotely.  Storing remotely is recommended option which we will see in the next section of the course. 

## Review terraform.tfstate file
- Terraform State files are JSON based
- Manual editing of Terraform state files is highly not recommended
- Review `terraform.tfstate` file step by step

## Resource: Update In-Place: Make changes by adding new tag to EC2 Instance 
- Add a new tag in `c2-ec2-instance.tf`
```
# Add this for EC2 Instance tags
    "tag1" = "Update-test-1"
```
- Review Terraform Plan
```
# Review the terraform plan
terraform plan 
Observation: You should see "~ update in-place" 
"Plan: 0 to add, 1 to change, 0 to destroy."

# Create / Update Resources 
terraform apply -auto-approve
Observation: "Apply complete! Resources: 0 added, 1 changed, 0 destroyed."
```
- **Important Note:** Here we have seen example for **update in-place**


## Resource: Destroy and Re-create Resources: Update Availability Zone
- This will destroy the EC2 Instance in 1 AZ and re-creates in other AZ
```
# Before
  availability_zone = "us-east-1a"

# After
  availability_zone = "us-east-1b"  
```
```
# Review the terraform plan
terraform plan 
Observation: 
1) -/+ destroy and then create replacement
2) # aws_instance.my-ec2-vm must be "replaced"
3) # aws_instance.my-ec2-vm must be "replaced" - This parameter forces replacement
4) "Plan: 1 to add, 0 to change, 1 to destroy."

# Create / Update Resources 
terraform apply -auto-approve
Observation: "Apply complete! Resources: 1 added, 0 changed, 1 destroyed."
```


## Resource: Destroy Resource
```
# Destroy Resource
terraform destroy 
Observation: 
1) - destroy
2) # aws_instance.my-ec2-vm will be destroyed
3) Plan: 0 to add, 0 to change, 1 to destroy
4) Destroy complete! Resources: 1 destroyed
```

## Understand Desired and Current States (High-Level Only)
- **Desired State:** Local Terraform Manifest (All *.tf files)
- **Current State:**  Real Resources present in your cloud

## Clean-Up
```
# Destroy Resource
terraform destroy -auto-approve 

# Remove Terraform Files
rm -rf .terraform*
rm -rf terraform.tfstate*
```

## References
- [Terraform State](https://www.terraform.io/docs/language/state/index.html)
- [Manipulating Terraform State](https://www.terraform.io/docs/cli/state/index.html)
  

# Terraform Remote State Storage & Locking

## Step-01: Introduction
- Understand Terraform Backends
- Understand about Remote State Storage and its advantages
- This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment.
- Create AWS S3 bucket to store `terraform.tfstate` file and enable backend configurations in terraform settings block
- Understand about **State Locking** and its advantages
- Create DynamoDB Table and  implement State Locking by enabling the same in Terraform backend configuration

## Step-02: Create S3 Bucket
- Go to Services -> S3 -> Create Bucket
- **Bucket name:** terraform-stacksimplify
- **Region:** US-East (N.Virginia)
- **Bucket settings for Block Public Access:** leave to defaults
- **Bucket Versioning:** Enable
- Rest all leave to **defaults**
- Click on **Create Bucket**
- **Create Folder**
  - **Folder Name:** dev
  - Click on **Create Folder**


## Step-03: Terraform Backend Configuration
- **Reference Sub-folder:** terraform-manifests
- [Terraform Backend as S3](https://www.terraform.io/docs/language/settings/backends/s3.html)
- Add the below listed Terraform backend block in `Terrafrom Settings` block in `main.tf`
```
# Terraform Backend Block
  backend "s3" {
    bucket = "terraform-stacksimplify"
    key    = "dev/terraform.tfstate"
    region = "us-east-1"    
  }
```

## Step-04: Test with Remote State Storage Backend
```t
# Initialize Terraform
terraform init

Observation: 
Successfully configured the backend "s3"! Terraform will automatically
use this backend unless the backend configuration changes.

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate

# Validate Terraform configuration files
terraform validate

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate

# Format Terraform configuration files
terraform fmt

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate

# Review the terraform plan
terraform plan 

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate

# Create Resources 
terraform apply -auto-approve

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate
Observation: Finally at this point you should see the terraform.tfstate file in s3 bucket

# Access Application
http://<Public-DNS>
```

## Step-05: Bucket Versioning - Test
- Update in `c2-variables.tf` 
```t
variable "instance_type" {
  description = "EC2 Instance Type - Instance Sizing"
  type = string
  #default = "t2.micro"
  default = "t2.small"
}
```
- Execute Terraform Commands
```t
# Review the terraform plan
terraform plan 

# Create Resources 
terraform apply -auto-approve

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev/terraform.tfstate
Observation: New version of terraform.tfstate file will be created
```


## Step-06: Destroy Resources
- Destroy Resources and Verify Bucket Versioning
```t
# Destroy Resources
terraform destroy -auto-approve
```
## Step-07: Terraform State Locking Introduction
- Understand about Terraform State Locking Advantages

## Step-08: Add State Locking Feature using DynamoDB Table
- Create Dynamo DB Table
  - **Table Name:** terraform-dev-state-table
  - **Partition key (Primary Key):** LockID (Type as String)
  - **Table settings:** Use default settings (checked)
  - Click on **Create**

## Step-09: Update DynamoDB Table entry in backend in c1-versions.tf
- Enable State Locking in `c1-versions.tf`
```t
  # Adding Backend as S3 for Remote State Storage with State Locking
  backend "s3" {
    bucket = "terraform-stacksimplify"
    key    = "dev2/terraform.tfstate"
    region = "us-east-1"  

    # For State Locking
    dynamodb_table = "terraform-dev-state-table"
  }
```

## Step-10: Execute Terraform Commands
```t
# Initialize Terraform 
terraform init

# Review the terraform plan
terraform plan 
Observation: 
1) Below messages displayed at start and end of command
Acquiring state lock. This may take a few moments...
Releasing state lock. This may take a few moments...
2) Verify DynamoDB Table -> Items tab

# Create Resources 
terraform apply -auto-approve

# Verify S3 Bucket for terraform.tfstate file
bucket-name/dev2/terraform.tfstate
Observation: New version of terraform.tfstate file will be created in dev2 folder
```

## Step-11: Destroy Resources
- Destroy Resources and Verify Bucket Versioning
```t
# Destroy Resources
terraform destroy -auto-approve

# Clean-Up Files
rm -rf .terraform*
rm -rf terraform.tfstate*  # This step not needed as e are using remote state storage here
```

## References 
- [AWS S3 Backend](https://www.terraform.io/docs/language/settings/backends/s3.html)
- [Terraform Backends](https://www.terraform.io/docs/language/settings/backends/index.html)
- [Terraform State Storage](https://www.terraform.io/docs/language/state/backends.html)
- [Terraform State Locking](https://www.terraform.io/docs/language/state/locking.html)
- [Remote Backends - Enhanced](https://www.terraform.io/docs/language/settings/backends/remote.html)
