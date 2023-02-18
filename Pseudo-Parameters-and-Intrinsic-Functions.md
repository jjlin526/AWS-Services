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

### Fn::ImportValue
The intrinsic function `Fn::ImportValue` returns the value of an output exported by another stack. You typically use this function to create cross-stack references. 
* In the following example template snippets, Stack A exports VPC security group values and Stack B imports them.

The following restrictions apply to cross-stack references:

* For each AWS account, `Export` names must be unique within a region.
* You can't create cross-stack references across regions. You can use the intrinsic function `Fn::ImportValue` to import only values that have been exported within the same region.
* For outputs, the value of the `Name` property of an `Export` can't use `Ref` or `GetAtt` functions that depend on a resource.
* Similarly, the `ImportValue` function can't include `Ref` or `GetAtt` functions that depend on a resource.
* You can't delete a stack if another stack references one of its outputs.
* You can't modify or remove an output value that is referenced by another stack.

**Stack A Export**  

```yaml
Outputs:
  PublicSubnet:
    Description: The subnet ID to use for public web servers
    Value:
      Ref: PublicSubnet
    Export:
      Name:
        'Fn::Sub': '${AWS::StackName}-SubnetID'
  WebServerSecurityGroup:
    Description: The security group ID to use for public web servers
    Value:
      'Fn::GetAtt':
        - WebServerSecurityGroup
        - GroupId
    Export:
      Name:
        'Fn::Sub': '${AWS::StackName}-SecurityGroupID'
```

**Stack B Import**  

```yaml
Resources:
  WebServerInstance:
    Type: 'AWS::EC2::Instance'
    Properties:
      InstanceType: t2.micro
      ImageId: ami-a1b23456
      NetworkInterfaces:
        - GroupSet:
            - Fn::ImportValue: 
              'Fn::Sub': '${NetworkStackNameParameter}-SecurityGroupID'
          AssociatePublicIpAddress: 'true'
          DeviceIndex: '0'
          DeleteOnTermination: 'true'
          SubnetId: Fn::ImportValue 
            'Fn::Sub': '${NetworkStackNameParameter}-SubnetID'
```

**Declaration**  

```yaml
Fn::ImportValue: sharedValueToImport

!ImportValue sharedValueToImport
```

You can't use the short form of `!ImportValue` when it contains a `!Sub`.

```yaml
# do not use
               !ImportValue 
'Fn::Sub': '${NetworkStack}-SubnetID' 
```

Instead, you must use the full function name, for example:
```yaml
Fn::ImportValue:
  !Sub "${NetworkStack}-SubnetID"
```

**Parameters**  
- **sharedValueToImport**: The stack output value that you want to import

**Return Value**  
The stack output value.

### Fn::Join
The intrinsic function `Fn::Join` appends a set of values into a single value, separated by the specified delimiter. If a delimiter is the empty string, the set of values are concatenated with no delimiter.

```yaml
Fn::Join: [ delimiter, [ comma-delimited list of values ] ]

!Join [ delimiter, [ comma-delimited list of values ] ]
```

**Parameters**  
- **delimiter**: The value you want to occur between fragments. The delimiter will occur between fragments only. It won't terminate the final value.
- **ListOfValues**: The list of values you want combined.

### Examples

```yaml
!Join [ ":", [ a, b, c ] ]
```

The following example uses `Fn::Join` to construct a string value. It uses the `Ref` function with the `AWS::Partition` parameter and the `AWS::AccountId` pseudo parameter.

```yaml
!Join
  - ''
  - - 'arn:'
    - !Ref AWS::Partition
    - ':s3:::elasticbeanstalk-*-'
    - !Ref AWS::AccountId
```

### Fn::Length
The intrinsic function `Fn::Length` returns the number of elements within an array or an intrinsic function that returns an array.

```yaml
Fn::Length : IntrinsicFunction

Fn::Length : Array
```

### Examples
This example snippet returns the number of elements in an intrinsic function that returns an array. The function returns 3.

```yaml
Transform: 'AWS::LanguageExtensions'
#...
  Fn::Length: 
    !Split ["|", "a|b|c"]
#...
```

This example snippet returns the number of elements in a `Ref` intrinsic function that refers to a list parameter type. If the parameter with the name `ListParameter` is a list with 3 elements, the function returns 3.

```yaml
Transform: 'AWS::LanguageExtensions'
#...
  Fn::Length: 
    !Ref ListParameter
#...
```

This example snippet returns the number of elements in the array passed to the intrinsic function. The function returns 3.

Transform: 'AWS::LanguageExtensions'
#...
  Fn::Length: 
    - 1
    - !Ref ParameterName
    - 3
#...

### Fn::Select
The intrinsic function `Fn::Select` returns a single object from a list of objects by index.

```yaml
Fn::Select: [ index, listOfObjects ] 

!Select [ index, listOfObjects ]
```

### Examples

The following example returns: "grapes".

```yaml
!Select [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ]
```

You can use `Fn::Select` to select an object from a `CommaDelimitedList` parameter. You might use a `CommaDelimitedList` parameter to combine the values of related parameters, which reduces the total number of parameters in your template. For example, the following parameter specifies a comma-delimited list of three CIDR blocks:

```yaml
Parameters: 
  DbSubnetIpBlocks: 
    Description: "Comma-delimited list of three CIDR blocks"
    Type: CommaDelimitedList
    Default: "10.0.48.0/24, 10.0.112.0/24, 10.0.176.0/24"
```

To specify one of the three CIDR blocks, use `Fn::Select` in the Resources section of the same template, as shown in the following sample snippet:

```yaml
Subnet0: 
  Type: "AWS::EC2::Subnet"
  Properties: 
    VpcId: !Ref VPC
    CidrBlock: !Select [ 0, !Ref DbSubnetIpBlocks ]
```

**Nested Functions with Short Form YAML**  

The following examples show valid patterns for using nested intrinsic functions with the `!Select` short form. You can't nest short form functions consecutively, so a pattern like `!GetAZs !Ref` isn't valid.

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

### Fn::Split

To split a string into a list of string values so that you can select an element from the resulting string list, use the `Fn::Split` intrinsic function. Specify the location of splits with a delimiter, such as `,` (a comma). After you split a string, use the `Fn::Select` function to pick a specific element.

For example, if a comma-delimited string of subnet IDs is imported to your stack template, you can split the string at each comma. From the list of subnet IDs, use the `Fn::Select` intrinsic function to specify a subnet ID for a resource.

```yaml
Fn::Split: [ delimiter, source string ]

!Split [ delimiter, source string ]
```

### Examples

The following example splits a string at each vertical bar (`|`). The function returns `["a", "b", "c"]`

```yaml
!Split [ "|" , "a|b|c" ]
```

If you split a string with consecutive delimiters, the resulting list will include an empty string. The following example shows how a string with two consecutive delimiters and an appended delimiter is split. The function returns `["a", "", "c", ""]`.

```yaml
!Split [ "|" , "a||c|" ]
```

The following example splits an imported output value, and then selects the third element from the resulting list of subnet IDs, as specified by the `Fn::Select` function.

```yaml
!Select [2, !Split [",", !ImportValue AccountSubnetIDs]]
```

### Fn::Sub
The intrinsic function `Fn::Sub` substitutes variables in an input string with values that you specify. In your templates, you can use this function to construct commands or outputs that include values that aren't available until you create or update a stack.

```yaml
Fn::Sub:
  - String
  - Var1Name: Var1Value
    Var2Name: Var2Value
    
!Sub
  - String
  - Var1Name: Var1Value
    Var2Name: Var2Value
```

If you're substituting only template parameters, resource logical IDs, or resource attributes in the String parameter, don't specify a variable map.

```yaml
Fn::Sub: String

!Sub String
```

**Parameters**  
- **String**: A string with variables that AWS CloudFormation substitutes with their associated values at runtime. Write variables as `${MyVarName}`. Variables can be template parameter names, resource logical IDs, resource attributes, or a variable in a key-value map. If you specify only template parameter names, resource logical IDs, and resource attributes, don't specify a key-value map.
- 
If you specify template parameter names or resource logical IDs, such as `${InstanceTypeParameter}`, CloudFormation returns the same values as if you used the `Ref` intrinsic function. If you specify resource attributes, such as `${MyInstance.PublicIp}`, CloudFormation returns the same values as if you used the `Fn::GetAtt` intrinsic function.

To write a dollar sign and curly braces (`${}`) literally, add an exclamation point (`!`) after the open curly brace, such as `${!Literal}`. CloudFormation resolves this text as `${Literal}`.
- **VarName**: The name of a variable that you included in the String parameter.
- **VarValue**: The value that CloudFormation substitutes for the associated variable name at runtime.

**Return Value**  
CloudFormation returns the original string, substituting the values for all the variables.

The following examples demonstrate how to use the `Fn::Sub` function.

**Fn::Sub with a Mapping**  

The following example uses a mapping to substitute the `${Domain}` variable with the resulting value from the `Ref` function.

```yaml
Name: !Sub 
  - 'www.${Domain}'
  - Domain: !Ref RootDomainName
```

**Fn::Sub without a Mapping**  

The following example uses `Fn::Sub` with the `AWS::Region` and `AWS::AccountId` pseudo parameters and the `vpc` resource logical ID to create an Amazon Resource Name (ARN) for a VPC

The YAML example uses a literal block to specify the user data script.

```yaml
UserData:
  Fn::Base64:
    !Sub |
      #!/bin/bash -xe
      yum update -y aws-cfn-bootstrap
      /opt/aws/bin/cfn-init -v --stack ${AWS::StackName} --resource LaunchConfig --configsets wordpress_install --region ${AWS::Region}
      /opt/aws/bin/cfn-signal -e $? --stack ${AWS::StackName} --resource WebServerGroup --region ${AWS::Region}
```

### Fn::ToJsonString
The `Fn::ToJsonString` intrinsic function converts an object or array to its corresponding JSON string.

```yaml
Fn::ToJsonString: Object

Fn::ToJsonString: Array
```

### Example

This example snippet converts the object passed to the intrinsic function to a JSON string.

```yaml
Transform: 'AWS::LanguageExtensions'
#...
  Fn::ToJsonString: 
    key1: value1
    key2: !Ref ParameterName
#...
```

In both of these examples, if the `Ref` to `ParameterName` resolves to `resolvedValue`, the function resolves to the following JSON string:

```json
"{\"key1\":\"value1\"},{\"key2\":\"resolvedValue\"}"
```

This example snippet converts the array passed to the intrinsic function to a JSON string.

```yaml
Transform: 'AWS::LanguageExtensions'
#...
  Fn::ToJsonString: 
    - key1: value1
      key2: !Ref ParameterName
#...
```

### Fn::Transform

The intrinsic function `Fn::Transform` specifies a **macro** to perform **custom processing** on part of a stack template. Macros enable you to perform custom processing on templates, from simple actions like find-and-replace operations to extensive transformations of entire templates. 

You can also use `Fn::Transform` to call the `AWS::Include transform` transform, which is a macro hosted by AWS CloudFormation.

```yaml
Fn::Transform:
  Name : macro name
  Parameters :
    Key : value
    
Transform:
  Name: macro name
  Parameters:
    Key: value
```

### Examples

The following example calls the `AWS::Include` transform, specifying that the location to retrieve a template snippet from is passed in the `InputValue` parameter.

```yaml
'Fn::Transform':
  Name: 'AWS::Include'
  Parameters:
    Location: !Ref InputValue
```

The following example calls the `AWS::Include` transform, specifying that the location to retrieve a template snippet from is located in the `RegionMap` mapping, under the key `us-east-1` and nested key `s3Location`.

```yaml
!Transform
Name: AWS::Include
Parameters:
  Location: !FindInMap
    - RegionMap
    - us-east-1
    - s3Location
```

No support functions. CloudFormation passes any intrinsic function calls included in `Fn::Transform` to the specified macro as literal strings. 

### Ref

The intrinsic function `Ref` returns the value of the specified parameter or resource.
* When you specify a parameter's logical name, it returns the value of the parameter.
* When you specify a resource's logical name, it returns a value that you can typically use to refer to that resource, such as a physical ID.

```yaml
Ref: logicalName

!Ref logicalName
```

### Examples

The following resource declaration for an Elastic IP address needs the instance ID of an EC2 instance and uses the `Ref` function to specify the instance ID of the `MyEC2Instance` resource:

```yaml
MyEIP:
  Type: "AWS::EC2::EIP"
  Properties:
    InstanceId: !Ref MyEC2Instance
```

No support functions: You can't use any functions in the `Ref` function. You must specify a string that's a resource logical ID.

### Pseudo Parameters
Pseudo parameters are parameters that are predefined by AWS CloudFormation. You don't declare them in your template. Use them the same way as you would a parameter, as the argument for the `Ref` function.

The following snippet assigns the value of the `AWS::Region` pseudo parameter to an output value:

```yaml
Outputs:
  MyStacksRegion:
    Value: !Ref "AWS::Region"
```

### AWS::AccountId

Returns the AWS account ID of the account in which the stack is being created, such as `123456789012`.

### AWS::NotificationARNs

Returns the list of notification Amazon Resource Names (ARNs) for the current stack.

```yaml
myASGrpOne:
  Type: AWS::AutoScaling::AutoScalingGroup
  Version: '2009-05-15'
  Properties:
    AvailabilityZones:
    - "us-east-1a"
    LaunchConfigurationName:
      Ref: MyLaunchConfiguration
    MinSize: '0'
    MaxSize: '0'
    NotificationConfigurations:
    - TopicARN:
        Fn::Select:
        - '0'
        - Ref: AWS::NotificationARNs
      NotificationTypes:
      - autoscaling:EC2_INSTANCE_LAUNCH
      - autoscaling:EC2_INSTANCE_LAUNCH_ERROR
```

### AWS::NoValue

Removes the corresponding resource property when specified as a return value in the `Fn::If` intrinsic function.

For example, you can use the `AWS::NoValue` parameter when you want to use a snapshot for an Amazon RDS DB instance only if a snapshot ID is provided. If the `UseDBSnapshot` condition evaluates to true, CloudFormation uses the `DBSnapshotName` parameter value for the `DBSnapshotIdentifier` property. If the condition evaluates to false, CloudFormation removes the `DBSnapshotIdentifier` property.

```yaml
MyDB:
  Type: AWS::RDS::DBInstance
  Properties:
    AllocatedStorage: '5'
    DBInstanceClass: db.t2.small
    Engine: MySQL
    EngineVersion: '5.5'
    MasterUsername:
      Ref: DBUser
    MasterUserPassword:
      Ref: DBPassword
    DBParameterGroupName:
      Ref: MyRDSParamGroup
    DBSnapshotIdentifier:
    Fn::If:
      - UseDBSnapShot
      - Ref: DBSnapshotName
      - Ref: AWS::NoValue
```

### AWS::Partition

Returns the partition that the resource is in. For standard AWS Regions, the partition is `aws`. For resources in other partitions, the partition is `aws-partitionname`. For example, the partition for resources in the China (Beijing and Ningxia) Region is `aws-cn` and the partition for resources in the AWS GovCloud (US-West) region is `aws-us-gov`.

### AWS::Region

Returns a string representing the Region in which the encompassing resource is being created, such as `us-west-2`.

### AWS::StackId

Returns the ID of the stack as specified with the `aws cloudformation create-stack` command, such as `arn:aws:cloudformation:us-west-2:123456789012:stack/teststack/51af3dc0-da77-11e4-872e-1234567db123`.

### AWS::StackName

Returns the name of the stack as specified with the `aws cloudformation create-stack` command, such as `teststack`.

### AWS::URLSuffix

Returns the suffix for a domain. The suffix is typically `amazonaws.com`, but might differ by Region. For example, the suffix for the China (Beijing) Region is `amazonaws.com.cn`
