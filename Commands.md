# Terraform Commands Cheat Sheet

## 1. Initialize Terraform

```bash
terraform init
```

* Initializes Terraform working directory
* Downloads required providers and modules

---

## 2. Format Terraform Code

```bash
terraform fmt
```

* Formats `.tf` files according to Terraform standards

Format all files recursively:

```bash
terraform fmt -recursive
```

---

## 3. Validate Configuration

```bash
terraform validate
```

* Checks syntax and configuration validity

---

## 4. Preview Infrastructure Changes

```bash
terraform plan
```

* Shows what will be created, modified, or destroyed

Save plan:

```bash
terraform plan -out=tfplan
```

Use variable file:

```bash
terraform plan -var-file=dev.tfvars
```

---

## 5. Apply Changes

```bash
terraform apply
```

Apply saved plan:

```bash
terraform apply tfplan
```

Auto approve:

```bash
terraform apply -auto-approve
```

---

## 6. Destroy Infrastructure

```bash
terraform destroy
```

Auto approve:

```bash
terraform destroy -auto-approve
```

Destroy specific resource:

```bash
terraform destroy -target=aws_instance.web
```

---

## 7. View Terraform State

Show current state:

```bash
terraform show
```

List resources:

```bash
terraform state list
```

View resource details:

```bash
terraform state show aws_instance.web
```

---

## 8. Output Values

Display all outputs:

```bash
terraform output
```

Display specific output:

```bash
terraform output instance_ip
```

---

## 9. Import Existing Resources

```bash
terraform import aws_instance.web i-0123456789abcdef0
```

Examples:

```bash
terraform import aws_s3_bucket.bucket my-bucket
terraform import aws_security_group.sg sg-12345678
```

---

## 10. Terraform Workspaces

Create workspace:

```bash
terraform workspace new dev
```

List workspaces:

```bash
terraform workspace list
```

Switch workspace:

```bash
terraform workspace select dev
```

Show current workspace:

```bash
terraform workspace show
```

Delete workspace:

```bash
terraform workspace delete dev
```

---

## 11. Provider Commands

Show providers:

```bash
terraform providers
```

Upgrade providers:

```bash
terraform init -upgrade
```

---

## 12. Terraform Version

```bash
terraform version
```

---

## 13. Refresh State

```bash
terraform refresh
```

Alternative:

```bash
terraform apply -refresh-only
```

---

## 14. State Management

Move resource:

```bash
terraform state mv SOURCE DESTINATION
```

Example:

```bash
terraform state mv aws_instance.web aws_instance.app
```

Remove resource from state:

```bash
terraform state rm aws_instance.web
```

Pull state:

```bash
terraform state pull
```

Push state:

```bash
terraform state push terraform.tfstate
```

---

## 15. Lock Management

Unlock state:

```bash
terraform force-unlock LOCK_ID
```

---

## 16. Terraform Console

```bash
terraform console
```

Examples:

```bash
> length(["a","b","c"])
3

> upper("terraform")
"TERRAFORM"
```

---

## 17. Dependency Graph

```bash
terraform graph
```

Generate graph image:

```bash
terraform graph | dot -Tpng > graph.png
```
---

## 18. Taint / Untaint Resources

Mark for recreation:

```bash
terraform taint aws_instance.web
```

Remove taint:

```bash
terraform untaint aws_instance.web
```

---

## 19. Target Specific Resource

Plan specific resource:

```bash
terraform plan -target=aws_instance.web
```

Apply specific resource:

```bash
terraform apply -target=aws_instance.web
```

---

## 20. Variables

Pass variable:

```bash
terraform apply -var="instance_type=t3.micro"
```

Use variable file:

```bash
terraform apply -var-file=dev.tfvars
```

---

# Typical Terraform Workflow

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

---

# Production Workflow

```bash
terraform init
terraform fmt -recursive
terraform validate
terraform plan -out=tfplan
terraform apply tfplan
terraform output
```

---

# Interview-Must-Know Commands

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform import
terraform output
terraform state list
terraform state show
terraform state rm
terraform workspace new
terraform workspace select
terraform providers
terraform console
terraform graph
terraform force-unlock
```

---

# Terraform Files Reference

| File             | Purpose                                |
| ---------------- | -------------------------------------- |
| main.tf          | Main infrastructure code               |
| variables.tf     | Variable declarations                  |
| terraform.tfvars | Variable values                        |
| outputs.tf       | Output values                          |
| provider.tf      | Provider configuration                 |
| versions.tf      | Terraform/provider version constraints |
| backend.tf       | Remote state configuration             |

---

# Quick Debugging Commands

```bash
terraform validate
terraform fmt
terraform plan
terraform state list
terraform state show RESOURCE_NAME
terraform output
terraform providers
terraform version
```

Save this as **`Terraform-CheatSheet.md`** in your Git repository for quick reference during interviews and project work.

# Terraform Commands Cheat Sheet

A complete Terraform command reference for DevOps Engineers, Cloud Engineers, Site Reliability Engineers (SREs), and Infrastructure Engineers.

---

## 📌 Table of Contents

* [Terraform Workflow](#terraform-workflow)
* [Initialization](#initialization)
* [Formatting](#formatting)
* [Validation](#validation)
* [Planning](#planning)
* [Applying Changes](#applying-changes)
* [Destroying Infrastructure](#destroying-infrastructure)
* [Terraform State](#terraform-state)
* [Outputs](#outputs)
* [Import Existing Resources](#import-existing-resources)
* [Workspaces](#workspaces)
* [Providers](#providers)
* [Variables](#variables)
* [State Management](#state-management)
* [Lock Management](#lock-management)
* [Terraform Console](#terraform-console)
* [Dependency Graph](#dependency-graph)
* [Taint and Untaint](#taint-and-untaint)
* [Target Resources](#target-resources)
* [Terraform Files Reference](#terraform-files-reference)
* [Interview Commands](#interview-commands)

---

# Terraform Workflow

Typical Terraform lifecycle:

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
```

Production workflow:

```bash
terraform init
terraform fmt -recursive
terraform validate
terraform plan -out=tfplan
terraform apply tfplan
terraform output
```

---

# Initialization

Initialize Terraform project:

```bash
terraform init
```

Upgrade providers:

```bash
terraform init -upgrade
```

---

# Formatting

Format Terraform files:

```bash
terraform fmt
```

Format recursively:

```bash
terraform fmt -recursive
```

---

# Validation

Validate Terraform configuration:

```bash
terraform validate
```

---

# Planning

Preview infrastructure changes:

```bash
terraform plan
```

Save execution plan:

```bash
terraform plan -out=tfplan
```

Use variables file:

```bash
terraform plan -var-file=dev.tfvars
```

Target a specific resource:

```bash
terraform plan -target=aws_instance.web
```

---

# Applying Changes

Apply infrastructure changes:

```bash
terraform apply
```

Apply saved plan:

```bash
terraform apply tfplan
```

Auto approve:

```bash
terraform apply -auto-approve
```

Apply using variables file:

```bash
terraform apply -var-file=dev.tfvars
```

Pass variable directly:

```bash
terraform apply -var="instance_type=t3.micro"
```

---

# Destroying Infrastructure

Destroy all resources:

```bash
terraform destroy
```

Auto approve destroy:

```bash
terraform destroy -auto-approve
```

Destroy a specific resource:

```bash
terraform destroy -target=aws_instance.web
```

---

# Terraform State

Show current state:

```bash
terraform show
```

List resources:

```bash
terraform state list
```

Show resource details:

```bash
terraform state show aws_instance.web
```

Refresh state:

```bash
terraform refresh
```

Recommended refresh method:

```bash
terraform apply -refresh-only
```

---

# Outputs

Display all outputs:

```bash
terraform output
```

Display specific output:

```bash
terraform output instance_ip
```

---

# Import Existing Resources

Import existing EC2 instance:

```bash
terraform import aws_instance.web i-0123456789abcdef0
```

Import S3 bucket:

```bash
terraform import aws_s3_bucket.bucket my-bucket
```

Import Security Group:

```bash
terraform import aws_security_group.sg sg-12345678
```

---

# Workspaces

Create workspace:

```bash
terraform workspace new dev
```

List workspaces:

```bash
terraform workspace list
```

Select workspace:

```bash
terraform workspace select dev
```

Show current workspace:

```bash
terraform workspace show
```

Delete workspace:

```bash
terraform workspace delete dev
```

---

# Providers

View providers:

```bash
terraform providers
```

Check Terraform version:

```bash
terraform version
```

---

# Variables

Pass variable:

```bash
terraform apply -var="region=us-east-1"
```

Use variable file:

```bash
terraform apply -var-file=prod.tfvars
```

---

# State Management

Move state resource:

```bash
terraform state mv SOURCE DESTINATION
```

Example:

```bash
terraform state mv aws_instance.web aws_instance.app
```

Remove resource from state:

```bash
terraform state rm aws_instance.web
```

Pull remote state:

```bash
terraform state pull
```

Push state:

```bash
terraform state push terraform.tfstate
```

---

# Lock Management

Unlock Terraform state:

```bash
terraform force-unlock LOCK_ID
```

---

# Terraform Console

Open Terraform console:

```bash
terraform console
```

Examples:

```bash
length(["a","b","c"])
```

Output:

```text
3
```

```bash
upper("terraform")
```

Output:

```text
TERRAFORM
```

---

# Dependency Graph

Generate dependency graph:

```bash
terraform graph
```

Generate PNG image:

```bash
terraform graph | dot -Tpng > graph.png
```

---

# Taint and Untaint

Mark resource for recreation:

```bash
terraform taint aws_instance.web
```

Remove taint:

```bash
terraform untaint aws_instance.web
```

---

# Target Resources

Plan specific resource:

```bash
terraform plan -target=aws_instance.web
```

Apply specific resource:

```bash
terraform apply -target=aws_instance.web
```

Destroy specific resource:

```bash
terraform destroy -target=aws_instance.web
```

---

# Terraform Files Reference

| File             | Purpose                            |
| ---------------- | ---------------------------------- |
| main.tf          | Main infrastructure definition     |
| variables.tf     | Input variable declarations        |
| terraform.tfvars | Variable values                    |
| outputs.tf       | Output definitions                 |
| provider.tf      | Provider configuration             |
| versions.tf      | Version constraints                |
| backend.tf       | Remote state backend configuration |

---

# Frequently Used Interview Commands

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform import
terraform output
terraform state list
terraform state show
terraform state rm
terraform workspace new
terraform workspace select
terraform providers
terraform console
terraform graph
terraform force-unlock
```

---

# Common Troubleshooting Commands

Check configuration:

```bash
terraform validate
```

Check formatting:

```bash
terraform fmt
```

Preview changes:

```bash
terraform plan
```

View resources:

```bash
terraform state list
```

Inspect resource:

```bash
terraform state show RESOURCE_NAME
```

Display outputs:

```bash
terraform output
```

Check providers:

```bash
terraform providers
```

Check version:

```bash
terraform version
```

---

# Best Practices

* Always run `terraform fmt` before committing code.
* Run `terraform validate` before creating plans.
* Use remote state storage (S3, Azure Storage, GCS).
* Enable state locking for team environments.
* Use workspaces for environment separation.
* Store secrets in secret managers, not in Terraform code.
* Review `terraform plan` output before every apply.
* Use modules to reduce code duplication.
* Commit `.tf` files but never commit state files containing sensitive information.

---

## License

This repository is intended for learning, interview preparation, and daily Terraform administration.

⭐ If this cheat sheet helped you, consider starring the repository.
