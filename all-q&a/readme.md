```
| Component        | Purpose                | Example              |
| ---------------- | ---------------------- | -------------------- |
| Entra ID         | Identity & access      | Users, groups, login |
| Management Group | Organize subscriptions | Prod / Dev hierarchy |
| Subscription     | Billing & resources    | VM, Storage, AKS     |
```

<img width="1636" height="922" alt="image" src="https://github.com/user-attachments/assets/a6a6fe38-9846-4e1b-abbb-41874cf33df6" />


### 1. Azure Landing Zone Questions
   
Questions

### What is an Azure Landing Zone?
```
An Azure Landing Zone is a pre-configured Azure environment that provides a secure and standardized foundation for deploying applications and workloads.
It includes:
Identity and access management
Networking setup
Security policies
Monitoring
Governance rules
Resource organization
The goal is to help teams deploy resources in Azure consistently, securely, and according to company standards without setting everything up from scratch every time.
For example, when a new project team wants to use Azure, the landing zone already provides:
A subscription structure
RBAC access
VNet connectivity
Security policies
Logging and monitoring
CI/CD standards
So teams can start deploying quickly while remaining compliant with enterprise governance.
```

How do you design enterprise-scale landing zones?
```
I design enterprise-scale Azure landing zones by creating a secure, scalable, and standardized foundation for all teams and applications.
First, I organize the environment using Management Groups and separate subscriptions for production, non-production, and shared services.
Then I implement:
Centralized identity management using Microsoft Entra ID
Hub-and-spoke networking for secure connectivity
Azure Policies for governance and compliance
RBAC for controlled access
Centralized monitoring and logging
Standard tagging for cost management and ownership

I also use Infrastructure as Code like Bicep and Azure DevOps pipelines so the landing zone can be deployed consistently and automatically.
The main goal is to provide teams with a ready-to-use Azure environment that is secure, compliant, and easy to scale across the organization.
```

Difference between subscription, management group, and tenant?
```
You can explain it like this in a simple interview-friendly way:
Tenant is the top-level Azure identity environment.
It represents the organization and contains users, groups, applications, and Microsoft Entra ID.
Management Group is used to organize multiple subscriptions together.
It helps apply governance, policies, and access controls across many subscriptions centrally.
Subscription is where actual Azure resources are created and billed.
It acts as a logical container for resources like VMs, AKS, databases, and storage accounts.

Simple hierarchy:
Tenant
   └── Management Groups
           └── Subscriptions
                   └── Resources

Example:
Tenant = Entire company
Management Group = Production / Non-Production / Business Units
Subscription = Individual projects or applications
So:
Tenant manages identity
Management Group manages governance
Subscription manages resources and billing
```

How do you structure management groups?
```
I structure Management Groups based on organization, environment, and governance requirements so policies and access can be managed centrally.

Usually, I create a hierarchy like this:

Tenant Root
   ├── Platform
   │      ├── Shared Services
   │      └── Connectivity
   │
   ├── Production
   │      ├── Business Unit A
   │      └── Business Unit B
   │
   └── Non-Production
          ├── Dev
          ├── Test
          └── Sandbox

Then I apply:

Security policies at higher levels
Environment-specific controls at lower levels
RBAC based on team ownership
Budget and compliance policies per business unit

This approach helps maintain:

Central governance
Security consistency
Easy scaling
Better cost management
Clear separation between production and non-production workloads.
```

How do you separate prod/non-prod?
```
I separate production and non-production environments using separate subscriptions and management groups to improve security, governance, and cost control.

For example:

Management Group
   ├── Production Subscriptions
   └── Non-Production Subscriptions

Then I apply:

Stricter security and policies for production
Different RBAC access levels
Separate VNets and resources
Different monitoring and backup rules
Separate budgets and cost tracking

Non-production environments like Dev and Test usually allow more flexibility, while production is tightly controlled with approval processes and stricter compliance.

This separation reduces risk and prevents development activities from impacting live production workloads.
```

How do you enforce governance across subscriptions?
```
I enforce governance across subscriptions mainly using Management Groups, Azure Policy, RBAC, and standardized deployment processes.

First, I organize subscriptions under Management Groups so governance can be applied centrally.

Then I use Azure Policy to enforce standards such as:

Mandatory tagging
Allowed Azure regions
Approved VM sizes
Denying public IPs
Enabling diagnostic logs

I also use RBAC to control who can create or modify resources.

For consistency, all infrastructure is deployed using Bicep and Azure DevOps pipelines, so teams follow approved deployment patterns instead of creating resources manually.

This helps maintain security, compliance, cost control, and operational consistency across all subscriptions.
```

How do you onboard new applications securely?
```
I onboard new applications securely by using standardized landing zones, automated deployments, and predefined security controls.

First, the application is deployed into the correct subscription and network based on the environment such as Dev, Test, or Production.

Then I apply:

RBAC for controlled access
Azure Policies for compliance
Private networking and NSGs
Managed identities instead of hardcoded secrets
Key Vault for secret management
Centralized logging and monitoring

All infrastructure is deployed using Bicep and Azure DevOps pipelines so configurations remain consistent and secure.

Before production deployment, security and compliance checks are validated to ensure the application follows enterprise standards.
```

### 2. Azure Governance Questions

Question

How do you enforce tagging standards?
```
“I enforce tagging standards in Azure mainly using Azure Policy.

First, I define mandatory tags such as Environment, Owner, Cost Center, and Application Name. Then I apply Azure Policies at the Management Group or Subscription level to ensure all resources follow the standard.

I use:

* **Deny policies** to block resources without required tags,
* **Inherit/Append policies** to auto-apply tags,
* **Remediation tasks** to fix existing non-compliant resources.

This helps with governance, cost tracking, compliance, and resource management across the organization.”
```

How do you prevent public IP creation?
```
“To prevent public IP creation in Azure, I use Azure Policy at the Management Group or Subscription level.

I create a policy that denies the creation of Public IP resources or prevents NICs/VMs from associating with public IPs. This ensures workloads remain private and follow security standards.

For existing environments, I also use:

* NSGs and private networking,
* Azure Firewall or Bastion for secure access,
* Remediation tasks to identify and fix non-compliant resources.

This approach helps enforce secure network governance across the organization.”
```

How do you restrict regions?
```
“To restrict regions in Azure, I use Azure Policy at the Management Group or Subscription level.

I create a policy that allows resource deployment only in approved Azure regions, such as Central India or East US, and denies deployments in unauthorized regions.

This helps with:

* Compliance requirements
* Data residency
* Cost optimization
* Governance standardization

In enterprise environments, region restriction policies are usually implemented as part of the Azure Landing Zone governance model.”
```

What is Azure Policy?
```
“Azure Policy is a governance service in [Microsoft Azure](https://azure.microsoft.com/?utm_source=chatgpt.com) used to enforce organizational standards and compliance across Azure resources.

It helps control how resources are created and configured by evaluating resources against defined rules.

Using Azure Policy, we can:

* Enforce tagging standards
* Restrict Azure regions
* Prevent public IP creation
* Enforce specific VM SKUs
* Ensure security and compliance requirements

Policies can be assigned at:

* Management Group
* Subscription
* Resource Group

Common policy effects include:

* Deny
* Audit
* Append
* Modify
* DeployIfNotExists

In short:

> Azure Policy helps automate governance and compliance in Azure environments.”

```

Difference between Azure Policy and RBAC?
```
| Azure Policy                                              | RBAC (Role-Based Access Control)           |
| --------------------------------------------------------- | ------------------------------------------ |
| Used for governance and compliance                        | Used for access management                 |
| Controls **what can be created/configured**               | Controls **who can access resources**      |
| Enforces standards on resources                           | Assigns permissions to users/groups        |
| Works on resource properties                              | Works on user roles and actions            |
| Example: Restrict regions, enforce tags, block public IPs | Example: Contributor, Reader, Owner access |
| Uses policy effects like Deny, Audit, Modify              | Uses built-in/custom roles                 |
| Focuses on resource compliance                            | Focuses on authorization                   |

```
What are initiatives in Azure Policy?
```
“An Initiative in Azure Policy is a collection of multiple policies grouped together and managed as a single unit.

It helps apply and manage governance standards more efficiently across Azure environments.

For example, instead of assigning separate policies for:

* Mandatory tags
* Allowed regions
* No public IPs
* Approved VM SKUs

we can group them into one Initiative called:

text id="2qk0ec"
Enterprise Governance Baseline

Benefits of Initiatives:

* Centralized policy management
* Easier compliance tracking
* Simplified assignments
* Better governance at scale

Initiatives are commonly used in Azure Landing Zones and enterprise environments to enforce organization-wide standards.”

```

How do you implement policy-as-code?

### 3. Identity & Security Questions


Question

What is Microsoft Entra ID?
```
“[Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/whatis?utm_source=chatgpt.com) (previously Azure Active Directory) is Microsoft’s cloud-based identity and access management service.

It is used to:

* Manage users and groups
* Authenticate users
* Provide Single Sign-On (SSO)
* Control access to Azure resources and applications
* Enable security features like MFA and Conditional Access

In Azure, Entra ID works with RBAC to control who can access resources and what actions they can perform.

In simple terms:

> Microsoft Entra ID manages identities and access in Azure and Microsoft cloud services.”

```

Difference between RBAC and Entra roles?

How do you implement least privilege?

What is PIM?

What is Conditional Access?

How do you implement Zero Trust?

How do managed identities work?

How do you secure AKS?

How do you manage secrets?


### 4. Azure Networking Questions

Questions

Explain hub-and-spoke architecture

What is Azure Firewall?

Difference between NSG and Firewall?

What is VNet peering?

ExpressRoute vs VPN Gateway?

How do you secure inbound traffic?

How do private endpoints work?

How do you design hybrid networking?


### 5. AKS Questions

Questions

How do you design enterprise AKS?

How do you secure AKS?

How do you implement ingress?

How do you manage secrets?

How do you monitor AKS?

Difference between node pools?

How do you optimize AKS costs?

How do you handle upgrades?


### 6. Infrastructure as Code (Bicep)

Why Bicep over ARM?

How do modules work?

How do you structure reusable templates?

How do you manage environments?

How do you handle secrets?

How do you implement CI/CD for IaC?

### 7. Azure DevOps / CI-CD Questions

Questions

How do you standardize pipelines?

How do you implement GitOps?

How do you manage releases?

How do approvals work?

How do you separate infra and app pipelines?

Blue-green vs canary deployments?

### 8. FinOps Questions

Questions

How do you implement cost allocation?

What tagging standards do you use?

How do you forecast Azure costs?

How do you reduce AKS costs?

What are Reserved Instances/Savings Plans?

How do you detect unused resources?

### 9. Monitoring & Observability Questions

Questions

What monitoring stack do you use?

How do you implement centralized logging?

Difference between metrics and logs?

What are SLOs/SLIs?

How do you reduce MTTR?

### 10. ServiceNow / CMDB / ITSM Questions

Questions

What is CMDB?

How do you sync Azure inventory to CMDB?

How do you integrate Azure with ServiceNow?

What is change management?

How do you automate change approvals?

### 11. Scenario-Based Architecture Questions

### Design a secure multi-subscription Azure platform for 100 teams.
```
Expected discussion:

Landing zones
Management groups
Policies
Hub-spoke
RBAC
Monitoring
CI/CD
Cost management
```
### A team deployed resources violating governance policies. What do you do?
```
Expected:

Azure Policy deny/audit
Exceptions process
CI/CD validation
Platform guardrails
```

### AKS costs increased by 300%. How do you troubleshoot?
```
Expected:

Analyze node utilization
HPA/VPA
Spot nodes
Rightsizing
Logging
Kubecost/Azure Monitor
```

### 12. Leadership Questions

Questions

How do you drive cloud adoption?

How do you influence engineering teams?

How do you handle resistance to governance?

How do you train teams?

How do you balance security vs developer velocity?

### Questions You Should Ask Them

How mature is the Azure platform today?

Are landing zones already implemented?

Is AKS centrally managed?

What governance tooling is used?

How is FinOps handled currently?

What are the biggest platform challenges today?

How large is the Azure estate?
