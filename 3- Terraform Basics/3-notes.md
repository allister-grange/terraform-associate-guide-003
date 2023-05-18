# Terraform Basics

## Reading

[Get Get Started - AWS](https://developer.hashicorp.com/terraform/tutorials/aws-get-started)  
[Terraform Settings](https://developer.hashicorp.com/terraform/language/v1.1.x/settings)  
[Purpose of Terraform State](https://developer.hashicorp.com/terraform/language/v1.1.x/state/purpose)  
[Manage Terraform Versions](https://developer.hashicorp.com/terraform/tutorials/configuration-language/versions)  
[Providers](https://developer.hashicorp.com/terraform/language/v1.1.x/providers)  
[Provider Requirements](https://developer.hashicorp.com/terraform/language/v1.1.x/providers/requirements)  
[How Terraform Works With Plugins](https://developer.hashicorp.com/terraform/plugin/how-terraform-works)  
[Provider Configuration](https://developer.hashicorp.com/terraform/language/v1.1.x/providers/configuration)  
[Lock and Upgrade Provider Versions](https://developer.hashicorp.com/terraform/tutorials/configuration-language/provider-versioning)  
[Dependency Lock File](https://developer.hashicorp.com/terraform/language/v1.1.x/files/dependency-lock)

## Notes

### **Terraform providers**

Providers are plugins that allow Terraform to interact with cloud providers, SaaS providers, and other APIs. Providers supply the **resource types** and **data sources** that Terraform can manage. Without providers, Terraform cannot build any infrastructure. You can think of providers as downloading the API that Terraform then interacts with to manage infrastructure.

Providers come from the **Terraform Registry** for most large providers, but you can download them from other sources if your provider is in some niche.

Providers are defined as follows:

```terraform
provider "azurerm" {
  // mainly holds provider specific configuration
  features {}
  skip_provider_registration = true
}

```

Providers must be specified in the `required_providers` block within the `terraform` resource before they can be used. A `required_providers` block consists of a local name, a source location, and a version constraint:

```terraform
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=3.0.0"
    }
  }
}
```

You can use variables in provider configurations, but not outputs from resources.

There are also two "meta-arguments" that are defined by Terraform itself and available for all provider blocks:
  - `alias`, for using the same provider with different configurations for different resources
  - `version`, which Terraform **doesn't recommend** using (use provider requirements instead)


#### **Using Multiple Providers**

```terraform
# The default provider configuration; resources that begin with `aws_` will use
# it as the default, and it can be referenced as `aws`.
provider "aws" {
  region = "us-east-1"
}

# Additional provider configuration for west coast region; resources can
# reference this as `aws.west`.
provider "aws" {
  alias  = "west"
  region = "us-west-2"
}
```

To then use that alternate provider, you can select it as a reference:

```terraform
resource "aws_instance" "foo" {
  provider = aws.west

  # ...
}
```

#### **How Terraform Fetches Providers**

**Source Addresses** are used to uniquely identity providers. They are built in three parts: `[<HOSTNAME>/]<NAMESPACE>/<TYPE>`

- Hostname (optional): The hostname of the Terraform registry that distributes the provider
- Namespace: An organizational namespace within the specified registry
- Type: short name for the platform or system the provider manages

An example of a source address is `registry.terraform.io/hashicorp/http`.

Terraform will then download providers from this source address when `terraform init` is run. This will create a lock file to ensure that Terraform will use the same provider versions when re-running `terraform apply`.

### **Plugin-based architecture**

Plugins enable developers to extend Terraform by writing new plugins or compiling modified versions of existing plugins.

There are two parts to Terraform: **Terraform Core** and **Terraform Plugins**. **Terraform Core** provides the entry point to `terraform` and then it enables people to build upon it with plugins.

## Exam Objectives / Testing

<details>
<summary>Install and version Terraform providers</summary>

<details>
<summary>Installing providers</summary>

- To install a provider, you need both a `required_providers` block in the `terraform` resource, and a `provider` resource block detailing the configuration for that provider
- The `required_providers` block will need the **source address** of the provider
- You prepare the provider for being used by running `terraform init`
</details>

<details>
<summary>Versioning providers</summary>

- You can version your provider in the `required_providers` block in the `terraform resource`
- `terraform init` will create a versioning lock file when it's run
</details>

</details>

<details>
<summary>Write Terraform configuration using multiple providers</summary>

- You can define multiple providers and reference them using their `alias` field which is passed into the `provider` resource block
</details>

<details>
<summary>Describe how Terraform finds and fetches providers</summary>

- **Source Addresses** are used to uniquely identity providers. They are built in three parts: `[<HOSTNAME>/]<NAMESPACE>/<TYPE>`. Terraform will then download providers from this source address when `terraform init` is run. The `hostname` determines what **registry** terraform will look in for the provider. 

</details>

<details>
<summary>Describe plugin-based architecture</summary>

- Plugins enable Terraform's platform to be extended. There are two parts to Terraform: **Terraform Core** and **Terraform Plugins**. **Terraform Core** provides the entry point to `terraform` and then it enables people to build upon it with plugins.
</details>
