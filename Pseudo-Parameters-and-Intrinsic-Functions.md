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


















