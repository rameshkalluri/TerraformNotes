## Understanding Terraform State File
- What is Terraform State ? 
  - It is the primary core thing for terraform to function
  - In a short way, its the underlying database containing the resources information which are provisioning using Terraform
  - **Primary Purpose:** To store bindings between objects in a remote system and resource instances declared in your configuration. 
  - When Terraform creates a remote object in response to a change of configuration, it will record the identity of that remote object against a particular resource instance, and then potentially update or delete that object in response to future configuration changes.
- Terraform state file created when we first run the `terraform apply`
- Terraform state file is created locally in working directory.
- If required, we can confiure the `backend block` in `terraform block` which will allow us to store state file remotely.  Storing remotely is recommended option which we will see in the next section of the course. 
