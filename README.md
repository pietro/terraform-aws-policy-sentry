# terraform-aws-policy-sentry

Builds secure IAM Policies with resource constraints. For more information on Policy Sentry, see [the documentation](https://policy-sentry.readthedocs.io/en/latest/).

## Requirements

* You must have Policy Sentry 0.7.1 installed beforehand and it must be executable from your `$PATH`. Follow the installation instructions [here](https://policy-sentry.readthedocs.io/en/latest/user-guide/installation.html)

* You will have to run `terraform apply` **twice**. See the instructions for more details.

## Usage

### Example

Use the module as below:

* [main.tf](./examples/demo/main.tf):

```hcl
module "policy_sentry_demo" {
  source                              = "github.com/kmcquade/terraform-aws-policy-sentry"
  name                                = var.name
  read_access_level                   = var.read_access_level
  write_access_level                  = var.write_access_level
  list_access_level                   = var.list_access_level
  tagging_access_level                = var.tagging_access_level
  permissions_management_access_level = var.permissions_management_access_level
  wildcard_only_single_actions               = var.wildcard_only_actions
  minimize                            = var.minimize
}
```

Assuming you have your [variables.tf](./examples/demo/variables.tf) file set properly (redacted from this README for readability), provide the following in your `terraform.tfvars` file.

* [terraform.tfvars](./examples/demo/terraform.tfvars):

```hcl
name = "PolicySentryTest"

list_access_level = [
  "arn:aws:s3:::example-org",
]

read_access_level = [
  "arn:aws:kms:us-east-1:123456789012:key/shaq"
]

write_access_level = [
  "arn:aws:kms:us-east-1:123456789012:key/shaq"
]
```

### Demo

* Run `terraform apply` once to create the JSON policy file.

![](https://raw.githubusercontent.com/kmcquade/terraform-aws-policy-sentry/master/docs/asciinema/policy-sentry-terraform-1.gif)

* Run `terraform apply` **again** to create the IAM policy

![](https://raw.githubusercontent.com/kmcquade/terraform-aws-policy-sentry/master/docs/asciinema/policy-sentry-terraform-2.gif)

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Providers

No provider.

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:-----:|
| create\_policy | Set to true to create the actual IAM policies. Defaults to true. | `bool` | `true` | no |
| description | The description to include for the IAM policy. | `string` | `"Generated by Policy Sentry"` | no |
| list\_access\_level | Provide a list of Amazon Resource Names (ARNs) that your role needs LIST access to. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| minimize | If set to true, it will minimize the size of the IAM Policy file. Defaults to false. | `bool` | `false` | no |
| name | The name of the rendered policy file (no file extension). | `string` | n/a | yes |
| permissions\_management\_access\_level | Provide a list of Amazon Resource Names (ARNs) that your role needs PERMISSIONS MANAGEMENT access to. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| read\_access\_level | Provide a list of Amazon Resource Names (ARNs) that your role needs READ access to. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| region | The AWS region for these resources. Defaults to us-east-1 | `string` | `"us-east-1"` | no |
| tagging\_access\_level | Provide a list of Amazon Resource Names (ARNs) that your role needs TAGGING access to. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_list\_service | To generate a list of AWS service actions that (1) are at the LIST access level and (2) do not support resource constraints, list the service prefix here. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_permissions\_management\_service | To generate a list of AWS service actions that (1) are at the PERMISSIONS MANAGEMENT access level and (2) do not support resource constraints, list the service prefix here. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_read\_service | To generate a list of AWS service actions that (1) are at the READ access level and (2) do not support resource constraints, list the service prefix here. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_single\_actions | Individual actions that do not support resource constraints. For example, s3:ListAllMyBuckets | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_tagging\_service | To generate a list of AWS service actions that (1) are at the TAGGING access level and (2) do not support resource constraints, list the service prefix here. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| wildcard\_only\_write\_service | To generate a list of AWS service actions that (1) are at the WRITE access level and (2) do not support resource constraints, list the service prefix here. | `list` | <pre>[<br>  ""<br>]</pre> | no |
| write\_access\_level | Provide a list of Amazon Resource Names (ARNs) that your role needs WRITE access to. | `list` | <pre>[<br>  ""<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| iam\_policy\_arn | The ARN assigned by AWS to this policy. |
| iam\_policy\_document | The policy document. |
| iam\_policy\_id | The policy's ID. |
| iam\_policy\_name | The name of the policy. |
| iam\_policy\_path | The path of the policy in IAM |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Maintenance

* [Pre-commit hook](https://github.com/antonbabenko/pre-commit-terraform#4-run)

Run this every time before you push to Git.

```
pre-commit run -a
```


## Todo
* Update the documentation in the Policy Sentry docs.
* Publish this on Terraform module registry

## License

Copyright: &copy; 2020 Kinnaird McQuade