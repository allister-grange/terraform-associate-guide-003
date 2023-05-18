# Terraform Basics - Spaced Repetition (Anki) Cards


What do providers supply Terraform? The resource types and data sources that Terraform can manage

In Terraform, for a commonly used provider (like AWS), what is the source? The Terraform Registry

Where must providers be specified to be used in Terraform? In the required_providers block

What 3 things does a required_providers block specify?

{{c1::local name}}
{{c2::source}}
{{c3::version}}

What do you provide to a provider block in Terraform for unique identification when you have two or more of them? An alias

When using a provider that looks like this, how would you access it in a recourse block?

provider "aws" {
  alias  = "west"
  region = "us-west-2"
}

provider = aws.west

What is used to uniquely identify where you download a provider from? Source addresses

What are the three building blocks of source addresses for providers? {{c1::hostname}}/{{c2::namespace}}/{{c3::type}}

When does Terraform validate your providers? When running `terraform init`

How does Terraform enable developers to extend it's functionality? Through plugins

When run, what will the `terraform init` command produce? A version locking file

To install a provider in Terraform, what block and resource do you need? A `required_providers` block and a `provider` resource

What are providers and provisioners both considered by Terraform? Plugins
