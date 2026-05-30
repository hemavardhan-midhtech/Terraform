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
