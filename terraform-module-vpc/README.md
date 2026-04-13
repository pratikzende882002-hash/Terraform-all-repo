# terraform-module-vpc

Terraform module to create an AWS VPC.

## Usage

```hcl
module "vpc" {
  source = "git::https://github.com/<your-org>/terraform-module-vpc.git?ref=v1.0.0"

  cidr_block = "10.0.0.0/16"
  vpc_name   = "myapp-dev-vpc"

  tags = {
    Environment = "dev"
    ManagedBy   = "Terraform"
  }
}
```

## Inputs

| Name        | Description             | Type          | Default | Required |
|-------------|-------------------------|---------------|---------|----------|
| cidr_block  | CIDR block for the VPC  | `string`      | —       | yes      |
| vpc_name    | Name tag for the VPC    | `string`      | —       | yes      |
| tags        | Map of tags to apply    | `map(string)` | `{}`    | no       |

## Outputs

| Name   | Description          |
|--------|----------------------|
| vpc_id | The ID of the VPC    |
