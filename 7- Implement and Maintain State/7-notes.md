# Implement and Maintain State

## Reading

[Backends](https://developer.hashicorp.com/terraform/language/v1.1.x/settings/backends)  
[State Locking](https://developer.hashicorp.com/terraform/language/v1.1.x/state/locking)  
[Command: login](https://developer.hashicorp.com/terraform/cli/commands/login)  
[Cloud configuration](https://developer.hashicorp.com/terraform/language/settings/terraform-cloud)  
[Manage Resource Drift](https://developer.hashicorp.com/terraform/tutorials/state/resource-drift#introduce-drift)  

## Notes

### **Backends**

Backends define where Terraform's state snapshots are stored. Terraform state is used to keep track of resources that terraform manages.

Terraform can store its state in a remote backend, integrate with Terraform Cloud, or do neither and default to storing state locally.

Backend configuration is done using a `backend` block. The backend block goes within the `terraform` configuration block. A backend block cannot refer to named values (like variables, locals or data sources).

```terraform
terraform {
  backend "remote" {
    organization = "example_corp"

    workspaces {
      name = "my-app-prod"
    }
  }
}
```

Whenever a configuration's backend changes, you must run `terraform init` again to validate and configure the backend before you can perform any plans, applies, or state operations.d.

If you change your configuration settings you will be prompted to `reinitialize`. 

#### **Default local backend**

By default, the state is stored locally. This is not optimal as 1) secrets are in plain text in state and 2) you cannot collaborate effectively when you have two copies of state running for one Terraform configuration.

#### **Backend and cloud integration authentication methods**

When using Terraform cloud, Terraform will manage your state file for you. If you have a `cloud` block, you cannot specify a `backend` block for this reason.

Because `backend` configurations often require secrets, and you cannot refer to named values, you can pass in credentials into your terraform command to fill in a *partial configuration*. A partial configuration is where you purposefully omit certain backend arguments that contain secret information.

You can pass in these missing arguments using a file, cli arguments, or interactively. 

Passing in using cli:
```bash
terraform init \
    -backend-config="address=demo.consul.io" \
    -backend-config="path=example_app/terraform_state" \
    -backend-config="scheme=https"
```

To pass in the arguments using a file, `terraform init -backend-config=PATH`. The file name should follow use the suffix `.tfbackend`

#### **Remote state back end options**

- There are cloud provider storage solutions like an AWS S3 bucket, or Azure Blob Storage
- There is also the option of Terraform cloud that provides a smoother integration experience and convenience

It is important to note if your remote state provider supports *state locking*, which will lock the state file when a `terraform apply` is being run. This keeps your state consistent and helps with collaboration.

To unlock the state manually, you must run the `terraform force-unlock <lock_id>` command.

#### **Backend block and cloud integration in configuration**

Example Azure configuration

```terraform
terraform {
  backend "azurerm" {
    resource_group_name  = "StorageAccount-ResourceGroup"
    storage_account_name = "abcd1234"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

### **State Locking**

As stated above, it is important to note if your remote state provider supports *state locking*, which will lock the state file when a `terraform apply` is being run. This keeps your state consistent and helps with collaboration.

You can `force-unlock` the state but this is not recommended.

### **Resource drift and Terraform state**

Resource drift is when your resources within your cloud provider have been modified through a method other than Terraform.

If you suspect that your infrastructure configuration changed outside of the Terraform workflow, you can use a `terraform plan -refresh-only` to inspect what the changes to your state file would be. This is safer than the refresh subcommand, which automatically overwrites your state file without displaying the updates.

If you opt yes to `refresh`ing your data, your state will have the current state of your resources, and your 
configuration will be out of date. You want to now either update your configuration, or run `terraform apply` to revert the manual changes made in the cloud. 

### **Secret management in state files**

When you run Terraform commands with a local state file, Terraform stores secrets in plain text, even if you have flagged them as sensitive. Terraform needs to store these values in your state so that it can tell if you have changed them since the last time you applied your configuration.

In order to secure these secrets, you need to store your `state` in a `backend` that has correct access controls. 

## Exam Objectives / Testing

<details>
<summary>Describe default local backend</summary>

- Default location of state in local
- Secrets are in plain text in state
- Limits collaboration as you shouldn't have two copies of state representing one Terraform configuration, which you will have if two people clone one Terraform repo with no remote backend
</details>

<details>
<summary>Describe state locking</summary>

- When modifying resources in the cloud, your state file is updated
- You don't want this file to be corrupted by two people editing it as the same time, hence locking
- In order to lock the state file, it needs to be in a remote state solution that supports *state locking*
</details>

<details>
<summary>Handle backend and cloud integration authentication methods</summary>

- When using a remote backend for your state, you will need to authenticate
- You can use a *partial configuration* by leaving sensitive arguments black in your `backend` block 
- You can then pass in the definition of these sensitive arguments using a file, cli arguments, or interactively
</details>

<details>
<summary>Differentiate remote state back end options</summary>

- There are cloud provider storage solutions like an AWS S3 bucket, or Azure Blob Storage
- There is also the option of Terraform cloud that provides a smoother integration experience and convenience
- It's pertinent that your `backend` provides state locking for collaboration
</details>

<details>
<summary>Manage resource drift and Terraform state</summary>

- Resource drift is when your resources within your cloud provider have been modified through a method other than Terraform
- You can use a `terraform plan -refresh-only` to inspect what the changes to your state file would be from this drift
- If you update your resources outside of the Terraform flow, you should run `terraform plan -refresh-only` and then ensure that you update your Terraform configuration to match what is in the cloud provider
</details>

<details>
<summary>Describe backend block and cloud integration in configuration</summary>

- The `backend` block is configured within the `terraform` block
```terraform
terraform {
  backend "azurerm" {
    resource_group_name  = "StorageAccount-ResourceGroup"
    storage_account_name = "abcd1234"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```
</details>

<details>
<summary>Understand secret management in state files</summary>

- When you run Terraform commands with a local state file, Terraform stores secrets in plain text
- In order to secure these secrets, you need to store your `state` in a `backend`
</details>