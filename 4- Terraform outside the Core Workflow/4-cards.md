# Terraform Outside of the Core Workflow - Spaced Repetition (Anki) Cards

What tool do you use when you want to import in existing infrastructure under Terraform management? `terraform import`

Importing infrastructure involves five steps:

1) {{c1::Identify the existing infrastructure you will import.}}
2) {{c2::Import infrastructure into your Terraform state file.}}
3) {{c3::Write Terraform configuration that matches that infrastructure.}}
4) {{c4::Review the Terraform plan to ensure the configuration matches the expected state and }}infrastructure.
5) {{c5::Apply the configuration to update your Terraform state.}}

How do you import an AWS instance with the resource_id of i-abcd1234 into a Terraform resource with the id of aws_instance.foo? terraform import aws_instance.foo i-abcd1234

What do you need to be careful of when using import in Terraform? That you only import a resource into your configuration once

When running `terraform state` commands that modify the state, what will Terraform produce? A backup file

What is a tainted resource in Terraform? A resource in an incomplete or degraded state

What will happen to a tainted resource when `terraform apply` is run? Terraform will rebuild it

What does the `terraform state list` command do? It will display the resources addresses for all resources in your state

What command in Terraform would you run to list all resources in your state? `terraform state list`

What does the `terraform state show <resource_address>` command do? It will show detailed information about one resource

What command in Terraform would you run to show detailed information about one resource? `terraform state show <resource_address>`

What does the `terraform refresh` command do? It will update the state data to match the real-world condition of the managed resources

What command in Terraform would you run to update the state data to match the real-world condition of the managed resources? `terraform refresh`

What does the `terraform state mv` command do? It can be used to move resources from one state file to another, or to rename resources

What command in Terraform would you run to rename a resource? `terraform state mv`

What command in Terraform would you run to move a resource from one state file to another? `terraform state mv`

What does the `terraform state rm` command do? It will stop Terraform from managing a resource *without* deleting the real-world resource

What command in Terraform would you run to stop managing a resource without deleting it? `terraform state rm`

What does the `terraform state pull` command do? It will manually download and override your local copy of state from a remote state location

What command in Terraform would you run to manually download and override your local copy of state from a remote state location? `terraform state pull`

What does the `terraform state push` command do? Manually upload a local state file to a remote state

What does the `terraform apply -replace=<resource_address>` command do? It will rebuild that resource

What command in Terraform would you run to replace/re-establish a resource? `terraform apply -replace=<resource_address>`

What does the `terraform taint <resource_address>` command do? Marks a resource as tainted so that it's replaced next `terraform apply`

What command in Terraform would you run to trigger a resource to be rebuilt on the next `terraform apply`? `terraform taint <resource_address>`

What does the `terraform untaint <resource_address>` command do? Un-taints a resource so that it will not be replaced on the next `terraform apply`

What command in Terraform would you run to un-taint a resource? `terraform untaint <resource_address>`

What environment variable do you set to change the verbosity of the logs in Terraform? `TF_LOG`

To persist Terraform logs, what environment variable do you set? `TF_LOG_PATH`

Where are debugging logs used in Terraform outputted to? `stderr`