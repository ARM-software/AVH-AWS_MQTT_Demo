# VHT_AWS_MQTT_Demo
AWS MQTT Demo for Arm Virtual Hardware

## Secret values 

The following (secret) configuration values need to be added to the repositories 
[Secret store](../../settings/secrets/actions):

Secret Name                    | Description
:------------------------------|:--------------------
**AWS Access**                 | Settings and credentials required to acces AWS EC2 and S3 services
`AWS_IAM_PROFILE`              | The [IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use.html) to be used for AWS access. The value shall be preceded with `Name=` prior to the actual profile name. For example `Name=myAVHRole`.
`AWS_ACCESS_KEY_ID`<br>`AWS_SECRET_ACCESS_KEY`      | [Access key pair](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) for the AWS account (as IAM user) that shall be used by the CI workflow for AWS access.
`AWS_S3_BUCKET`                | The name of the S3 storage bucket to be used for data exchange between GitHub and AWS AMI.
`AWS_DEFAULT_REGION`           | The data center region the AVH AMI will be run on. For example `eu-west-1`.
`AWS_SECURITY_GROUP_ID`        | The id of the [VPC security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) to add the EC2 instance to. Shall have format `sg-xxxxxxxx`.
`AWS_SUBNET_ID`                | The id of the [VPC subnet](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#view-subnet) to connect the EC2 instance to. Shall have format `subnet-xxxxxxxx`.
**IoT Cloud Access**           | Settings and credentials required to connect an [AWS IoT Thing](https://github.com/MDK-Packs/Documentation/tree/master/AWS_Thing)
`CLIENT_CERTIFICATE_PEM`       | Client (device) certificate
`CLIENT_PRIVATE_KEY_PEM`       | Client (device) private key
`IOT_THING_NAME`               | Client  (device) name
`MQTT_BROKER_ENDPOINT`         | MQTT broker host name
