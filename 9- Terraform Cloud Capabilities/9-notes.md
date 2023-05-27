# Terraform Cloud Capabilities

## Reading

[What is Terraform Cloud?](https://developer.hashicorp.com/terraform/cloud-docs)  
[Terraform Workflow](https://developer.hashicorp.com/terraform/cloud-docs/overview#terraform-workflow)
[Workspaces](https://developer.hashicorp.com/terraform/cloud-docs/workspaces)
[Private Registry](https://developer.hashicorp.com/terraform/cloud-docs/registry)
[Teams](https://developer.hashicorp.com/terraform/cloud-docs/users-teams-organizations/teams)
[Sentinel](https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/sentinel)

## Notes

### **Terraform Cloud**

*Terraform Cloud* is an application that helps teams use Terraform together. It provides solutions for the pain points of using Terraform, such as remote state, resource drift, access control, secrets and more.

Terraform Cloud offers a generous free tier, including the use of workspaces.

#### **Workflow**

When more than one person is working on a Terraform project, you need at minimum to have a remote state solution, and ideally also a CI environment. Terraform Cloud can handle this for you. Terraform Cloud offers *Terraform Cloud Agents* that will run Terraform on your own isolated, private, or on-premises infrastructure, or they can provide cloud services for "remote operations".

#### **Workspaces**

When working in a corporate workplace, it's natural that you will have many collections of Terraform configurations for different environments. This is usually handled by having separate directories for each environment in your configuration.

Terraform Cloud manages infrastructure collections with *workspaces* instead of directories.

| Component               | Local Terraform                                               | Terraform Cloud                                                            |
| ----------------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Terraform configuration | On disk                                                       | In linked version control repository, or periodically uploaded via API/CLI |
| Variable values         | As `.tfvars` files, as CLI arguments, or in shell environment | In workspace                                                               |
| State                   | On disk or in remote backend                                  | In workspace                                                               |
| Credentials and secrets | In shell environment or entered at prompts                    | In workspace, stored as sensitive variables                                |

To switch workspaces in Terraform, you run the `terraform workspace select <workspace_name>` command. Terraform will not create a new workspace when this is run. To create a new workspace, you must run `terraform workspace new <workspace_name>`.

#### **Private Registry**

Terraform Cloud's *private registry* works similarly to the public Terraform Registry and helps you share Terraform providers and Terraform modules across your organization.Private providers and private modules are hosted on an organization's private registry and are only available to members of that organization.

#### **Teams**

*Teams* are groups of Terraform Cloud users within an organization. If a user belongs to at least one team in an organization, they are considered a member of that organization.

The organization can grant *workspace* permissions to teams that allow its members to start Terraform runs, create workspace variables, read and write state, etc

#### **Sentinel**

Policies are rules that Terraform Cloud enforces on runs. You use the *Sentinel* policy language to define Sentinel policies. After you define policies, you must add them to policy sets that Terraform Cloud can enforce on workspaces.

## Exam Objectives / Testing

<details>
<summary>Explain how Terraform Cloud helps to manage infrastructure</summary>

- Terraform cloud provides streamlined solutions for the pain points of setting up a Terraform platform in a corporate environment
- Remote state, secrets, a CI environment are all provided as a service to consume
</details>

<details>
<summary>Describe how Terraform Cloud enables collaboration and governance</summary>

- With *sentinel* and *teams*, you can govern who has access to run what, creating a more secure Terraform configuration
- Remote state, secrets, a CI environment are all provided as a service to consume, which are essential for collaboration
</details>