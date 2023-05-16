# The Purpose of Terraform - Spaced Repetition (Anki) Cards

What is the benefit of Terraform being multi-cloud and provider-agnostic? Increased reliability 

How does using Terraform with multiple cloud providers increase your reliability? If one provider goes down, all of your infrastructure isn't affected

How does Terraform state improve the performance of 'terraform apply'? By caching the state of your infrastructure so that Terraform doesn't have to query the providers every run

How is Terraform state beneficial from the perspective of syncing? It enables multiple people to be able to work on one Terraform project

How does Terraform enable multiple people to work on one project? By using remote state

What will Terraform do to make sure two people using a remote storage solution can't run terraform apply at the same time? Remote locking

What flag do you need to pass to Terraform to use the state file as a cache and not query the providers? -refresh=false

How is Terraform state beneficial from the perspective of tracking metadata? It allows Terraform to infer what order to delete resources in

When you want to use existing infrastructure with your Terraform config, what tool do you use? An import resource block

