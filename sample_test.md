# learn_terraform

Here’s a concise crash course on the HashiCorp Terraform Associate exam:  

---

### **1. Terraform Basics**
- **Infrastructure as Code (IaC):** Declarative language to define infrastructure.
- **Providers:** Plugins for cloud services (e.g., AWS, Azure, GCP).  
  Example:  
  ```hcl
  provider "aws" {
    region = "us-west-2"
  }
  ```
- **Resources:** Components managed by Terraform (e.g., EC2, S3).  
  Example:  
  ```hcl
  resource "aws_instance" "example" {
    ami           = "ami-12345678"
    instance_type = "t2.micro"
  }
  ```

---

### **2. Core Concepts**
- **Terraform Files:** `.tf` files for configuration, `.tfstate` for state, `.tfvars` for variables.
- **Terraform Commands:**
  - `terraform init` - Initialize directory.
  - `terraform plan` - Preview changes.
  - `terraform apply` - Apply changes.
  - `terraform destroy` - Delete infrastructure.
- **State Management:**
  - Local or remote.
  - `terraform state list` - List resources.
  - `terraform state show <resource>` - View resource.

---

### **3. Variables and Outputs**
- **Defining Variables:**  
  ```hcl
  variable "instance_type" {
    default = "t2.micro"
    type    = string
  }
  ```
- **Referencing Variables:** `${var.instance_type}`.
- **Outputs:** Share information.  
  Example:  
  ```hcl
  output "instance_ip" {
    value = aws_instance.example.public_ip
  }
  ```

---

### **4. Terraform Modules**
- Grouped configurations to reuse.
- Structure: `main.tf`, `variables.tf`, `outputs.tf`.
- Example:  
  ```hcl
  module "vpc" {
    source = "./modules/vpc"
    cidr_block = "10.0.0.0/16"
  }
  ```

---

### **5. Remote Backends**
- Store state files remotely (e.g., S3, Azure Blob).
- Example:  
  ```hcl
  terraform {
    backend "s3" {
      bucket         = "my-bucket"
      key            = "path/to/terraform.tfstate"
      region         = "us-west-2"
    }
  }
  ```

---

### **6. Terraform Workspaces**
- For managing multiple environments (e.g., dev, prod).
  Commands:
  - `terraform workspace new dev`
  - `terraform workspace select dev`

---

### **7. Lifecycle Rules and Provisioners**
- **Lifecycle Rules:**  
  ```hcl
  lifecycle {
    prevent_destroy = true
  }
  ```
- **Provisioners:** Configure resources post-creation (e.g., `remote-exec`, `local-exec`).

---

### **8. Best Practices**
- Use `.terraformignore` for sensitive files.
- Version control for `.tfstate`.
- Modularize configurations for scalability.

---

### **9. Common Exam Topics**
- Understand Terraform workflow (init, plan, apply, destroy).
- Handling `terraform.tfstate` and locking mechanisms.
- Module creation and variable usage.
- Debugging Terraform with `TF_LOG`.

---

Here are some **mock questions** to help you practice for the Terraform Associate exam:  

---

### **Section 1: Terraform Basics**  
1. **What command initializes a directory containing Terraform configuration files?**  
   a) `terraform apply`  
   b) `terraform init`  
   c) `terraform setup`  
   d) `terraform start`  
   **Answer:** b) `terraform init`

2. **Which file contains the mapping between resources in the configuration and their real-world counterparts?**  
   a) `terraform.tf`  
   b) `.terraformignore`  
   c) `terraform.tfstate`  
   d) `backend.tf`  
   **Answer:** c) `terraform.tfstate`

---

### **Section 2: Variables and Outputs**  
3. **How do you define a default value for a variable in Terraform?**  
   ```hcl
   variable "region" {
       ________ = "us-west-1"
   }
   ```  
   a) `default`  
   b) `value`  
   c) `output`  
   d) `set`  
   **Answer:** a) `default`

4. **Given the output block below, how do you reference `instance_ip` in another configuration file?**  
   ```hcl
   output "instance_ip" {
       value = aws_instance.example.public_ip
   }
   ```  
   a) `output.instance_ip`  
   b) `module.instance_ip`  
   c) `aws_instance.example.instance_ip`  
   d) `module.<module_name>.instance_ip`  
   **Answer:** d) `module.<module_name>.instance_ip`

---

### **Section 3: State and Backends**  
5. **What happens if two team members attempt to run `terraform apply` simultaneously on the same backend?**  
   a) The first apply runs; the second is ignored.  
   b) Terraform locks the state file to prevent conflicts.  
   c) Both apply operations execute concurrently.  
   d) Terraform overwrites the backend with the most recent state.  
   **Answer:** b) Terraform locks the state file to prevent conflicts.

6. **Which backend is recommended for shared team collaboration?**  
   a) Local backend  
   b) Consul backend  
   c) Remote backend (e.g., S3)  
   d) Git backend  
   **Answer:** c) Remote backend (e.g., S3)

---

### **Section 4: Workspaces**  
7. **What command switches to a workspace named `prod`?**  
   a) `terraform workspace create prod`  
   b) `terraform workspace select prod`  
   c) `terraform workspace use prod`  
   d) `terraform workspace activate prod`  
   **Answer:** b) `terraform workspace select prod`

---

### **Section 5: Provisioners**  
8. **What is the purpose of provisioners in Terraform?**  
   a) Store state files remotely  
   b) Perform actions on resources post-creation  
   c) Manage multiple environments  
   d) Handle resource dependencies  
   **Answer:** b) Perform actions on resources post-creation

9. **Which provisioner allows you to execute a command locally on your machine?**  
   a) `remote-exec`  
   b) `local-exec`  
   c) `exec`  
   d) `custom-exec`  
   **Answer:** b) `local-exec`

---

### **Section 6: Advanced Concepts**  
10. **Which Terraform lifecycle argument ensures a resource will not be destroyed accidentally?**  
    a) `destroy_protect`  
    b) `prevent_destroy`  
    c) `safe_delete`  
    d) `immutable`  
    **Answer:** b) `prevent_destroy`

11. **What file is used to ignore sensitive or unnecessary files from being tracked by Terraform?**  
    a) `.terraformconfig`  
    b) `terraform.lock.hcl`  
    c) `.terraformignore`  
    d) `.tfvars`  
    **Answer:** c) `.terraformignore`

---

Here are some **mock questions** to help you practice for the Terraform Associate exam:  

---

### **Section 1: Terraform Basics**  
1. **What command initializes a directory containing Terraform configuration files?**  
   a) `terraform apply`  
   b) `terraform init`  
   c) `terraform setup`  
   d) `terraform start`  
   **Answer:** b) `terraform init`

2. **Which file contains the mapping between resources in the configuration and their real-world counterparts?**  
   a) `terraform.tf`  
   b) `.terraformignore`  
   c) `terraform.tfstate`  
   d) `backend.tf`  
   **Answer:** c) `terraform.tfstate`

---

### **Section 2: Variables and Outputs**  
3. **How do you define a default value for a variable in Terraform?**  
   ```hcl
   variable "region" {
       ________ = "us-west-1"
   }
   ```  
   a) `default`  
   b) `value`  
   c) `output`  
   d) `set`  
   **Answer:** a) `default`

4. **Given the output block below, how do you reference `instance_ip` in another configuration file?**  
   ```hcl
   output "instance_ip" {
       value = aws_instance.example.public_ip
   }
   ```  
   a) `output.instance_ip`  
   b) `module.instance_ip`  
   c) `aws_instance.example.instance_ip`  
   d) `module.<module_name>.instance_ip`  
   **Answer:** d) `module.<module_name>.instance_ip`

---

### **Section 3: State and Backends**  
5. **What happens if two team members attempt to run `terraform apply` simultaneously on the same backend?**  
   a) The first apply runs; the second is ignored.  
   b) Terraform locks the state file to prevent conflicts.  
   c) Both apply operations execute concurrently.  
   d) Terraform overwrites the backend with the most recent state.  
   **Answer:** b) Terraform locks the state file to prevent conflicts.

6. **Which backend is recommended for shared team collaboration?**  
   a) Local backend  
   b) Consul backend  
   c) Remote backend (e.g., S3)  
   d) Git backend  
   **Answer:** c) Remote backend (e.g., S3)

---

### **Section 4: Workspaces**  
7. **What command switches to a workspace named `prod`?**  
   a) `terraform workspace create prod`  
   b) `terraform workspace select prod`  
   c) `terraform workspace use prod`  
   d) `terraform workspace activate prod`  
   **Answer:** b) `terraform workspace select prod`

---

### **Section 5: Provisioners**  
8. **What is the purpose of provisioners in Terraform?**  
   a) Store state files remotely  
   b) Perform actions on resources post-creation  
   c) Manage multiple environments  
   d) Handle resource dependencies  
   **Answer:** b) Perform actions on resources post-creation

9. **Which provisioner allows you to execute a command locally on your machine?**  
   a) `remote-exec`  
   b) `local-exec`  
   c) `exec`  
   d) `custom-exec`  
   **Answer:** b) `local-exec`

---

### **Section 6: Advanced Concepts**  
10. **Which Terraform lifecycle argument ensures a resource will not be destroyed accidentally?**  
    a) `destroy_protect`  
    b) `prevent_destroy`  
    c) `safe_delete`  
    d) `immutable`  
    **Answer:** b) `prevent_destroy`

11. **What file is used to ignore sensitive or unnecessary files from being tracked by Terraform?**  
    a) `.terraformconfig`  
    b) `terraform.lock.hcl`  
    c) `.terraformignore`  
    d) `.tfvars`  
    **Answer:** c) `.terraformignore`

---

Here’s another set of **mock questions** for the Terraform Associate exam:

---

### **Section 7: Configuration and Syntax**  
1. **Which of the following is a valid way to reference a resource in another module?**  
   a) `resource.<module_name>.<resource_name>`  
   b) `module.<module_name>.<resource_name>`  
   c) `output.<module_name>.<resource_name>`  
   d) `module.resource.<resource_name>`  
   **Answer:** b) `module.<module_name>.<resource_name>`

2. **What is the correct syntax to use a conditional expression in Terraform?**  
   a) `condition ? true_expression : false_expression`  
   b) `condition : true_expression ? false_expression`  
   c) `if condition then true_expression else false_expression`  
   d) `condition ? false_expression : true_expression`  
   **Answer:** a) `condition ? true_expression : false_expression`

---

### **Section 8: Providers**  
3. **What happens if you do not specify a provider version in your configuration?**  
   a) Terraform uses the latest version available.  
   b) Terraform uses the oldest compatible version.  
   c) Terraform throws an error.  
   d) Terraform downloads all versions for backward compatibility.  
   **Answer:** a) Terraform uses the latest version available.

4. **How do you specify a specific provider version in your configuration?**  
   ```hcl
   provider "aws" {
       __________ = "~> 3.0"
   }
   ```  
   a) `version`  
   b) `provider_version`  
   c) `aws_version`  
   d) `plugin_version`  
   **Answer:** a) `version`

---

### **Section 9: State Management**  
5. **How do you move a resource from one Terraform state file to another?**  
   a) `terraform split`  
   b) `terraform move`  
   c) `terraform state mv`  
   d) `terraform migrate`  
   **Answer:** c) `terraform state mv`

6. **What command would you use to remove a resource from the state without destroying it?**  
   a) `terraform state rm`  
   b) `terraform destroy`  
   c) `terraform apply --ignore`  
   d) `terraform state forget`  
   **Answer:** a) `terraform state rm`

---

### **Section 10: Modules**  
7. **Which of the following is a recommended practice when using modules in Terraform?**  
   a) Store modules in the same folder as the main configuration.  
   b) Hardcode variable values in modules.  
   c) Use a version control system for module sources.  
   d) Avoid using outputs in modules.  
   **Answer:** c) Use a version control system for module sources.

8. **What command is used to update modules to the latest version specified?**  
   a) `terraform init`  
   b) `terraform refresh`  
   c) `terraform module update`  
   d) `terraform get -update`  
   **Answer:** d) `terraform get -update`

---

### **Section 11: Workspaces and Environments**  
9. **What is the default workspace in Terraform?**  
   a) `default`  
   b) `main`  
   c) `root`  
   d) `base`  
   **Answer:** a) `default`

10. **Which Terraform command lists all existing workspaces?**  
    a) `terraform workspace list`  
    b) `terraform workspaces`  
    c) `terraform workspace show`  
    d) `terraform list workspaces`  
    **Answer:** a) `terraform workspace list`

---

### **Section 12: Debugging and Logging**  
11. **How do you enable detailed logs for debugging in Terraform?**  
    a) Use the `--debug` flag with Terraform commands.  
    b) Set the environment variable `TF_LOG` to the desired log level.  
    c) Add `debug = true` to the Terraform configuration.  
    d) Enable logging in the backend configuration.  
    **Answer:** b) Set the environment variable `TF_LOG` to the desired log level.

12. **Which command allows you to validate the syntax of your Terraform configuration?**  
    a) `terraform plan`  
    b) `terraform validate`  
    c) `terraform init --check`  
    d) `terraform debug`  
    **Answer:** b) `terraform validate`

---

### **Section 13: Best Practices**  
13. **What is the purpose of a `terraform.lock.hcl` file?**  
    a) Stores the latest state of resources.  
    b) Ensures consistent provider versions.  
    c) Tracks environment variables.  
    d) Configures remote state locking.  
    **Answer:** b) Ensures consistent provider versions.

14. **Why should sensitive data not be stored in `.tfvars` files?**  
    a) Terraform cannot parse `.tfvars` files.  
    b) They are automatically shared across modules.  
    c) They might be accidentally committed to version control.  
    d) They are not supported in remote backends.  
    **Answer:** c) They might be accidentally committed to version control.

---

### Scenario Based Questions

Here are some **scenario-based questions** to help you prepare for the Terraform Associate exam:  

---

### **Scenario 1: Multi-environment Setup**
**Question:**  
Your company has environments for `development`, `staging`, and `production`. You’ve been asked to set up infrastructure using Terraform such that configurations can be reused, but resources for each environment must remain isolated.  

1. **How would you configure Terraform to manage multiple environments?**  
   a) Use a separate Terraform configuration file for each environment.  
   b) Use workspaces to manage multiple environments.  
   c) Use different backends for each environment.  
   d) Use conditional expressions to toggle configurations for each environment.  

**Answer:** b) Use workspaces to manage multiple environments.

2. **What command would you use to switch to the `staging` environment?**  
   **Answer:** `terraform workspace select staging`

---

### **Scenario 2: Remote State Storage**
**Question:**  
You are working in a team and need to ensure that Terraform state files are stored securely and accessible to everyone in the team. The state files must also be locked during operations to prevent conflicts.  

1. **Which backend would you use to achieve this?**  
   a) Local  
   b) Remote backend (e.g., S3 with DynamoDB)  
   c) Consul  
   d) Git  

**Answer:** b) Remote backend (e.g., S3 with DynamoDB)

2. **What additional configuration is required to enable state locking?**  
   **Answer:** Use DynamoDB for state locking in conjunction with the S3 backend.

---

### **Scenario 3: Module Reusability**
**Question:**  
Your team created a module for setting up an S3 bucket. Another team wants to reuse this module but with different bucket names and tags.  

1. **How would you design the module to support reusability?**  
   a) Hardcode the bucket name and tags in the module.  
   b) Use variables for bucket name and tags.  
   c) Define separate modules for each team.  
   d) Include the bucket name and tags in the output.  

**Answer:** b) Use variables for bucket name and tags.

2. **How would the other team reference your module?**  
   **Answer:**  
   ```hcl
   module "s3_bucket" {
       source      = "./path-to-module"
       bucket_name = "team-bucket"
       tags        = {
           Environment = "Production"
       }
   }
   ```

---

### **Scenario 4: Debugging Configuration Errors**
**Question:**  
You applied your Terraform configuration, but the EC2 instance was not created. After reviewing the `terraform plan` output, you suspect a variable is missing.  

1. **What command helps you validate the configuration to identify syntax issues?**  
   **Answer:** `terraform validate`

2. **What Terraform logging option can you enable for deeper insights during execution?**  
   **Answer:** Set `TF_LOG=DEBUG` in your environment.

---

### **Scenario 5: Handling Sensitive Data**
**Question:**  
You are defining a Terraform configuration for a database, and the database password must remain secure.  

1. **What’s the best way to handle sensitive values such as the database password?**  
   a) Hardcode the password in the Terraform configuration.  
   b) Use a `.tfvars` file to define the password.  
   c) Use environment variables or a secrets management tool like HashiCorp Vault.  
   d) Store the password in a remote state file.  

**Answer:** c) Use environment variables or a secrets management tool like HashiCorp Vault.

2. **How can you ensure the password value is not displayed in the Terraform plan or state file?**  
   **Answer:** Mark the variable as sensitive:  
   ```hcl
   variable "db_password" {
       type      = string
       sensitive = true
   }
   ```

---

### **Scenario 6: Resource Dependency**
**Question:**  
You have two resources: an S3 bucket and a Lambda function. The Lambda function’s deployment package must be uploaded to the S3 bucket.  

1. **How do you ensure the Lambda function is created only after the S3 bucket is ready?**  
   a) Use the `depends_on` argument in the Lambda resource.  
   b) Use a provisioner to wait for the S3 bucket.  
   c) Manually run Terraform for each resource.  
   d) Add a lifecycle rule to the Lambda function.  

**Answer:** a) Use the `depends_on` argument in the Lambda resource.

2. **What does the configuration look like?**  
   **Answer:**  
   ```hcl
   resource "aws_s3_bucket" "example" {
       bucket = "my-lambda-bucket"
   }

   resource "aws_lambda_function" "example" {
       function_name = "my-lambda"
       s3_bucket     = aws_s3_bucket.example.bucket
       depends_on    = [aws_s3_bucket.example]
   }
   ```

---

### **Scenario 7: Updating Infrastructure**
**Question:**  
You need to update the instance type of an existing EC2 instance from `t2.micro` to `t3.micro`.  

1. **What command previews the changes before applying them?**  
   **Answer:** `terraform plan`

2. **What happens to the EC2 instance when the change is applied?**  
   a) The instance is updated in place.  
   b) The instance is destroyed and recreated.  
   c) The instance is temporarily stopped and restarted.  
   d) The instance remains unchanged.  

**Answer:** b) The instance is destroyed and recreated (if `instance_type` cannot be updated in place).

---

Here are more **scenario-based questions** to broaden your preparation for the Terraform Associate exam:  

---

### **Scenario 8: Rolling Back Changes**  
**Question:**  
You applied a Terraform configuration, but a misconfiguration led to the creation of unwanted resources.  

1. **What is the fastest way to remove the unwanted resources while preserving the existing infrastructure?**  
   a) Use `terraform destroy`.  
   b) Manually delete the resources in the cloud console.  
   c) Remove the misconfigured resources from the `.tf` file and run `terraform apply`.  
   d) Use `terraform state rm` to remove the resources.  

**Answer:** c) Remove the misconfigured resources from the `.tf` file and run `terraform apply`.

2. **What is the risk of manually deleting resources outside of Terraform?**  
   **Answer:** Terraform's state file will become inconsistent with the actual infrastructure, leading to potential errors during future runs.

---

### **Scenario 9: Working with Outputs**  
**Question:**  
You have created an EC2 instance, and your team needs its public IP to configure another system.  

1. **How would you expose the instance's public IP using Terraform?**  
   **Answer:**  
   ```hcl
   resource "aws_instance" "example" {
       ami           = "ami-12345678"
       instance_type = "t2.micro"
   }

   output "instance_public_ip" {
       value = aws_instance.example.public_ip
   }
   ```

2. **What command allows you to view the output value after applying the configuration?**  
   **Answer:** `terraform output`

---

### **Scenario 10: Resource Drift Detection**  
**Question:**  
A team member manually modified an S3 bucket's settings through the AWS Management Console. You suspect the state file is no longer aligned with the real-world infrastructure.  

1. **What command can you use to detect the drift?**  
   a) `terraform validate`  
   b) `terraform refresh`  
   c) `terraform plan`  
   d) `terraform state list`  

**Answer:** b) `terraform refresh`

2. **How can you bring the configuration and the actual state back into alignment?**  
   **Answer:** Run `terraform plan` to review the differences and `terraform apply` to reconcile the changes.

---

### **Scenario 11: Dynamic Blocks**  
**Question:**  
You need to configure multiple ingress rules for a security group, but the number and details of these rules will depend on a list of CIDR blocks defined as a variable.  

1. **How would you implement this in Terraform?**  
   **Answer:** Use a `dynamic` block:  
   ```hcl
   resource "aws_security_group" "example" {
       name = "example"

       dynamic "ingress" {
           for_each = var.cidr_blocks
           content {
               cidr_blocks = [ingress.value]
               from_port   = 80
               to_port     = 80
               protocol    = "tcp"
           }
       }
   }
   ```

2. **What would you define in your variables?**  
   **Answer:**  
   ```hcl
   variable "cidr_blocks" {
       default = ["10.0.0.0/16", "192.168.1.0/24"]
   }
   ```

---

### **Scenario 12: Handling Resource Dependencies**  
**Question:**  
You need to deploy an RDS database instance, but it should not start provisioning until a VPC and a subnet are created.  

1. **How does Terraform handle implicit dependencies?**  
   **Answer:** If one resource references attributes of another (e.g., using `vpc_id`), Terraform automatically infers the dependency.  

2. **What happens if dependencies are not explicitly or implicitly declared?**  
   **Answer:** Terraform may attempt to create resources in parallel, which can result in failures if a resource depends on another that hasn’t been created yet.

---

### **Scenario 13: Remote Backend Migration**  
**Question:**  
Your team has been using a local backend to store the Terraform state file but now wants to migrate to an S3 remote backend.  

1. **What steps would you take to migrate the backend?**  
   **Answer:**  
   - Configure the remote backend in the `terraform` block:  
     ```hcl
     terraform {
         backend "s3" {
             bucket         = "my-terraform-state"
             key            = "global/terraform.tfstate"
             region         = "us-west-2"
         }
     }
     ```
   - Run `terraform init` and confirm the migration.

2. **What happens if you skip the migration confirmation?**  
   **Answer:** Terraform will not transfer the existing state, and you risk overwriting or losing your infrastructure's state.

---

### **Scenario 14: Resource Count and For-Each**  
**Question:**  
You are deploying multiple EC2 instances using a list of AMI IDs.  

1. **How would you define a resource to provision one instance per AMI ID?**  
   **Answer:** Use `for_each` or `count`:  
   ```hcl
   variable "ami_ids" {
       default = ["ami-123", "ami-456"]
   }

   resource "aws_instance" "example" {
       count         = length(var.ami_ids)
       ami           = var.ami_ids[count.index]
       instance_type = "t2.micro"
   }
   ```

2. **What is the difference between `count` and `for_each`?**  
   **Answer:**  
   - `count` is index-based and useful for lists.  
   - `for_each` is key-value based and works well for maps or sets.

---

### **Scenario 15: Lifecycle Management**  
**Question:**  
A critical S3 bucket should not be destroyed even if it is removed from the configuration.  

1. **How can you ensure this?**  
   **Answer:** Add a lifecycle rule to the bucket resource:  
   ```hcl
   resource "aws_s3_bucket" "example" {
       bucket = "critical-bucket"

       lifecycle {
           prevent_destroy = true
       }
   }
   ```

2. **What happens if you try to destroy the bucket?**  
   **Answer:** Terraform will throw an error and prevent the destruction.

---

