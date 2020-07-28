# terraform-aviatrix-aws-spoke

### Description
This module deploys a very simple spoke VPC, with a public and a private subnet in each availability zone. Transit gateways are created in the public subnets of the 2 first AZ's.

### Diagram
\<Provide a diagram of the high level constructs thet will be created by this module>
<img src="<IMG URL>"  height="250">

### Usage Example
```
module "spoke_aws_1" {
  source  = "terraform-aviatrix-modules/aws-spoke/aviatrix"
  version = "1.0.0"

  spoke_name = "my_first_spoke"
  cidr = "10.1.0.0/20"
  region = "eu-west-1"
  aws_account_name = "AWS"
  transit_gw = "tg-eu-west-1"
}
```

### Variables
The following variables are required:

key | value
:--- | :---
spoke_name | Name for this spoke VPC and it's gateways
region | AWS region to deploy this VPC in
cidr | What ip CIDR to use for this VPC
aws_account_name | The account name as known by the Aviatrix controller
transit_gw | The name of the transit gateway we want to attach this spoke to

The following variables are optional:

key | default | value 
:---|:---|:---
instance_size | t3.medium | The size of the Aviatrix spoke gateways
ha_gw | true | Set to false if you only want to deploy a single Aviatrix spoke gateway

### Outputs
This module will return the following outputs:

key | description
:---|:---
vpc | The created VPC as an object with all of it's attributes. This was created using the aviatrix_vpc resource.
spoke_gateway | The created Aviatrix spoke gateway as an object with all of it's attributes.