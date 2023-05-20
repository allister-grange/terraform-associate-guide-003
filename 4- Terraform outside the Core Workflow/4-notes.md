# Terraform Outside of the Core Workflow

## Reading

[Command: state](https://developer.hashicorp.com/terraform/cli/v1.1.x/commands/state)  
[Manage Resources in Terraform State](https://developer.hashicorp.com/terraform/tutorials/state/state-cli)  
[Command: import](https://developer.hashicorp.com/terraform/cli/v1.1.x/commands/import)  
[Import Terraform Configuration](https://developer.hashicorp.com/terraform/tutorials/state/state-import)  
[Debugging Terraform](https://developer.hashicorp.com/terraform/internals/v1.1.x/debugging)  
[Troubleshoot Terraform](https://developer.hashicorp.com/terraform/tutorials/configuration-language/troubleshooting-workflow#enable-terraform-logging)  

## Notes

### **Terraform Import**

Terraform allows you to import existing infrastructure into Terraform management. This will bring the management of this resource under Terraform's control.

When importing, you must manually build a `resource` configuration block for the mapping of the resource.

Importing infrastructure involves five steps:

1) Identify the existing infrastructure you will import.
1) Import infrastructure into your Terraform state file.
1) Write Terraform configuration that matches that infrastructure.
1) Review the Terraform plan to ensure the configuration matches the expected state and infrastructure.
1) Apply the configuration to update your Terraform state.


#### **Commands**

`terraform import [options] <resource_id>` where the `resource_id` matches the existing resource in your provider

Example: `terraform import aws_instance.foo i-abcd1234` will import an AWS instance into the `aws_instance` resource named `foo`

#### **Usage Tips**

Make sure that each resource imported into Terraform is only reference once. Just like in programming, it's not good to have two references to one object as you may have unexpected behavior.

### **Terraform State Commands**

The `terraform state` command is used for advanced state management. 

When running `terraform state` commands that modify the state, Terraform will build a backup file, you can control where this outputs with the `-backup` arg.

#### **Tainting**

A resource can become tainted when an object is in an incomplete or a degraded state. In this case, running `terraform apply` will re-create the resource.

#### **Commands**

`terraform state list` will display the resources addresses for all resources in your state

`terraform state show <resource_address>` will show detailed information about one resource 

`terraform refresh` will update the state data to match the real-world condition of the managed resources

`terraform state mv` can be used to move resources from one state file to another, or to rename resources

`terraform state rm` will stop Terraform from managing a resource *without* deleting the real-world resource

`terraform state pull` will manually download and override your local copy of state from a remote state location

`terraform state push` will manually upload a local state file to a remote state (it shouldn't be used, let the normal workflow handle this)

`terraform apply -replace=<resource_address>` if you know that the state of a resource is corrupt and you want to replace that resource, you can force that with passing of the `-replace` arg to terraform

`terraform taint <resource_address>` to purposefully taint a resource so that it's replaced

`terraform untaint <resource_address>` when you know a resource is actually untainted and Terraform has marked it incorrectly

### **Logging**

To configure logging in Terraform you must manipulate environment variables. `TF_LOG` is used to change the detail of the logging you receive on stderr. 

You can set `TF_LOG` to one of the log levels `TRACE`, `DEBUG`, `INFO`, `WARN` or `ERROR` to change the verbosity of the logs.

To persist logs you can set the `TF_LOG_PATH`. 

## Exam Objectives / Testing

<details>
<summary>Describe when to use terraform import to import existing infrastructure into your Terraform state</summary>

- When you want an already existing resource in your infrastructure to be manged by Terraform
- This is good for gradually moving your infrastructure management over to Terraform
</details>

<details>
<summary>Use terraform state to view Terraform state</summary>

- `terraform state list` to view the resources addresses for all resources in your state
- `terraform state show <resource_address>` to view the detailed state for one resource
- `terraform show` can also be used to view state 
</details>

<details>
<summary>Describe when to enable verbose logging and what the outcome is</summary>

- You should enable logging when you want to debug an issue that you're having
- You can set the logging level using the environment variable `TF_LOG`
- The debugging logs are outputted to `stderr`
</details>


