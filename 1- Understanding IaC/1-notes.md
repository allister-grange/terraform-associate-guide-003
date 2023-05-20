# Understanding IaC

## Reading

[Infrastructure as Code: What Is It? Why Is It Important?](https://www.hashicorp.com/resources/what-is-infrastructure-as-code)

## Notes

**The problem**

Standing up infrastructure in a traditional datacenter where you process work through tickets is slow, inconsistent and hard to scale. 

**The solution - IaC**

How do we take the process of 'ClickOps' for standing up infrastructure and codify the process? We do this through **IaC**.

**IaC** is a practise that enables the creation of infrastructure and services using declarative configuration files. This allows for a consistent and scalable environment that is fully automated and tracked through version control.

## Exam Objectives / Testing

<details>
<summary>Explain what IaC is</summary>

- The practice of managing and provisioning infrastructure resources using code
</details>

<details>
<summary>Describe advantages of IaC patterns</summary>

- Automation
  - The click heavy process of standing up infrastructure can now be codified into configuration file, saving large amounts of time 
- Consistency
  - Our infrastructure should be consistent as we're using an idempotent process to stand it up
- Scalability
  - Traditional datacenters with hypervisors had limited scale by nature their manual processes 
- Version control
  - Who changed what
  - Transparency of documentation
  - Tracking the changes of the infrastructure over time
</details>