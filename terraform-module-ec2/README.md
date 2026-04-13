# terraform-module-ec2

Terraform module to create an AWS EC2 instance with an attached Security Group.

## Usage

```hcl
module "ec2" {
  source = "git::https://github.com/<your-org>/terraform-module-ec2.git?ref=v1.0.0"

  instance_name = "myapp-dev-web-server-1"
  ami_id        = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"
  subnet_id     = "subnet-0abc123"
  vpc_id        = "vpc-0abc123"
  vpc_cidr      = "10.0.0.0/16"
  environment   = "dev"

  tags = {
    Environment = "dev"
    ManagedBy   = "Terraform"
  }
}
```

## Inputs

| Name          | Description                        | Type          | Default        | Required |
|---------------|------------------------------------|---------------|----------------|----------|
| instance_name | Name tag for the EC2 instance      | `string`      | —              | yes      |
| ami_id        | AMI ID                             | `string`      | —              | yes      |
| instance_type | EC2 instance type                  | `string`      | `"t2.micro"`   | no       |
| subnet_id     | Subnet to launch the instance in   | `string`      | —              | yes      |
| vpc_id        | VPC ID for the security group      | `string`      | —              | yes      |
| vpc_cidr      | VPC CIDR (SSH restriction in prod) | `string`      | `"10.0.0.0/8"` | no       |
| environment   | Environment (dev / uat / prod)     | `string`      | —              | yes      |
| tags          | Map of tags to apply               | `map(string)` | `{}`           | no       |

## Outputs

| Name              | Description                      |
|-------------------|----------------------------------|
| instance_id       | EC2 instance ID                  |
| public_ip         | Public IP of the instance        |
| security_group_id | Security group ID                |
