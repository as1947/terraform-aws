# Terraform on AWS
# Install terraform on AWS Ubuntu 18.08 LTS 
```
sudo apt-get update -y
sudo apt-get install wget unzip -y
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform

terraform -v
Terraform v1.1.6
on linux_amd64
+ provider registry.terraform.io/hashicorp/aws v3.74.3

```
# Install aws cli 
```
sudo apt install awscli
check aws security crendials at https://jhooq.com/error-configuring-terraform-aws-provider/
aws configure

Example: 

aws configure
AWS Access Key ID [None]: AAABBBCCCDDDEEEFFFGG      <<<<< AWS -> MY Profile ->My Security Credemntials 
AWS Secret Access Key [None]: aaabbbcccdddeeefffggghhhiiijjjkkklllmmmn
Default region name [None]: us-east-1
Default output format [None]: text

The above info is stored in 
ls ~/.aws/
config  credentials
```
# Create terraform main.tf
```
mkdir terraform-folder
cd terraform-folder
mkdir aws;cd aws
terraform fmt main.tf
AWS_ACCESS_KEY_ID=AKIATZE5TRKD7HNPRI45 AWS_SECRET_ACCESS_KEY=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 terraform init
terraform validate
terraform plan
terraform apply
```

- terraform init command to initialize a working directory that contains a Terraform configuration. After initialization, you will be able to perform other commands, like terraform plan and terraform apply.

- If you try to run a command that relies on initialization without first initializing, the command will fail with an error and explain that you need to run init.

- Initialization performs several tasks to prepare a directory, including accessing state in the configured backend, downloading and installing provider plugins, and downloading modules. Under some conditions (usually when changing from one backend to another), it might ask the user for guidance or confirmation.

- A working directory must be initialized before Terraform can perform any operations in it (like provisioning infrastructure or modifying state).

- A Terraform working directory typically contains:

- A Terraform configuration describing resources Terraform should manage. This configuration is expected to change over time.
- A hidden .terraform directory, which Terraform uses to manage cached provider plugins and modules, record which workspace is currently active, and record the last known backend configuration in case it needs to migrate state on the next run. This directory is automatically managed by Terraform, and is created during initialization.
- State data, if the configuration uses the default local backend. This is managed by Terraform in a terraform.tfstate file (if the directory only uses the default workspace) or a terraform.tfstate.d directory
