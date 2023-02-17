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







