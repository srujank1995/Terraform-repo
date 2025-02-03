# Terraform AWS VPC Setup

This repository contains Terraform configurations to create an AWS VPC named `demo-vpc` in the `us-east-1` region.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- [AWS CLI](https://aws.amazon.com/cli/)
- AWS IAM user with necessary permissions
- [Git](https://git-scm.com/downloads)

## Project Structure

```plaintext
terraform-vpc/
├── provider.tf       # Defines the AWS provider
├── variables.tf      # Contains all the variable definitions
├── main.tf           # Defines the VPC resource
├── README.md         # Project documentation
```

## Terraform Configuration

### **provider.tf** (AWS Provider Configuration)

```hcl
provider "aws" {
  region = var.aws_region
}
```

### **variables.tf** (Terraform Variables)

```hcl
variable "aws_region" {
  description = "The AWS region where resources will be created"
  type        = string
  default     = "us-east-1"
}

variable "vpc_cidr" {
  description = "The CIDR block for the VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "vpc_name" {
  description = "The name of the VPC"
  type        = string
  default     = "demo-vpc"
}
```

### **main.tf** (VPC Creation)

```hcl
resource "aws_vpc" "demo_vpc" {
  cidr_block = var.vpc_cidr

  tags = {
    Name = var.vpc_name
  }
}
```

## Setup and Deployment

### **Step 1: Clone the Repository**

```sh
git clone https://github.com/your-username/terraform-vpc.git
cd terraform-vpc
```

### **Step 2: Initialize Terraform**

```sh
terraform init
```

### **Step 3: Validate Terraform Configuration**

```sh
terraform validate
```

### **Step 4: Plan the Deployment**

```sh
terraform plan
```

### **Step 5: Apply the Configuration**

```sh
terraform apply -auto-approve
```

### **Step 6: Verify the VPC in AWS**

```sh
aws ec2 describe-vpcs --region us-east-1 --filters "Name=tag:Name,Values=demo-vpc"
```

### **Step 7: Destroy the Infrastructure (Optional)**

```sh
terraform destroy -auto-approve
```

## Best Practices

- Use **Terraform Workspaces** for different environments (dev/staging/prod).
- Store sensitive values in **Terraform Cloud/State Backend** instead of hardcoding.
- Use **IAM roles and policies** for secure access to AWS resources.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

Created by [Srujan Kinjawadekar](https://github.com/your-username). Feel free to reach out!

