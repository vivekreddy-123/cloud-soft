---
subcategory: "VPC (Virtual Private Cloud)"
layout: "aws"
page_title: "AWS: aws_route_table"
description: |-
  Provides a resource to create a VPC routing table.
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_route_table

Provides a resource to create a VPC routing table.

~> **NOTE on Route Tables and Routes:** Terraform currently
provides both a standalone [Route resource](route.html) and a Route Table resource with routes
defined in-line. At this time you cannot use a Route Table with in-line routes
in conjunction with any Route resources. Doing so will cause
a conflict of rule settings and will overwrite rules.

~> **NOTE on `gatewayId` and `natGatewayId`:** The AWS API is very forgiving with these two
attributes and the `awsRouteTable` resource can be created with a NAT ID specified as a Gateway ID attribute.
This _will_ lead to a permanent diff between your configuration and statefile, as the API returns the correct
parameters in the returned route table. If you're experiencing constant diffs in your `awsRouteTable` resources,
the first thing to check is whether or not you're specifying a NAT ID instead of a Gateway ID, or vice-versa.

~> **NOTE on `propagatingVgws` and the `awsVpnGatewayRoutePropagation` resource:**
If the `propagatingVgws` argument is present, it's not supported to _also_
define route propagations using `awsVpnGatewayRoutePropagation`, since
this resource will delete any propagating gateways not explicitly listed in
`propagatingVgws`. Omit this argument when defining route propagation using
the separate resource.

## Example Usage

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { RouteTable } from "./.gen/providers/aws/route-table";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new RouteTable(this, "example", {
      route: [
        {
          cidrBlock: "10.0.1.0/24",
          gatewayId: Token.asString(awsInternetGatewayExample.id),
        },
        {
          egressOnlyGatewayId: Token.asString(
            awsEgressOnlyInternetGatewayExample.id
          ),
          ipv6CidrBlock: "::/0",
        },
      ],
      tags: {
        Name: "example",
      },
      vpcId: Token.asString(awsVpcExample.id),
    });
  }
}

```

To subsequently remove all managed routes:

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { RouteTable } from "./.gen/providers/aws/route-table";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new RouteTable(this, "example", {
      route: [],
      tags: {
        Name: "example",
      },
      vpcId: Token.asString(awsVpcExample.id),
    });
  }
}

```

## Argument Reference

This resource supports the following arguments:

* `vpcId` - (Required) The VPC ID.
* `route` - (Optional) A list of route objects. Their keys are documented below. This argument is processed in [attribute-as-blocks mode](https://www.terraform.io/docs/configuration/attr-as-blocks.html).
This means that omitting this argument is interpreted as ignoring any existing routes. To remove all managed routes an empty list should be specified. See the example above.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider [`defaultTags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block) present, tags with matching keys will overwrite those defined at the provider-level.
* `propagatingVgws` - (Optional) A list of virtual gateways for propagation.

### route Argument Reference

This argument is processed in [attribute-as-blocks mode](https://www.terraform.io/docs/configuration/attr-as-blocks.html).

One of the following destination arguments must be supplied:

* `cidrBlock` - (Required) The CIDR block of the route.
* `ipv6CidrBlock` - (Optional) The Ipv6 CIDR block of the route.
* `destinationPrefixListId` - (Optional) The ID of a [managed prefix list](ec2_managed_prefix_list.html) destination of the route.

One of the following target arguments must be supplied:

* `carrierGatewayId` - (Optional) Identifier of a carrier gateway. This attribute can only be used when the VPC contains a subnet which is associated with a Wavelength Zone.
* `coreNetworkArn` - (Optional) The Amazon Resource Name (ARN) of a core network.
* `egressOnlyGatewayId` - (Optional) Identifier of a VPC Egress Only Internet Gateway.
* `gatewayId` - (Optional) Identifier of a VPC internet gateway or a virtual private gateway.
* `localGatewayId` - (Optional) Identifier of a Outpost local gateway.
* `natGatewayId` - (Optional) Identifier of a VPC NAT gateway.
* `networkInterfaceId` - (Optional) Identifier of an EC2 network interface.
* `transitGatewayId` - (Optional) Identifier of an EC2 Transit Gateway.
* `vpcEndpointId` - (Optional) Identifier of a VPC Endpoint.
* `vpcPeeringConnectionId` - (Optional) Identifier of a VPC peering connection.

Note that the default route, mapping the VPC's CIDR block to "local", is created implicitly and cannot be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

~> **NOTE:** Only the target that is entered is exported as a readable
attribute once the route resource is created.

* `id` - The ID of the routing table.
* `arn` - The ARN of the route table.
* `ownerId` - The ID of the AWS account that owns the route table.
* `tagsAll` - A map of tags assigned to the resource, including those inherited from the provider [`defaultTags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block).

## Timeouts

[Configuration options](https://developer.hashicorp.com/terraform/language/resources/syntax#operation-timeouts):

- `create` - (Default `5M`)
- `update` - (Default `2M`)
- `delete` - (Default `5M`)

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import Route Tables using the route table `id`. For example:

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
  }
}

```

Using `terraform import`, import Route Tables using the route table `id`. For example:

```console
% terraform import aws_route_table.public_rt rtb-4e616f6d69
```

<!-- cache-key: cdktf-0.17.1 input-8beca07e44d44bd6606ef4280e3b37d9bdb6fbc0002ac73d2bbb103e495b6ce4 -->