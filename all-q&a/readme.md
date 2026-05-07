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

How do you structure management groups?

How do you separate prod/non-prod?

How do you enforce governance across subscriptions?

How do you onboard new applications securely?


### 2. Azure Governance Questions

Question

How do you enforce tagging standards?

How do you prevent public IP creation?

How do you restrict regions?

What is Azure Policy?

Difference between Azure Policy and RBAC?

What are initiatives in Azure Policy?

How do you implement policy-as-code?

### 3. Identity & Security Questions


Question

What is Microsoft Entra ID?

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
