---
subcategory: "RDS (Relational Database)"
layout: "aws"
page_title: "AWS: aws_db_instances"
description: |-
  Terraform data source for listing RDS Database Instances.
---


<!-- Please do not edit this file, it is generated. -->
# Data Source: aws_db_instances

Terraform data source for listing RDS Database Instances.

## Example Usage

### Basic Usage

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { DataAwsDbInstances } from "./.gen/providers/aws/data-aws-db-instances";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new DataAwsDbInstances(this, "example", {
      filter: [
        {
          name: "db-instance-id",
          values: ["my-database-id"],
        },
      ],
    });
  }
}

```

## Argument Reference

The following arguments are optional:

* `filter` - (Optional) Configuration block(s) for filtering. Detailed below.

### filter Configuration block

The `filter` configuration block supports the following arguments:

* `name` - (Required) Name of the filter field. Valid values can be found in the [RDS DescribeDBClusters API Reference](https://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_DescribeDBClusters.html).
* `values` - (Required) Set of values that are accepted for the given filter field. Results will be selected if any given value matches.

## Attribute Reference

This data source exports the following attributes in addition to the arguments above:

* `instanceArns` - ARNs of the matched RDS instances.
* `instanceIdentifiers` - Identifiers of the matched RDS instances.

<!-- cache-key: cdktf-0.17.1 input-e80845c5e97757ead1a97783a9332fd4423a5a39e92d788d7a577b6a874e2e30 -->