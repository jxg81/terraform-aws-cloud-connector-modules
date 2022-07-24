# Zscaler Cloud Connector / AWS Gateway Load Balancer Endpoint and Endpoint Service Module

This module creates IAM Policies, Roles, and Instance Profile resources required for successful Cloud Connector deployments. As part of Zscaler provided deployment templates most resources have conditional create options leveraged "byo" variables should a customer want to leverage the module outputs with data reference to resources that may already exist in their AWS environment.

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.7, < 2.0.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 4.7.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 4.7.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_iam_policy_document.instance-assume-role-policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data |
| [aws_iam_policy_document.cc-callhome-policy-document](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data |
| [aws_iam_policy.cc-callhome-policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_policy) | resource |
| [aws_iam_role_policy_attachment.cc-callhome-policy-attachment](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.SecretsManagerReadWrite](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_role_policy_attachment) | resource |
| [aws_iam_role_policy_attachment.SSMManagedInstanceCore](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_role_policy_attachment) | resource |
| [aws_iam_role.cc-node-iam-role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_role) | resource |
| [aws_iam_instance_profile.cc-host-profile](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/aws_iam_instance_profile) | resource |
| [aws_iam_instance_profile.cc-host-profile-selected](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/aws_iam_instance_profile) | data |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="name_prefix"></a> [name\_prefix](#name\_prefix) | A prefix to associate to all the Cloud Connector module resources. | `string` | `null` | no |
| <a name="resource_tag"></a> [resource\_tag](#resource\_tag) | A tag to associate to all the Cloud Connector module resources. | `string` | `null` | no |
| <a name="global_tags"></a> [global\_tags](#global\_tags) | Populate any custom user defined tags from a map.<br>Example for defining tag Keys and Values:<pre>locals { <br>global_tags = {<br>  Owner = var.owner_tag <br>  ManagedBy = "terraform"<br>}</pre> | `map(string)` | `[]` | no |
| <a name="iam_role_policy_smrw"></a> [iam\_role\_policy\_smrw](#iam\_role\_policy\_smrw) | Cloud Connector EC2 Instance predefined IAM Role to access Secrets Manager resources. | `string` | `SecretsManagerReadWrite` | no |
| <a name="iam_role_policy_ssmcore"></a> [iam\_role\_policy\_ssmcore](#iam\_role\_policy\_ssmcore) | Cloud Connector EC2 Instance predefined IAM Role to access AWS SSM. | `string` | `AmazonSSMManagedInstanceCore` | no |
| <a name="iam_count"></a> [iam\_count](#iam\_count) | Default number IAM roles/policies/profiles to create. | `number` | `1` | no |
| <a name="cc_callhome_enabled"></a> [cc\_callhome\_enabled](#cc\_callhome\_enabled) | Determine whether or not to create the cc-callhome-policy IAM Policy and attach it to the CC IAM Role. | `bool` | `true` | no |
| <a name="byo_iam"></a> [byo\_iam](#byo\_iam) | Bring your own IAM Instance Profile for Cloud Connector. Setting this variable to true will effectively instruct this module to not create any resources and only reference data resources from values provided in byo_iam_instance_profile_id. | `bool` | `false` | no |
| <a name="byo_iam_instance_profile_id"></a> [byo\_iam\_instance\_profile\_id](#byo\_iam\_instance\_profile\_id) | Existing IAM Instance Profile IDs for Cloud Connector association. | `list(string)` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="iam_instance_profile_id"></a> [iam\_instance\_profile\_id](#iam\_instance\_profile\_id) | ID of the aws_iam_instance_profile data source |
| <a name="iam_instance_profile_arn"></a> [iam\_instance\_profile\_arn](#iam\_instance\_profile\_arn) | ARN of the aws_iam_instance_profile data source |