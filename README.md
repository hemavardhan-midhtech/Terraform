# Terraform

## What is Terraform?

Terraform is an open-source Infrastructure as Code (IaC) tool created by HashiCorp.

It allows you to:

* Provision cloud infrastructure using code
* Automate infrastructure deployment
* Manage resources consistently across environments
* Version control infrastructure
* Deploy resources on AWS, Azure, GCP, and other platforms

Terraform uses **HCL (HashiCorp Configuration Language)** to define infrastructure. ([Udemy][2])

---

# Why Terraform?

### Without Terraform

```text
Login to AWS
Create EC2
Create VPC
Create Security Groups
Configure Networking
Repeat for every environment
```

Problems:

* Manual work
* Human errors
* Difficult to reproduce
* Hard to scale

---

### With Terraform

```text
Write Code Once
terraform init
terraform plan
terraform apply
```

Benefits:

* Automation
* Consistency
* Reusability
* Version Control
* Easy Rollback

---

# Terraform Workflow

```text
Write Terraform Code
        ↓
terraform init
        ↓
terraform validate
        ↓
terraform plan
        ↓
terraform apply
        ↓
Infrastructure Created
```

---

# Terraform Installation Check

```bash
terraform version
```

Output:

```bash
Terraform v1.x.x
```

---

# Basic Terraform File Structure

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── provider.tf
```

---

# Provider Block

Example AWS Provider:

```hcl
provider "aws" {
  region = "us-east-1"
}
```

Provider = Cloud Platform Connection

Examples:

* AWS
* Azure
* Google Cloud

---

# Resource Block

Create EC2 Instance

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

Syntax:

```hcl
resource "<resource_type>" "<resource_name>" {
}
```

---

# Important Terraform Commands

## Initialize Project

```bash
terraform init
```

Downloads:

* Providers
* Plugins

---

## Validate Code

```bash
terraform validate
```

Checks:

* Syntax errors
* Configuration errors

---

## Format Code

```bash
terraform fmt
```

Auto-formats Terraform files.

---

## Preview Changes

```bash
terraform plan
```

Shows:

```text
What will be created
What will be modified
What will be destroyed
```

---

## Apply Changes

```bash
terraform apply
```

Creates infrastructure.

Auto approve:

```bash
terraform apply -auto-approve
```

---

## Destroy Infrastructure

```bash
terraform destroy
```

Deletes all resources created by Terraform.

```bash
terraform destroy -auto-approve
```

---

# Variables

variables.tf

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

main.tf

```hcl
instance_type = var.instance_type
```

---

# Outputs

outputs.tf

```hcl
output "instance_public_ip" {
  value = aws_instance.web.public_ip
}
```

Display:

```bash
terraform output
```

---

# Terraform State

Terraform stores infrastructure information in:

```text
terraform.tfstate
```

Purpose:

* Tracks resources
* Detects changes
* Maintains infrastructure status

Never manually edit:

```text
terraform.tfstate
```

---

# Common Terraform Commands

```bash
terraform init
terraform validate
terraform fmt
terraform plan
terraform apply
terraform destroy
terraform show
terraform output
terraform version
terraform state list
```

---

# Example Complete EC2 Deployment

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"

  tags = {
    Name = "Terraform-Server"
  }
}

output "public_ip" {
  value = aws_instance.web.public_ip
}
```

Deploy:

```bash
terraform init
terraform plan
terraform apply
```

Destroy:

```bash
terraform destroy
```

---

# Terraform Best Practices

* Store code in GitHub
* Use variables instead of hardcoding values
* Keep state files secure
* Use remote state storage
* Organize code into modules
* Run `terraform plan` before `terraform apply`
* Use separate environments (Dev, QA, Prod)

---

# Terraform Interview Questions

### What is Terraform?

Infrastructure as Code tool used to provision and manage infrastructure through code.

### What is a Provider?

Plugin that connects Terraform to a cloud platform.

Examples:

* AWS
* Azure
* GCP

### What is Terraform State?

A file that stores current infrastructure information.

### Difference between Plan and Apply?

```text
terraform plan
```

Preview changes.

```text
terraform apply
```

Execute changes.

### What is Infrastructure as Code?

Managing infrastructure using configuration files instead of manual creation.

### What is Terraform Module?

Reusable collection of Terraform configurations.

---

# Terraform Learning Roadmap

```text
Terraform Basics
       ↓
Providers
       ↓
Resources
       ↓
Variables
       ↓
Outputs
       ↓
State Management
       ↓
Modules
       ↓
Remote Backend
       ↓
AWS Infrastructure
       ↓
CI/CD Integration
       ↓
Production Deployments
```

This aligns with the course's Terraform objective of learning **Infrastructure as Code**, cloud resource provisioning, and automation within modern DevOps workflows. ([Udemy][1])

[1]: https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/?srsltid=AfmBOooX0G13veqmlLyeelu53ccGleAHoSlb8Bvlbqs9QXa9S3ZZ_2Kq&utm_source=chatgpt.com "DevOps for beginners: Docker, K8s, AWS & Azure + 4 ..."
[2]: https://www.udemy.com/topic/terraform/?p=43&srsltid=AfmBOoqVXqh0ccWTvo8yJ2UTanTmBIb3IGig98qAKOjcezrTDU6qR00x&utm_source=chatgpt.com "Top Terraform Courses Online - Updated [March 2026]"


Great idea. If you're pushing this to GitHub as a Terraform reference guide, adding a **Troubleshooting Section** makes it much more useful for interviews, labs, and real projects.

# Terraform Troubleshooting Guide

---

## 1. Provider Plugin Not Found

### Error

```bash
Error: Failed to query available provider packages
```

### Cause

* Provider not downloaded
* Internet connectivity issue
* Incorrect provider version

### Fix

```bash
terraform init
```

Reconfigure providers:

```bash
terraform init -upgrade
```

---

## 2. AWS Credentials Not Found

### Error

```bash
Error: No valid credential sources found
```

### Cause

Terraform cannot authenticate with AWS.

### Fix

Verify AWS credentials:

```bash
aws configure
```

Check identity:

```bash
aws sts get-caller-identity
```

Environment variables:

```bash
export AWS_ACCESS_KEY_ID=YOUR_KEY
export AWS_SECRET_ACCESS_KEY=YOUR_SECRET
export AWS_DEFAULT_REGION=us-east-1
```

---

## 3. Terraform Init Failed

### Error

```bash
terraform init
```

returns:

```bash
Error installing provider
```

### Fix

Clear cache:

```bash
rm -rf .terraform
rm .terraform.lock.hcl
```

Reinitialize:

```bash
terraform init
```

---

## 4. Invalid Terraform Syntax

### Error

```bash
Error: Invalid block definition
```

### Cause

* Missing braces
* Incorrect indentation
* Wrong HCL syntax

### Fix

Validate code:

```bash
terraform validate
```

Format automatically:

```bash
terraform fmt
```

---

## 5. Resource Already Exists

### Error

```bash
Error: Resource already exists
```

### Cause

Terraform is trying to create a resource that already exists.

### Fix

Import existing resource:

```bash
terraform import aws_instance.web i-1234567890
```

Verify state:

```bash
terraform state list
```

---

## 6. State File Lock Error

### Error

```bash
Error acquiring the state lock
```

### Cause

* Another Terraform process is running
* Previous execution crashed

### Fix

Force unlock:

```bash
terraform force-unlock LOCK_ID
```

Find active processes:

```bash
ps -ef | grep terraform
```

---

## 7. Terraform Plan Shows Unexpected Changes

### Error

```bash
terraform plan
```

Shows resources changing unexpectedly.

### Cause

* Manual cloud changes
* State drift

### Fix

Refresh state:

```bash
terraform refresh
```

Or:

```bash
terraform plan -refresh-only
```

---

## 8. Permission Denied Error

### Error

```bash
AccessDenied
UnauthorizedOperation
```

### Cause

IAM user lacks permissions.

### Fix

Verify permissions:

```bash
aws iam get-user
```

Check attached policies:

```bash
aws iam list-attached-user-policies --user-name USERNAME
```

Common required permissions:

* EC2
* VPC
* IAM
* S3
* EKS

---

## 9. Terraform State Corrupted

### Symptoms

```bash
terraform apply
```

fails unexpectedly.

### Fix

Backup state:

```bash
cp terraform.tfstate terraform.tfstate.backup
```

Inspect state:

```bash
terraform show
```

List resources:

```bash
terraform state list
```

---

## 10. Resource Dependency Issues

### Error

```bash
Dependency cycle detected
```

### Cause

Two resources depend on each other.

### Fix

Use:

```hcl
depends_on = [aws_vpc.main]
```

Example:

```hcl
resource "aws_subnet" "app" {
  depends_on = [aws_vpc.main]
}
```

---

## 11. Variable Not Defined

### Error

```bash
Error: Reference to undeclared input variable
```

### Fix

variables.tf

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

Reference:

```hcl
instance_type = var.instance_type
```

---

## 12. Backend Initialization Error

### Error

```bash
Backend initialization required
```

### Fix

```bash
terraform init -reconfigure
```

or

```bash
terraform init -migrate-state
```

---

## 13. Terraform Apply Hanging

### Symptoms

```bash
terraform apply
```

stuck for a long time.

### Debug

```bash
TF_LOG=DEBUG terraform apply
```

Linux/macOS:

```bash
export TF_LOG=DEBUG
terraform apply
```

Windows:

```powershell
$env:TF_LOG="DEBUG"
terraform apply
```

---

## 14. Destroy Fails

### Error

```bash
terraform destroy
```

cannot remove resources.

### Cause

* Dependency conflicts
* Manual modifications

### Fix

Check state:

```bash
terraform state list
```

Destroy specific resource:

```bash
terraform destroy -target=aws_instance.web
```

---

## 15. Module Not Found

### Error

```bash
Module not installed
```

### Fix

```bash
terraform init
```

Upgrade modules:

```bash
terraform get -update
```

---

## Terraform Debugging Commands

```bash
terraform validate
terraform fmt
terraform plan
terraform show
terraform output
terraform state list
terraform state show RESOURCE
terraform graph
terraform refresh
terraform force-unlock LOCK_ID
```

---

## Emergency Recovery Checklist

### Backup State

```bash
cp terraform.tfstate terraform.tfstate.backup
```

### Verify Configuration

```bash
terraform validate
```

### Check Planned Changes

```bash
terraform plan
```

### Inspect Resources

```bash
terraform state list
```

### Reinitialize Environment

```bash
rm -rf .terraform
rm .terraform.lock.hcl
terraform init
```

---

# Terraform Project Structure (Recommended)

```text
terraform-project/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
├── terraform.tfvars
├── backend.tf
├── modules/
│   ├── vpc/
│   ├── ec2/
│   └── security-group/
│
├── environments/
│   ├── dev/
│   ├── qa/
│   └── prod/
│
└── README.md
```

## Quick Troubleshooting Flow

```text
terraform validate
        ↓
terraform fmt
        ↓
terraform init
        ↓
terraform plan
        ↓
terraform apply
        ↓
Issue?
        ↓
terraform state list
        ↓
terraform show
        ↓
TF_LOG=DEBUG terraform apply
        ↓
Fix & Re-run
```

This section fits very well at the end of your GitHub README and gives your repository a more professional DevOps/Cloud Engineer documentation style.
