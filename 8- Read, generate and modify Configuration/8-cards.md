# Read, Generate and Modify Configuration - Spaced Repetition (Anki) Cards

How do you access attributes of a `resource` block in Terraform? `<RESOURCE TYPE>.<NAME>.<ATTRIBUTE>`

What would you use to retrieve read-only data from your cloud provider in Terraform? A `data` block

What is the difference between a `resource` and `data` block in Terraform? A data block is read-only, a resource block modifies resources

How do you access data from a `data` block in Terraform? `data.<TYPE>.<NAME>.<ATTRIBUTE>`

What does Terraform use to generate plans, refresh state and apply changes? A dependency graph

What traversal will Terraform use to walk its graph? A parallel depth-first search

How do you define a list/tuple in Terraform? ["a", "b", "c"]

How do you define a map/object in Terraform? 
{
  name = "John",
  age  = 52
}

What is the type constraint on a structural type in Terraform? It will allow all types

What is the type constraint on a collection type in Terraform? It will only allow one type

What is the general pattern for calling functions in Terraform? A function name followed by comma-separated arguments in parentheses `max(5,12,9)`

How do you mark a variable as sensitive in Terraform? You surround it with the sensitive function `sensitive(data)`

What can you use to test your Terraform functions? The `terraform console`

What are the three methods of injecting secrets into your Terraform configuration? {{c1::Environment Variables}}, {{c2::Encrypted Files}}, {{c3::Secret Stores}}

How do you use an environment variable to set a variable value in Terraform? set `TF_VAR_<variable_name>`

What block do you use to download secrets (whether a file or from a vault) to populate your Terraform config with? A `data` block

How do you use a variable in a string in Terraform? `"${var.name}-rest-of-string"`

What is a implicit dependency in Terraform? When two resources rely on each other, but you haven't specified depends on

What is an explicit dependency in Terraform? When you specify the `[depend_on]` argument to a resource