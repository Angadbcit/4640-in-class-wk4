# 4640-in-class-wk4

## Team

- Misha Makaroff
- Angad Bains

## Task 1

Create a key for cloud-init:
`ssh-keygen -t ed25519 -f /home/anges/w4/lab4key1`

Update the config file with the actual public key value and packages to the cloud file.

```bash
ssh-authorized-keys:
      - ssh-ed25519 *** anges@root

package_update: true
package_upgrade: true
packages:
  - nginx
  - nmap

runcmd:
  - systemctl enable nginx
  - systemctl start nginx
```

## Task 2

Enable DNS hostname of VPC, as by default it is off.

`enable_dns_hostnames = true`

Set a tag for project name for the resources as:
`project_name = local.project_name`

For the public subnet, set the availability zone and public ip on launch as:

`availability_zone = "us-west-2a"`
`map_public_ip_on_launch = true`

Set the vpc id for resources as:
`vpc_id = aws_vpc.web.id`

Set gateway id for resources as:
`gateway_id = aws_internet_gateway.web-gw.id`

Set subnet id for resources as:
`subnet_id = aws_subnet.web.id`

SSH key setup for the instance

```bash

```

We must allow http and ssh connecions to allow for our setup to work

```bash
  cidr_ipv4   = "10.0.0.0/8"
  from_port   = 80
  ip_protocol = "tcp"
  to_port     = 80

  cidr_ipv4   = "0.0.0.0/0"
  from_port   = 22
  ip_protocol = "tcp"
  to_port     = 22
```

Ec2 instance setup config:

```bash
ami = data.aws_ami.debian.id
instance_type = "t3.micro"
vpc_security_group_ids = [aws_security_group.web.id]
```

## Task 3

Create the terraform directory: `terraform init`
Check the config file: `terraform validate`
Dry run the config: `terraform plan`

## References

1. [cloud-init syntax](https://cloudinit.readthedocs.io/en/latest/reference/examples.html)
2. [Tag details](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc#tags-1)
3. [Avalability and Public IP](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet#availability_zone-1)
4. [VPC id format](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/internet_gateway)
5. [Routing table format](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route)
6. [Network rules](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc_security_group_ingress_rule)
