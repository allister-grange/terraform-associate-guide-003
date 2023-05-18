# The Purpose of Terraform

## Reading

[What is Terraform?](https://developer.hashicorp.com/terraform/intro)  
[Use cases](https://developer.hashicorp.com/terraform/intro/v1.1.x/use-cases)  
[Purpose of Terraform State](https://developer.hashicorp.com/terraform/language/v1.1.x/state/purpose)

## Notes

### Cloud-agnostic

Terraform can provision infrastructure across many providers in one workflow. When provisioning resources across multiple cloud providers increase your tolerance as you protect yourself form provider specific outages. 

### Terraform State

The two requirements for Terraform to run are: the state and the configuration files. So, why is state good?

**Mapping to the Real World**

The state file is used as a database for resources you have provisioned in your providers. 

Be warned, when importing existing resources into your Terraform config, you need to make sure that you maintain only one reference to it in your configuration.

**Metadata**

Terraform needs to track metadata about the built resources as it needs to be able to calculate dependency trees so that it knows the sequencing of deletes. This is important when it comes to deleting resources across providers as well. 

**Performance**

When your state becomes rather large, you can use the state file as a cache so that you don't need to go out to your provider to check the status of all of the infrastructure when writing a plan. This is enabled with the `-refresh=false` flag.

**Syncing**

Remote state allows for people to collaborate on the same Terraform project. Terraform performs remote locking and will prevent users from running Terraform at the same time. Without state this wouldn't be possible.

## Exam Objectives / Testing

<details>
<summary>Explain multi-cloud and provider-agnostic benefits</summary>

- Increases reliability through distributing your infrastructure across multiple platforms
</details>

<details>
<summary>Explain the benefits of state</summary>

<details>
<summary>Performance</summary>

- You can cache the state of your infrastructure so that Terraform doesn't have to query the providers every run
</details>

<details>
<summary>Syncing</summary>

- State enables multiple people to be able to work on one Terraform project by using remote state and locking configuration changes to one person at a time
</details>

<details>
<summary>Metadata</summary>

- By using state, Terraform can track metadata needed to infer what order to delete resources in
</details>
