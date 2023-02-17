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

* Subnet bits is the inverse of subnet mask. To calculate the required host bits for a given subnet bits, subtract the subnet bits from 32 for IPv4 or 128 for IPv6.

**Return Value**
An array of CIDR address blocks




