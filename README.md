# 🚀 Server Provision using Ansible Playbook

 **Note:** All commands are for **CentOS** systems.

## 📌 1. Prerequisites

- Ansible (**version: 2.15**) and Python (**version: 3.9**) must be installed.
- AWS credentials must be configured on the local machine or exported as environment variables.
- `boto3` and `botocore` libraries must be installed (used by Ansible for AWS interactions).
- Ansible `amazon.aws` collection must be installed.
- A valid **AWS Key Pair** should exist in the target region.
- The specified **AMI ID** must exist in the given region.
- The user must have permissions to create **EC2 instances** and **security groups**.



## ⚙️ 2. Components Used

- `hosts`: Specifies where the playbook will run.
- `connection`: Defines how tasks are executed.
- `gather_facts`: Specifies whether system facts are collected.
- `ec2_group` module: Used to create/manage AWS security groups.
- `amazon.aws.ec2_instance` module: Used to launch EC2 instances.
- `debug`: Used to display the public IP of the created instance.



## 🛠️ 3. Configuration Details

- `hosts`: `local`
- `connection`: `local`
- `gather_facts`: `false`
- `keypair`: `new-key`
- `instance_type`: `t3.micro`
- `instance_name`: `ec2-instance`
- `region`: `ap-south-1`
- `image`: `ami-002f6e91abff6eb96`
- `security_group`: `my-jenkins-security-grp1`



## 🔁 4. Flow of Execution

-  Playbook execution begins on the **local machine** using `hosts: local` and `connection: local`.
-  No system facts are gathered (`gather_facts: false`).
-  A **Security Group** is configured.
-  A security group named `my-jenkins-security-grp1` is created with:
  - Inbound rules for **ports 22, 80, and 8080** (open to all).
  - An **egress rule** allowing all outbound traffic.
- The `amazon.aws.ec2_instance` module is invoked.
- An **EC2 instance** is launched with the defined parameters.
- Playbook execution command:
  
  ```bash
  ansible-playbook server_creation_aws.yml
