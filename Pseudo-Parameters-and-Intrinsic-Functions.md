### Pseudo Parameters and Intrinsic Functions

**Pseudo parameters**: Aliases for common AWS specific configuration data
* Critical for composing AWS account and regionally agnostic templates

**Intrinsic functions**: Helpers that resolve different bits of data within a template
* Importing values from other CloudFormation stacks or applying simple string substitutions

Both pseudo parameters and intrinsic functions can be used together to dynamically resolve complex configs.

### Intrinsic Functions
* AWS CloudFormation provides several build-in functions that help you manage your stacks. Use intrinsic functions in your templates to assign values to properties that are not available until runtime.

### Fn::Base64
* The intrinsic function `Fn::Base64` returns the Base64 representation of the input string. This function is typically used to pass encoded data to Amazon EC2 instances by way of the `UserData` property.
* Base64 is a way to represent binary data as a string of ASCII characters. It is often used to transmit binary data over protocols that are designed to handle only ASCII characters, such as email or HTTP.

```yaml
Fn::Base64: valueToEncode

!Base64 valueToEncode
```

If you use the short form and immediately include another function in the valueToEncode parameter, use the full function name for at least one of the functions. For example, the following syntax isn't valid:

```yaml
!Base64 !Sub string
!Base64 !Ref logical_ID
```

Instead, use the full function name for at least one of the functions, as shown in the following examples:

```yaml
!Base64
  "Fn::Sub": string

Fn::Base64:
  !Sub string
```

For example, you may use `Fn::Base64` to encode a shell script that is passed to an EC2 instance as user data.

```yaml
UserData:
  !Base64 |
    #!/bin/bash
    echo "Hello, World!"
```

In this example, the !Base64 function encodes the Bash script as a Base64-encoded string. This string can be passed to an EC2 instance as user data to run the script on the instance.

### Fn::Cidr
* The intrinsic function `Fn::Cidr` returns an array of CIDR address blocks. The number of CIDR blocks returned is dependent on the `count` parameter.

```yaml
Fn::Cidr:
  - ipBlock
  - count
  - cidrBits
  
!Cidr [ipBlock, count, cidrBits]
```

**Parameters**  

- **ipBlock**: The user-specified CIDR address block to be split into smaller address blocks.
- **count**: The number of CIDRs to generate. Valid range is between 1 and 256.
- **cidrBits**: The number of subnet bits for the CIDR. For eaxmple, specifying a value of "8" for this parameter will create a CIDR with a mask of "/24".

The `Fn::Cidr` function takes three parameters: the base IP address, the number of subnets to generate, and the size of each subnet. It generates a list of CIDR blocks that covers the specified IP address range.

* Subnet bits is the inverse of subnet mask. To calculate the required host bits for a given subnet bits, subtract the subnet bits from 32 for IPv4 or 128 for IPv6.

**Return Value**  

An array of CIDR address blocks

**Example**  

This example creates 6 CIDRs with a subnet mask "/27" inside from a CIDR with a mask of "/24".

```yaml
!Cidr [ "192.168.0.0/24", 6, 5 ]
```

In this example, the `!Cidr` function generates a list of two CIDR blocks that cover the IP address range 10.0.0.0/16. The second parameter, 2, specifies that two subnets should be generated, and the third parameter, 8, specifies that each subnet should have a size of 256 IP addresses (2^8).
```yaml
Subnets:
  !Cidr [ "10.0.0.0/16", 2, 8 ]
```

The resulting list of CIDR blocks might look like this:
```yaml
[  "10.0.0.0/24",  "10.0.1.0/24"]
```
This list of CIDR blocks could be used to create two subnets in a VPC, each with 256 IP addresses.

**Creating an IPv6 enabled VPC**  

This example template creates an IPv6 enabled subnet.

```yaml
Resources:
    ExampleVpc:
        Type: AWS::EC2::VPC
        Properties:
            CidrBlock: "10.0.0.0/16"
     IPv6CidrBlock:
        Type: AWS::EC2::VPCCidrBlock
        Properties:
            AmazonProvidedIpv6CidrBlock: true
            VpcId: !Ref ExampleVpc
     ExampleSubnet:
        Type: AWS::EC2::Subnet
        DependsOn: IPv6CidrBlock
        Properties:
            AssignIpv6AddressOnCreation: true
            CidrBlock: !Select [ 0, !Cidr [ !GetAtt ExampleVpc.CidrBlock, 1, 8 ]]
            Ipv6CidrBlock: !Select [ 0, !Cidr [ !Select [ 0, !GetAtt ExampleVpc.Ipv6CidrBlocks], 1, 64 ]]
            VpcId: !Ref ExampleVpc
```

A CIDR block is a way of specifying a range of IP addresses. It consists of an IP address and a network mask that specifies the number of bits in the address that are used to identify the network. CIDR notation is often used to specify the IP address ranges used by subnets in a VPC.

### Fn::FindInMap
The intrinsic function `Fn::FindInMap` returns the value corresponding to keys in a two-level map that is declared in the `Mappings` section.

```yaml
Fn::FindInMap: [ MapName, TopLevelKey, SecondLevelKey ]

!FindInMap [ MapName, TopLevelKey, SecondLevelKey ]
```

You cannot nest two instances of two functions in short form.

**Parameters**  

- **MapName**: The logical name of a mapping declared in the Mappings section that contains the keys and values.
- **TopLevelKey**: The top-level key name. Its value is a list of key-value pairs.
- **SecondLevelKey**: The second-level key name, which is set to one of the keys from the list assigned to `TopLevelKey`.

**Return Value**  
The value that is assigned to `SecondLevelKey`.

### Example
The following example shows how to use `Fn::FindInMap` for a template with a `Mappings` section that contains a single map, `RegionMap`, that associates AMIs with AWS Regions.

* The map has 5 top-level keys that correspond to various AWS Regions.
* Each top-level key is assigned a list with two second level keys, `"HVM64"` and `"HVMG2"`, that correspond to the AMI's architecture.
* Each of the second-level keys is assigned an appropriate AMI name.

The example template contains an `AWS::EC2::Instance` resource whose `ImageId` property is set by the `FindInMap` function.

`MapName` is set to the map of interest, `"RegionMap"` in this example. `TopLevelKey` is set to the region where the stack is created, which is determined by using the `"AWS::Region"` pseudo parameter. `SecondLevelKey` is set to the desired architecture, `"HVM64"` for this example.

`FindInMap` returns the AMI assigned to `FindInMap`. For a `HVM64` instance in `us-east-1`, FindInMap would return `"ami-0ff8a91507f77f867"`.

```yaml
Mappings: 
  RegionMap: 
    us-east-1: 
      HVM64: "ami-0ff8a91507f77f867"
      HVMG2: "ami-0a584ac55a7631c0c"
    us-west-1: 
      HVM64: "ami-0bdb828fd58c52235"
      HVMG2: "ami-066ee5fd4a9ef77f1"
    eu-west-1: 
      HVM64: "ami-047bb4163c506cd98"
      HVMG2: "ami-31c2f645"
    ap-southeast-1: 
      HVM64: "ami-08569b978cc4dfa10"
      HVMG2: "ami-0be9df32ae9f92309"
    ap-northeast-1: 
      HVM64: "ami-06cd52961ce9f0d85"
      HVMG2: "ami-053cdd503598e4a9d"
Resources: 
  myEC2Instance: 
    Type: "AWS::EC2::Instance"
    Properties: 
      ImageId: !FindInMap
        - RegionMap
        - !Ref 'AWS::Region'
        - HVM64
      InstanceType: m1.small
```

### Fn::GetAtt
The `Fn::GetAtt` intrinsic function returns the value of an attribute from a resource in the template. 
* This function allows you to retrieve specific pieces of information about a resource in your CloudFormation stack, such as its IP address, domain name, or other properties

```yaml
Fn::GetAtt: [ logicalNameOfResource, attributeName ]

!GetAtt logicalNameOfResource.attributeName
```

**Parameters**  
- **logicalNameOfResource**: The logical name (also called logical ID) of the resource that contains the attribute that you want.
- **attributeName**: The name of the resource-specific attribute whose value you want. 

**Return Value**  
The attribute value.

### Example

This example snippet returns a string containing the DNS name of the load balancer with the logical name `myELB`.

```yaml
!GetAtt myELB.DNSName
```

The following example template returns the `SourceSecurityGroup.OwnerAlias` and `SourceSecurityGroup.GroupName` of the load balancer with the logical name `myELB`.

```yaml
AWSTemplateFormatVersion: 2010-09-09
Resources:
  myELB:
    Type: AWS::ElasticLoadBalancing::LoadBalancer
    Properties:
      AvailabilityZones:
        - eu-west-1a
      Listeners:
        - LoadBalancerPort: '80'
          InstancePort: '80'
          Protocol: HTTP
  myELBIngressGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: ELB ingress group
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          SourceSecurityGroupOwnerId: !GetAtt myELB.SourceSecurityGroup.OwnerAlias
          SourceSecurityGroupName: !GetAtt myELB.SourceSecurityGroup.GroupName         
```

### Fn::GetAZs
The intrinsic function `Fn::GetAZs` returns an array that lists Availability Zones for a specified region in alphabetical order. Because customers have access to different Availability Zones, the intrinsic function `Fn::GetAZs` enables template authors to write templates that adapt to the calling user's access. That way you don't have to hard-code a full list of Availability Zones for a specified region.

```yaml
Fn::GetAZs: region

!GetAZs region
```

**Parameters**  
- **region**: The name of the region for which you want to get the Availability Zones.

You can use the `AWS::Region` pseudo parameter to specify the region in which the stack is created. Specifying an empty string is equivalent to specifying AWS::Region.

**Return Value**  
The list of Availability Zones for the region.

### Examples
For these examples, CloudFormation evaluates `Fn::GetAZs` to the following array—assuming that the user has created the stack in the `us-east-1` region:

`[ "us-east-1a", "us-east-1b", "us-east-1c", "us-east-1d" ]`

```yaml
Fn::GetAZs: ""
Fn::GetAZs:
  Ref: "AWS::Region"
Fn::GetAZs: us-east-1
```

The following example uses `Fn::GetAZs` to specify a subnet's Availability Zone:

```yaml
mySubnet: 
  Type: "AWS::EC2::Subnet"
  Properties: 
    VpcId: 
      !Ref VPC
    CidrBlock: 10.0.0.0/24
    AvailabilityZone: 
      Fn::Select: 
        - 0
        - Fn::GetAZs: ""
```

**Nested Functions with Short Form YAML**  

The following examples show valid patterns for using nested intrinsic functions using short form YAML. You cannot nest short form functions consecutively, so a pattern like !GetAZs !Ref is not valid.

```yaml
AvailabilityZone: !Select 
  - 0
  - !GetAZs 
    Ref: 'AWS::Region'
```

```yaml
AvailabilityZone: !Select 
  - 0
  - Fn::GetAZs: !Ref 'AWS::Region'
```



















