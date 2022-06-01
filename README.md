# AWS MQTT Demo for Arm Virtual Hardware

This project demonstrates how to setup a development workflow with cloud-based Continuous Integration (CI) for testing an IoT application that connects to AWS cloud services.

Code development and debug can be done locally, for example with [CMSIS-Build](https://arm-software.github.io/CMSIS_5/develop/Build/html/index.html) and [Keil MDK](https://developer.arm.com/tools-and-software/embedded/keil-mdk) tools. We are also working on a development flow for [Keil Studio](https://keil.arm.com) that will provide a cloud-native development environment.

Automated build and test runs are executed on [Arm Virtual Hardware](https://www.arm.com/virtual-hardware)(AVH) in AWS and get managed with GitHub Actions. The test results can be then observed in repository's [Actions](https://github.com/ARM-software/AVH-GetStarted/actions).

For more details also check [**AWS MQTT Example description**](https://arm-software.github.io/AVH/main/examples/html/aws_mqtt.html) in Arm Virtual Hardware documentation.

## Setup of CI Test

To build and run this application with a CI workflow on GitHub the following steps are required. For details refer to [Run AMI with GitHub Actions](https://arm-software.github.io/AVH/main/infrastructure/html/run_ami_github.html).

1. **Amazon Web Service (AWS) account** with:
    - Amazon EC2 (elastic cloud) access
    - Amazon S3 (storage) access
    - Registration to access AVH Amazon Machine Image [AVH AMI](https://aws.amazon.com/marketplace/search/results?searchTerms=Arm+Virtual+Hardware)
    - User role setup for scripted API access

2. **GitHub**:
    - Fork this repository with at least _Write_ access rights
    - Store the AWS account configuration (obtained in step 1) as
    [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) - **AWS Access** values in the forked repository
    
3. **AWS IoT Thing**:
    - Use the [AWS IoT console](https://console.aws.amazon.com/iotv2/) to create a thing, download its certificates, create a policy, and attach the policy to the thing
    - Store this configuration as [GitHub Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) - **IoT Cloud Access** values in the forked repository

## GitHub Secrets - Values

The following (secret) configuration values need to be added to the repositories [Secret store](../../settings/secrets/actions):

Secret Name                    | Description
:------------------------------|:--------------------
**AWS Access**                 | **Settings and credentials to acces AWS services for running Arm Virtual Hardware**
`AWS_IAM_PROFILE`              | The [IAM Instance Profile](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html) associated with the AVH EC2 instance granting it access to required AWS resources.
`AWS_ACCESS_KEY_ID`<br>`AWS_SECRET_ACCESS_KEY`      | [Access key pair](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for the AWS account (as IAM user) that shall be used by the CI workflow for AWS access.
`AWS_S3_BUCKET_NAME`           | The name of the [S3 storage bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-buckets-s3.html) to be used for temporary data storage by Arm Virtual Hardware.
`AWS_DEFAULT_REGION`           | The data center region for running new AVH AMI. For example `eu-west-1`.
`AWS_SECURITY_GROUP_ID`        | The id of the [VPC security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) to add the EC2 instance to. Shall have format `sg-xxxxxxxx`.
`AWS_SUBNET_ID`                | The id of the [VPC subnet](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#view-subnet) to connect the EC2 instance to. Shall have format `subnet-xxxxxxxx`.
**IoT Cloud Access**           | <b>Settings and credentials required to connect an [AWS IoT Thing](https://github.com/MDK-Packs/Documentation/tree/master/AWS_Thing)</b>
`CLIENT_CERTIFICATE_PEM`       | Client (device) certificate
`CLIENT_PRIVATE_KEY_PEM`       | Client (device) private key
`IOT_THING_NAME`               | Client  (device) name
`MQTT_BROKER_ENDPOINT`         | MQTT broker host name
