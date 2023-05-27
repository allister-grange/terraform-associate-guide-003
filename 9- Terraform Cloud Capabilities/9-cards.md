# Terraform Cloud Capabilities - Spaced Repetition (Anki) Cards

What Hashicorp solution can you use with Terraform to streamline your experience with Terraform? Terraform Cloud

When more than one person is working on a Terraform project, you need at minimum to have a {{c1::remote state solution}}, and ideally also a {{c2::CI environment}}

Terraform Cloud offers what to run Terraform actions on your own private servers? Terraform Cloud Agents

Terraform Cloud manages infrastructure collections with {{c1::workspaces}} instead of directories

What would you use to create and share private modules for your corporation in Terraform? The private registry 

What is the name of Terraform's policy enforcer? Sentinel 

After you define policies in Sentinel in Terraform, where do you need to add them? To policy sets on workspaces

To switch workspaces in Terraform, what do you run? `terraform workspace select <workspace_name>`

Will Terraform create a new workspace when you run `terraform workspace select <workspane_name>? No

How do you create a new workspace in Terraform? `terraform workspace new <workspace_name>`