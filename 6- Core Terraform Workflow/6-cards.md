# Core Terraform Workflow - Spaced Repetition (Anki) Cards

The core Terraform workflow has three steps:

1) {{c1::**Write** - Author infrastructure as code}}
1) {{c2::**Plan** - Preview changes before applying, `terraform plan`}}
1) {{c3::**Apply** - Provision reproducible infrastructure, `terraform apply`}}

When working in a team, where does Terraform recommend executing your plans? In a continuous integration environment

How do you initialize a working directory containing Terraform configuration files? `terraform init`

What will `terraform init` configure? Backend state configurations, modules and plugins

What will Terraform build after running `terraform init`? A dependency version lock file for your plugins

How do you validate that your Terraform configuration files are syntactically valid and internally consistent? `terraform validate`

What command do you use in Terraform to create an execution plan for the changes you are making in your infrastructure? `terraform plan`

If you want to output a plan file to disk to use later in Terraform, what do you run? `terraform plan -out=<plan_file>`

How do you read a Terraform plan on disk in a human-readable format? `terraform show <plan_file>`

How do you produce and execute the actions you have configured in your Terraform? `terraform apply`

How do you execute the actions in a Terraform plan that is on disk? `terraform apply <plan_file>`

How do you destroy all Terraform resources? `terraform destroy`

How do you format your Terraform configuration files? `terraform fmt`

Why is `terraform init` not sufficient to test your code? Because it is only interested in the `terraform`, `provider` and `module` blocks

When does Terraform validate your providers? When running `terraform init`

What does `terraform apply` do in Terraform? Executes a plan to modify Terraform resources

After executing a `terraform plan`, you notice that a resource has a tilde (~) next to it. What does this mean? The resource will be updated in place