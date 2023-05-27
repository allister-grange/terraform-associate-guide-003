# Implement and Maintain State - Spaced Repetition (Anki) Cards

What do backends in Terraform store? State files

What is a state file used for in Terraform? To keep a track of resources that Terraform manages

What are the three places that Terraform can use for backends? Local, Terraform cloud and a remote backend (cloud)

What block is used to store state remotely in Terraform? The `backend` block

Where does the `backend` block go in Terraform? Within the `terraform` block

What is the limitation with arguments to the `backend` block in Terraform? It cannot refer to named values (like variables, locals or data sources)

Whenever a configuration's backend changes, what must you do? Run `terraform init`

Where is state stored by default in Terraform? Locally

Why are local state files not optimal in Terraform? You cannot collaborate effectively and secrets are in plain text

When passing in arguments for your backend configuration for Terraform to place into the `backend` block, what is your configuration considered to be? A partial configuration

What is a partial configuration in Terraform? When you leave sensitive configuration arguments for you `backend` block empty and pass them in through some other means

How can you pass in arguments to a partial configuration in Terraform? Using a file, cli arguments, or interactively

How method does Terraform use to enable collaboration with remote state (if two people `apply` at the same time)? State locking 

What is resource drift in Terraform? When your resources within your cloud provider have been modified through a method other than Terraform

If you suspect that you have resource drift in your Terraform, what should you run? `terraform plan -refresh-only`

After running `terraform plan -refresh-only` and seeing that there have been changes in your resources, what do you need to do? Update your configuration to match the changes

What Terraform command can be used to remove the lock on the state for the current configuration? `terraform force-unlock <lock_id>`