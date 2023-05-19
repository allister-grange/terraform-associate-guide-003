# Interact with Terraform Modules

[Modules](https://developer.hashicorp.com/terraform/language/modules)
[Finding and Using Modules](https://developer.hashicorp.com/terraform/registry/modules/use)
[Input Variables](https://developer.hashicorp.com/terraform/language/values/variables)
[Module Blocks](https://developer.hashicorp.com/terraform/language/v1.1.x/modules/syntax#accessing-module-output-values)

## Notes

### **Modules**

*Modules* are containers for multiple resources that are used together. Modules are the main way to reuse resource configurations in Terraform.

There are *root modules* and *child modules*. Child modules are used within root modules.

#### **Calling a child module**

When calling a module, you must pass in values for its input variables. 

```terraform
module "servers" {
  source = "./app-cluster"

  servers = 5
}
```

All modules require a `source` argument, which is a pointer either to the local module, or to a remote module source that Terraform will then download to use.

You must run `terraform init` when adding, removing or modifying modules.

#### **Set module version**

When using public modules from a module registry, it's recommended to pass in a `version` argument into the `module` block. This is not required for local `modules`. 

#### **Accessing Module Output Values**

The resources defined inside a module are encapsulated, so the calling module cannot access them directly, instead you use *output values* to selectively export values to then be used in the calling module.

To reference an output from a module block you can call it with `module.<name>.<output_value>`.



- 5a)	Contrast and use different module source options including the public Terraform Module Registry
- 5b)	Interact with module inputs and outputs
- 5c)	Describe variable scope within modules/child modules
- 5d)	Set module version

## Exam Objectives / Testing

<details>
<summary>Contrast and use different module source options including the public Terraform Module Registry</summary>

- Nested list
  - with sub-items
</details>

<details>
<summary>Interact with module inputs and outputs</summary>

- Nested list
  - with sub-items
</details>

<details>
<summary>Describe variable scope within modules/child modules</summary>

- Nested list
  - with sub-items
</details>

<details>
<summary>Set module version</summary>

- Nested list
  - with sub-items
</details>