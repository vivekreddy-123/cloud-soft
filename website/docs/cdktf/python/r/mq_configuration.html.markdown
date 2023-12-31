---
subcategory: "MQ"
layout: "aws"
page_title: "AWS: aws_mq_configuration"
description: |-
  Provides an MQ configuration Resource
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_mq_configuration

Provides an MQ Configuration Resource.

For more information on Amazon MQ, see [Amazon MQ documentation](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/welcome.html).

## Example Usage

```python
# Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.mq_configuration import MqConfiguration
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
        MqConfiguration(self, "example",
            data="<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n<broker xmlns=\"http://activemq.apache.org/schema/core\">\n  <plugins>\n    <forcePersistencyModeBrokerPlugin persistenceFlag=\"true\"/>\n    <statisticsBrokerPlugin/>\n    <timeStampingBrokerPlugin ttlCeiling=\"86400000\" zeroExpirationOverride=\"86400000\"/>\n  </plugins>\n</broker>\n\n",
            description="Example Configuration",
            engine_type="ActiveMQ",
            engine_version="5.15.0",
            name="example"
        )
```

## Argument Reference

The following arguments are required:

* `data` - (Required) Broker configuration in XML format. See [official docs](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/amazon-mq-broker-configuration-parameters.html) for supported parameters and format of the XML.
* `engine_type` - (Required) Type of broker engine. Valid values are `ActiveMQ` and `RabbitMQ`.
* `engine_version` - (Required) Version of the broker engine.
* `name` - (Required) Name of the configuration.

The following arguments are optional:

* `authentication_strategy` - (Optional) Authentication strategy associated with the configuration. Valid values are `simple` and `ldap`. `ldap` is not supported for `engine_type` `RabbitMQ`.
* `description` - (Optional) Description of the configuration.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block) present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the configuration.
* `id` - Unique ID that Amazon MQ generates for the configuration.
* `latest_revision` - Latest revision of the configuration.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider [`default_tags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block).

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import MQ Configurations using the configuration ID. For example:

```python
# Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import TerraformStack
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name):
        super().__init__(scope, name)
```

Using `terraform import`, import MQ Configurations using the configuration ID. For example:

```console
% terraform import aws_mq_configuration.example c-0187d1eb-88c8-475a-9b79-16ef5a10c94f
```

<!-- cache-key: cdktf-0.17.1 input-b759ec2d3a7c87e87eb4d3a72708fca5cbe69ea9d6e34ac95603e56968dfd088 -->