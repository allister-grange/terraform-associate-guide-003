# Interact with Terraform Modules - Spaced Repetition (Anki) Cards

What do all `module` blocks require in Terraform? A source argument

What can a source argument be for a module in Terraform? A URL, local path or a registry source address

When importing a module from the Terraform public registry, what do you use as the source? A registry source address `<NAMESPACE>/<NAME>/<PROVIDER>`

What are modules in Terraform? They are containers for multiple resources that enable reusability

When adding, removing or modifying modules in Terraform, what do you need to run? `terraform init`

When installing a Terraform module from a module registry, what should you pass in? A version argument

How do you access outputs from a Terraform module? `module.<name>.<output_value>`

When defining a module, what do you need to use to define what inputs can be passed into the module? Variables

When passing variables into the child modules, the calling module passes the variables in how? Arguments in the module block

When accessing a variable in Terraform, what is the prefix? `var.`

The root module variables are set using the {{c1::CLI}}, {{c2::environment variables}}, {{c3::variable files}} or in a {{c4::Terraform Cloud workspace}}.

How would you automatically load in variables from a file in Terraform? Name the file `terraform.tfvars` or `terraform.tfvars.json`, or files ending in `.auto.tfvars` or `.auto.tfvars.json`

When defining variables in a `.tfvar` file, what is the difference? You don't need to include the `variable` block surrounding the variable

The Terraform get command is used for what? To download and update modules 