# Read, Generate and Modify Configuration

## Reading

[Resources](https://developer.hashicorp.com/terraform/language/v1.1.x/resources)  
[Data Sources](https://developer.hashicorp.com/terraform/language/v1.1.x/data-sources)  
[Resource Graph](https://developer.hashicorp.com/terraform/internals/v1.1.x/graph)  
[Complex Types](https://developer.hashicorp.com/terraform/language/v1.1.x/expressions/type-constraints#complex-types)  
[Functions](https://developer.hashicorp.com/terraform/language/v1.1.x/functions)  

## Notes

### **Variables and outputs**

Variables are straightforward in Terraform if you have previous coding experience.

Please refer to [Objective 5 - Interact with Terraform Modules](../5-%20Interact%20with%20Terraform%20Modules/5-notes.md) for examples of defining and using variables and outputs, along with details about their scope.

What was missed in the above section was how to use a variable in a string, which can be done with the following: `"${var.name}-rest-of-string"`.

### **Resources**

A resource block is how we define infrastructure we want built in our environment. A resource block can range from something quite simple to something rather more complex.

```terraform
resource "aws_instance" "web" {
  ami           = "ami-a1b2c3d4"
  instance_type = "t2.micro"
}
```

The resource is given a *resource type* and a *name*. The name is used to later reference the resource within the module scope, and the resource type tells the provider what you want to build. The resource type and name together serve as an identifier for a given resource and so must be unique within a module. `<RESOURCE TYPE>.<NAME>.` You can use this access attributes of the built resource with `<RESOURCE TYPE>.<NAME>.<ATTRIBUTE>`.

An *implicit dependency* will be created when a resource references a named value from another resource. If you use the `[depends_on]` variable, you have created an *explicit dependency*. 

### **Data sources**

*Data sources* allow Terraform to use information defined outside of Terraform, defined by another separate Terraform configuration. Each provider may offer data sources alongside its set of resource types.

Data sources can be accessed using a `data` block:

```terraform
data "aws_ami" "example" {
  most_recent = true

  owners = ["self"]
  tags = {
    Name   = "app-server"
    Tested = "true"
  }
}
```

They are *read* objects and as such shouldn't be confused with `resource` blocks that *create, update, modify and read* the resources.

If the query constraint arguments for a data resource refer only to constant values or values that are already known, the data resource will be read and its state updated during Terraform's "refresh" phase, which runs prior to creating a plan. This ensures that the retrieved data is available for use during planning and so Terraform's plan will show the actual values obtained.

You can access data from a data block using `data.<TYPE>.<NAME>.<ATTRIBUTE>`.

### **Resource graph**

Terraform builds a dependency graph from the Terraform configurations, and walks this graph to generate plans, refresh state, and more.

A graph is built from these node types:

- **Resource Node** - Represents a single resource. If you have the count metaparameter set, then there will be one resource node for each count. The configuration, diff, state, etc. of the resource under change is attached to this node.

- **Provider Configuration Node** - Represents the time to fully configure a provider. This is when the provider configuration block is given to a provider, such as AWS security credentials.

- **Resource Meta-Node** - Represents a group of resources, but does not represent any action on its own. This is done for convenience on dependencies and making a prettier graph. This node is only present for resources that have a count parameter greater than 1.

To walk the graph, a standard depth-first traversal is done. Graph walking is done in parallel: a node is walked as soon as all of its dependencies are walked.

### **Types**

- `List`
  - Lists/tuples are represented by a pair of square brackets containing a comma-separated sequence of values, like `["a", 15, true]`

- `Map`
  - Maps/objects are represented by a pair of curly braces containing a series of <KEY> = <VALUE> pairs:
```terraform
{
  name = "John"
  age  = 52
}
```
  - Maps can be separated using a comma or a line break
  - The keys in a map must be strings; they can be left unquoted if they are a valid identifier, but must be quoted otherwise. You can use a non-literal string expression as a key by wrapping it in parentheses, like (var.business_unit_tag_name) = "SRE"
- `Set`
  - Used in much the same way that a `list` is

A *structural type* will allow *several distinct types* to be grouped together as a single value. Like the list `["a", 15, true]`, where as a *collection type* will only allow *one* type, such as `["a", "b", "c"]`. 


### **Functions**

The Terraform language includes a number of built-in functions that you can call from within expressions to transform and combine values. The general syntax for function calls is a function name followed by comma-separated arguments in parentheses `max(5,12,9)`.

To treat the value of a variable as sensitive, you need to surround the variable with a `sensitive()` function.

```terraform
locals {
  sensitive_content = sensitive(file("${path.module}/sensitive.txt"))
}
```

You can test functions using `terraform console`.

### **Secure secret injection**

For the following examples I will show how to populate this variable:
```terraform
variable "username" {
  description = "The username for the DB master user"
  type        = string
}
```

1) **Environment Variables**  
You can set the environment variable called `TF_VAR_username` to populate `var.username`
1) **Encrypted Files** (e.g., KMS, PGP, SOPS)  
Create a file containing `username: <username>` and then encrypt this file and include it into version control, you can then use a `data` block to read the file into Terraform, then load that into a `locals` variable block and then use it in your `resource` 
1) **Secret Stores** (e.g., Vault, AWS Secrets manager)  
This method is similar to storing the variable in a file, but instead you use a cloud provider vault, and then pull it into your configuration using a `data` block

## Exam Objectives / Testing

<details>
<summary>Demonstrate use of variables and outputs</summary>

Please refer to [Objective 5 - Interact with Terraform Modules](../5-%20Interact%20with%20Terraform%20Modules/5-notes.md) for examples of defining and using variables and outputs.
</details>

<details>
<summary>Describe secure secret injection best practice</summary>

- Leave the variable name undefined and use one of the following processes to populate it
- There's three ways to populate secret values
  - Environment variables
  - Encrypted files
  - Secret stores
</details>

<details>
<summary>Understand the use of collection and structural types</summary>

- A *structural type* will allow *several distinct types* to be grouped together as a single value. Like the list `["a", 15, true]`
- A *collection type* will only allow *one* type, such as `["a", "b", "c"]`

</details>

<details>
<summary>Create and differentiate resource and data configuration</summary>

- A `resource` is used to modify your infrastructure in your `provider`, whereas a `data` block is for read-only data
- Defining a `resource` block
```terraform
resource "aws_instance" "web" {
  ami           = "ami-a1b2c3d4"
  instance_type = "t2.micro"
}
```
- Defining a `data` block
```terraform
data "aws_ami" "example" {
  most_recent = true

  owners = ["self"]
  tags = {
    Name   = "app-server"
    Tested = "true"
  }
}
```
</details>

<details>
<summary>Use resource addressing and resource parameters to connect resources together</summary>

- The `resource` is given a *resource type* and a *name*
- The resource type and name together serve as an identifier for a given resource and so must be unique within a module
- You can use `<RESOURCE TYPE>.<NAME>.<ATTRIBUTE>` to access attributes from a resource, this can then be used to populate arguments in other resources
</details>

<details>
<summary>Use HCL and Terraform functions to write configuration</summary>

- Terraform includes a number of built-in functions
- The general syntax for function calls is function name followed by comma-separated arguments in parentheses `max(5,12,9)`
- You can test functions using `terraform console`
</details>

<details>
<summary>Describe built-in dependency management (order of execution based)</summary>

- Terraform builds a dependency graph from configuration and walks this graph to perform its functions
- The walking of the graph is done with depth-first traversal and is done in parallel
- The graph is built from these node types
  - Resource Node
  - Provider Configuration Node
  - Resource Meta-Node
</details>
