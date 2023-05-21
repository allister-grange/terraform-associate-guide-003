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

