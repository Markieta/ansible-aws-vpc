# ansible-aws-vpc

Example implementation to create/destroy AWS VPCs and their components using Ansible.

## Prerequisites



### Package Dependencies



```bash
pip install boto boto3 --upgrade --user
```


RHEL 7... python 2.7.5 ... ansible 2.7.8


### AWS Setup



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



### Create VPC(s)



```bash
ansible-playbook -i inventories/<env>/hosts sandwich_launcher_vpcs.yml -e "activity=create"
```

### Destroy VPC(s)



```bash
ansible-playbook -i inventories/<env>/hosts sandwich_launcher_vpcs.yml -e "activity=destroy"
```


