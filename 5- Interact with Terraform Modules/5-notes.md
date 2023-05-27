# Interact with Terraform Modules

## Reading

[Modules](https://developer.hashicorp.com/terraform/language/modules)  
[Finding and Using Modules](https://developer.hashicorp.com/terraform/registry/modules/use)  
[Input Variables](https://developer.hashicorp.com/terraform/language/values/variables)  
[Module Blocks](https://developer.hashicorp.com/terraform/language/v1.1.x/modules/syntax#accessing-module-output-values)  

## Notes

### **Modules**

*Modules* are containers for multiple resources that are used together. Modules are the main way to reuse resource configurations in Terraform.

There are *root modules* and *child modules*. Child modules are used within root modules.

#### **Calling a child module**

When calling a module, you must pass in values for its input variables. 

```terraform
module "servers" {
  source = "./app-cluster"

  servers = 5
}
```

All modules require a `source` argument, which is a pointer either to the local module, or to a remote module source that Terraform will then download to use.

You must run `terraform init` when adding, removing or modifying modules.

#### **Setting the module version**

When using public modules from a module registry, it's recommended to pass in a `version` argument into the `module` block. This is not required for local modules. 

To update modules, you can run the `terraform get` command.

#### **Accessing module output values**

The resources defined inside a module are encapsulated, so the calling module cannot access them directly, instead you use *output values* to selectively export values to then be used in the calling module.

To reference an output from a module block you can call it with `module.<name>.<output_value>`.

#### **Using input variables**

Each input variable accepted by a `module` must be declared within that `module` using a variable block:

You can force validation on a variable block by using the `validation` block.

```terraform
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```

Variables are then used by calling an object named `var`.

```terraform
resource "aws_instance" "example" {
  instance_type = "t2.micro"
  ami           = var.image_id
}
```

When defining variables within a `.tfvar` file, you do not need to build the `variable` block, you only need the variable name assignment:

```terraform
image_id = "ami-abc123"
availability_zone_names = [
  "us-east-1a",
  "us-west-1c",
]
```

#### **Module sources**

The `source` for a module tells Terraform where to find the source code for the module. 

The `source` argument can be treated as a URL, or in special cases you can prefix with actions such as `git::` or `s3::`. If your module is local, you can also pass in a path.

When using modules from the Terraform registry, you can reference the `registry source address` like you would with a provider. `<NAMESPACE>/<NAME>/<PROVIDER>`.

#### **Variable scope within modules/child modules**

The root module variables are set using the CLI, environment variables, variable files or in a Terraform Cloud workspace.

When passing variables into the child modules, the calling module passes the variables in using the `module` block.

The outputs defined by the child module will then be accessible in the calling module.

Terraform will automatically pick up files with the name `terraform.tfvars` or `terraform.tfvars.json`, or files ending in `.auto.tfvars` or `.auto.tfvars.json`

Variables defined within modules will not be accessible by their parent module.

## Exam Objectives / Testing

<details>
<summary>Contrast and use different module source options including the public Terraform Module Registry</summary>

- All `module` blocks require a source argument
- This source argument can be a local path, a URL or a special format for module providers like `git`, `s3` buckets and `svn`
- When using a module from the Terraform public registry, you use the format `<NAMESPACE>/<NAME>/<PROVIDER>`, which is very similar to a `source address` for a provider
</details>

<details>
<summary>Interact with module inputs and outputs</summary>

- When defining a `module` block, you need to pass in the `source` argument and the inputs required for that module
- The inputs for that module are decided by variables that are used within the `child module`, and are then defined when passed in as input by the calling module
- When `terraform apply` is run, the module will have output that it defines that can then be used by the calling module
</details>

<details>
<summary>Describe variable scope within modules/child modules</summary>

- The root module variables are set using the CLI, environment variables and variable files
- When passing variables into the child modules, the calling module passes the variables in using the `module` block, these variables are then used within the scope of the child module
</details>

<details>
<summary>Set module version</summary>

- When using remote modules, it's recommended that you set the version you're using by passing the `version` argument into the `module`
</details>