# ansible-aws-vpc

Example implementation to create/destroy AWS VPCs and their components using Ansible.

## Environment Details

The following instructions are tested and based on:

* RHEL 7
* Python 2.7.5
* Ansible 2.7.8

However, this code should work on other environments such as Fedora and/or Python3, and newer versions of Ansible.

## Prerequisites

The below prerequisites must be satisfied prior to using this Ansible code.

### Package Dependencies

Install the following Python packages required for the Ansible AWS modules:

```bash
pip install boto boto3 --upgrade --user
```

_Note: This can alternatively be done via your package manager if `boto3` is available and up to date._

### AWS Setup

A service account must be created with the appropriate permissions in order for Ansible to authenticate against your AWS environment.

Refer to [IAM Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) for full details.

#### Authorization

I attached the following policies to my user in order to execute all Ansible tasks:

* AmazonEC2FullAccess
* IAMFullAccess
* AmazonS3FullAccess
* CloudFrontFullAccess
* AmazonRoute53FullAccess
* AWSCertificateManagerFullAccess

_Note: These policies are quite liberal and should probably be more restrictive._

#### Authentication

Export your AWS access key and secret in the terminal session that will be running the Ansible playbook:

```bash
export AWS_ACCESS_KEY='<AWS_ACCESS_KEY>'
export AWS_SECRET_KEY='<AWS_SECRET_KEY>'
```

_Note: Exporting secrets as environment variables is not a good practice. Consider a secrets management solution (such as [HashiCorp Vault](https://www.vaultproject.io/)) for production._

## Usage

How to use this Ansible code.

### Create VPC(s)

Create all VPCs and their contained resources:

```bash
ansible-playbook -i inventories/<env>/hosts sandwich_launcher_vpcs.yml -e "activity=create"
```

_Note: This may take several minutes to complete._

### Destroy VPC(s)

Destroy all VPCs and their contained resources:

```bash
ansible-playbook -i inventories/<env>/hosts sandwich_launcher_vpcs.yml -e "activity=destroy"
```

_Note: This will **immediately delete** all VPCs defined in the selected inventory. You will not be prompted to validate._
