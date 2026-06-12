# terraform_cicd

A production-ready **Terraform Infrastructure as Code (IaC) project** with automated CI/CD pipelines using GitHub Actions.

## 📋 Overview

This repository demonstrates a complete GitOps workflow for managing infrastructure with Terraform. It includes automated linting, planning, and deployment pipelines that ensure code quality and safe infrastructure changes.

## 🏗️ Project Structure

```
.
├── main.tf                          # Terraform configuration
├── README.md                        # This file
├── .github/workflows/               # GitHub Actions CI/CD pipelines
│   ├── lint.yaml                   # Linting and validation
│   ├── plan.yaml                   # Terraform plan for PRs
│   ├── apply.yaml                  # Apply changes to production
│   └── annotated.yml               # Basic validation workflow
└── .gitignore                       # Git exclusions
```

## 🔄 CI/CD Workflow

### 1. **Lint Workflow** (lint.yaml)
- **Trigger**: Pull Requests and pushes to main
- **Steps**:
  - Checks Terraform code formatting (`terraform fmt`)
  - Validates Terraform syntax (`terraform validate`)
  - Runs TFLint for best practices
- **Outcome**: Blocks PRs if code doesn't meet standards

### 2. **Plan Workflow** (plan.yaml)
- **Trigger**: Pull Requests to main
- **Steps**:
  - Generates Terraform execution plan
  - Posts plan as a PR comment for review
  - Blocks PR if plan fails
- **Purpose**: Shows what infrastructure changes will be applied

### 3. **Apply Workflow** (apply.yaml)
- **Trigger**: Pushes to main (after PR merge)
- **Steps**:
  - Initializes Terraform with remote state
  - Generates and saves execution plan
  - Applies approved changes (requires production environment approval)
  - Updates and commits state file back to repository
- **Purpose**: Deploys infrastructure changes automatically

## 📦 Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) >= 1.7.0
- [TFLint](https://github.com/terraform-linters/tflint)
- Git
- GitHub repository with Actions enabled

## 🚀 Getting Started

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Anjalii146/terraform.git
   cd terraform
   ```

2. **Initialize Terraform**:
   ```bash
   terraform init
   ```

3. **Format and validate**:
   ```bash
   terraform fmt -recursive
   terraform validate
   ```

4. **Create a feature branch**:
   ```bash
   git checkout -b feature/add-resources
   ```

5. **Add your infrastructure code** to `main.tf`

6. **Push and create a Pull Request**:
   ```bash
   git push origin feature/add-resources
   ```

7. **Review the plan** in the PR comment and merge when ready

## 🔐 Required Setup

### GitHub Secrets & Environments
- Configure the `production` environment in GitHub Settings for deployment approval
- Set up necessary cloud provider credentials as repository secrets

### Remote State
- Configure `terraform` backend to store state remotely (AWS S3, Azure Storage, Terraform Cloud, etc.)
- Update `terraform init` to use backend configuration

## 📝 Best Practices

- Always work on feature branches, never push directly to main
- Review the Terraform plan in PR comments before merging
- Keep infrastructure code DRY with variables and modules
- Use meaningful commit messages
- Lock Terraform version for consistency

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Push to origin
4. Create a Pull Request
5. Wait for CI/CD pipeline to pass
6. Merge when approved
7. Monitor the Apply workflow for successful deployment

## 📚 Additional Resources

- [Terraform Documentation](https://www.terraform.io/docs)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [TFLint Documentation](https://github.com/terraform-linters/tflint/blob/master/README.md)

## 📄 License

This project is open source and available under the MIT License.