---
subcategory: "RDS (Relational Database)"
layout: "aws"
page_title: "AWS: aws_db_option_group"
description: |-
  Provides an RDS DB option group resource.
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_db_option_group

Provides an RDS DB option group resource. Documentation of the available options for various RDS engines can be found at:

* [MariaDB Options](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.MariaDB.Options.html)
* [Microsoft SQL Server Options](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.html)
* [MySQL Options](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.MySQL.Options.html)
* [Oracle Options](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.Oracle.Options.html)

## Example Usage

```python
# Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Token, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.db_option_group import DbOptionGroup
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        DbOptionGroup(self, "example",
            engine_name="sqlserver-ee",
            major_engine_version="11.00",
            name="option-group-test-terraform",
            option=[DbOptionGroupOption(
                option_name="Timezone",
                option_settings=[DbOptionGroupOptionOptionSettings(
                    name="TIME_ZONE",
                    value="UTC"
                )
                ]
            ), DbOptionGroupOption(
                option_name="SQLSERVER_BACKUP_RESTORE",
                option_settings=[DbOptionGroupOptionOptionSettings(
                    name="IAM_ROLE_ARN",
                    value=Token.as_string(aws_iam_role_example.arn)
                )
                ]
            ), DbOptionGroupOption(
                option_name="TDE"
            )
            ],
            option_group_description="Terraform Option Group"
        )
```

~> **Note:** Any modifications to the `aws_db_option_group` are set to happen immediately as we default to applying immediately.

~> **WARNING:** You can perform a destroy on a `aws_db_option_group`, as long as it is not associated with any Amazon RDS resource. An option group can be associated with a DB instance, a manual DB snapshot, or an automated DB snapshot.

If you try to delete an option group that is associated with an Amazon RDS resource, an error similar to the following is returned:

> An error occurred (InvalidOptionGroupStateFault) when calling the DeleteOptionGroup operation: The option group 'optionGroupName' cannot be deleted because it is in use.

More information about this can be found [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithOptionGroups.html#USER_WorkingWithOptionGroups.Delete).

## Argument Reference

This resource supports the following arguments:

* `name` - (Optional, Forces new resource) The name of the option group. If omitted, Terraform will assign a random, unique name. Must be lowercase, to match as it is stored in AWS.
* `name_prefix` - (Optional, Forces new resource) Creates a unique name beginning with the specified prefix. Conflicts with `name`. Must be lowercase, to match as it is stored in AWS.
* `option_group_description` - (Optional) The description of the option group. Defaults to "Managed by Terraform".
* `engine_name` - (Required) Specifies the name of the engine that this option group should be associated with.
* `major_engine_version` - (Required) Specifies the major version of the engine that this option group should be associated with.
* `option` - (Optional) A list of Options to apply.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block) present, tags with matching keys will overwrite those defined at the provider-level.

Option blocks support the following:

* `option_name` - (Required) The Name of the Option (e.g., MEMCACHED).
* `option_settings` - (Optional) A list of option settings to apply.
* `port` - (Optional) The Port number when connecting to the Option (e.g., 11211).
* `version` - (Optional) The version of the option (e.g., 13.1.0.0).
* `db_security_group_memberships` - (Optional) A list of DB Security Groups for which the option is enabled.
* `vpc_security_group_memberships` - (Optional) A list of VPC Security Groups for which the option is enabled.

Option Settings blocks support the following:

* `name` - (Optional) The Name of the setting.
* `value` - (Optional) The Value of the setting.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The db option group name.
* `arn` - The ARN of the db option group.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block).

## Timeouts

[Configuration options](https://developer.hashicorp.com/terraform/language/resources/syntax#operation-timeouts):

- `delete` - (Default `15m`)

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import DB Option groups using the `name`. For example:

```python
# Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformStack
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
```

Using `terraform import`, import DB Option groups using the `name`. For example:

```console
% terraform import aws_db_option_group.example mysql-option-group
```

<!-- cache-key: cdktf-0.17.1 input-e2653f20f77c2a6f4979ce5eb3a9c3c9dc22aa167c5aac46782e52fe6e4b9e98 -->