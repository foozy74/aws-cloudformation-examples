# CloudFormation Examples

This repository contains CloudFormation example templates, each building on the previous stack:

- Create Basic Amazon EC2 Instance
- Enable SSH and HTTP/HTTPS Traffic
- Assign an IP Address and Output the Website URL
- Make the Template Dynamic
- Add RDS Postgresql Database
- Enable Inbound Traffic on Port 5432
- Add CodeDeploy agent, tags, and CodeDeployTrustRole
- Create CodePipeline
- Delete Your Stacks & Snapshots



## 1. Create Basic Amazon EC2 Instance

To create the stack using this template, run the `create-stack` command-line:

`$ aws cloudformation create-stack --stack-name ec2-rds-example --template-body file://01_ec2.yaml`

check all AIM Images
`aws ec2 describe-images --owners self amazon`

aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --region eu-central-1

check all AIM images per Regions
` https://docs.aws.amazon.com/de_de/ec2/latest/instancetypes/ec2-instance-regions.html#instance-types-eu-west-2`

Amazon EC2 AMI Locator
Ubunut
`https://cloud-images.ubuntu.com/locator/ec2/`

## 2. Enable SSH and HTTP/HTTPS Traffic

You can update your stack using the `update-stack` command:

`$ aws cloudformation update-stack --stack-name ec2-rds-example --template-body file://02_ec2.yaml`

## 3. Assign an IP Address and Output the Website URL

You can update your stack using the `update-stack` command:

`$ aws cloudformation update-stack --stack-name ec2-rds-example --template-body file://03_ec2.yaml`

## 4. Make the Template Dynamic

You can update the stack with this command, passing in the parameter values:

```bash
$ aws cloudformation update-stack --stack-name ec2-rds-example --template-body file://04_ec2.yaml \
--parameters ParameterKey=AvailabilityZone,ParameterValue=us-east-1a \
ParameterKey=EnvironmentType,ParameterValue=dev \
ParameterKey=KeyPairName,ParameterValue=jenna
```

## 5. Add RDS Postgresql Database

You can update the stack with this command, passing in the parameter values:

```bash
$ aws cloudformation update-stack --stack-name ec2-rds-example --template-body file://05_rds.yaml \
--parameters ParameterKey=AvailabilityZone,ParameterValue=us-east-1a \
ParameterKey=EnvironmentType,ParameterValue=dev \
ParameterKey=KeyPairName,ParameterValue=jenna \
ParameterKey=DBPassword,ParameterValue=Abcd1234
```

## 6. Enable Inbound Traffic on Port 5432

You can update the stack with this command, passing in the parameter values:

```bash
$ aws cloudformation update-stack --stack-name ec2-rds-example --template-body file://06_rds.yaml \
--parameters ParameterKey=AvailabilityZone,ParameterValue=us-east-1a \
ParameterKey=EnvironmentType,ParameterValue=dev \
ParameterKey=KeyPairName,ParameterValue=jenna \
ParameterKey=DBPassword,ParameterValue=Abcd1234
```

## 7. Delete Your Stacks & Snapshots

Don’t forget to delete your stack so you don’t accrue charges. You can do that with the `delete-stack` command:

`$ aws cloudformation delete-stack --stack-name ec2-rds-example`

If you left the `DeletionPolicy` and `UpdateReplacePolicy` properties set to snapshot and you no longer need those snapshots, then you can also delete those snapshots using the AWS Console so you don't accrue charges for those either.

Navigate to the RDS Management Console. From there, go to the Snapshots menu option. Select the snapshots created from your stack (hint: they will have a snapshot name that starts with your stack name) and select Delete snapshot from the Actions menu.
