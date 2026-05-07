# 🚀 Infrastructure Engineering Project - Group F

Welcome to the GitHub Organization for **Group F**'s Infrastructure Engineering project. This organization hosts the complete platform implementation based on Kubernetes, GitOps, and Infrastructure as Code (IaC) principles.

---

## 🛠️ Project Repositories

Below you will find the core components of our platform. Each repository contains its own specific documentation and implementation details.

| Repository | Description | Documentation |
| :--- | :--- | :--- |
| [**📁 infrastructure**](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure) | Core Kubernetes infrastructure and cloud resources (IaC). | [📖 README](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure/blob/main/README.md) |
| [**📁 gitops**](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops) | GitOps configurations and application deployments. | [📖 README](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/blob/main/README.md) |
| [**📁 backend**](https://github.com/Infrastructure-Engineering-PT-Group-F/backend) | 3-tier application backend (REST API). | [📖 README](https://github.com/Infrastructure-Engineering-PT-Group-F/backend/blob/main/README.md) |
| [**📁 frontend**](https://github.com/Infrastructure-Engineering-PT-Group-F/frontend) | 3-tier application frontend (SPA). | [📖 README](https://github.com/Infrastructure-Engineering-PT-Group-F/frontend/blob/main/README.md) |

---

## 📋 Assignment Details

Below is the transcribed content of the original assignment guidance.

<details>
<summary><b>Click to expand Assignment Text</b></summary>

For the assignment, you will implement a platform based on Kubernetes.
This document serves as the overall guidance and grading explanation. Please understand the expectations and how your grades will be calculated.

### Expectations
Based on the platform you are developing and maintaining, you must show understanding and apply best practices related to the practices taught in the lectures.

You are responsible for the documentation of your platform (and, therefore, project), which needs to reside in your GitHub repositories (README, docs folder, etc.).

You must use well described GitHub issues to outline your work and rely on pull request for any changes, with both serving as part of your documentation and audit trail.

Wherever possible and feasible you must implement GitHub Actions pipelines to validate changes (e.g. linting Kubernetes manifests), and you are required to follow security best practices throughout the assignment.

After kicking off the provisioning of the infrastructure with Infrastructure as Code (IaC) the entire platform needs to be deployed without a single click (exceptions possible).

The assignment will be concluded by a presentation and demo.

### Components
The platform must consist of, at least, the following components:
* Kubernetes infrastructure deployed using Infrastructure as Code (IaC)
* applications deployed using GitOps principles
* secrets management
* DNS management
* HTTPS endpoints incl. publicly valid SSL certificates
* security (multi-tenancy, network separation, resource management, …)
* provisioning of “SaaS” applications (3-tier, instance-based multi-tenancy) through GitOps and Crossplane
* bonus task: basic monitoring

### Kubernetes
It is highly recommended to leverage the managed Kubernetes services in Google Cloud. You can also self-manage Kubernetes on a public cloud provider with a distribution of your liking if all endpoints are publicly available. The cloud provider must support the IaC tool.

For managed clusters, you must use the cloud provider’s storage solutions. You can choose the monitoring tool used with the recommendation to leverage cloud provider solutions if your cluster is managed. You must provide the lecturer access (cluster-admin) to your cluster.

### Capacity & Cost Planning and Management
In the beginning, you are required to perform capacity planning and document your choices as well as its associated cost planning in a GitHub issue.
The goal is to increase the usage of nodes while still being able to scale applications fast when required and keeping the costs low.
You should aim to keep the number of worker nodes low but highly available and cost effective. If you self-manage a cluster, it is permitted to only use one node as the control plane and no workloads are allowed to run on the control plane.
Your cluster can also be zonal only to reduce additional cloud costs.
You are expected to present your capacity and cost planning and compare it to the actual costs incurred. The actual costs must be logged (with screenshots, invoices, etc.) in the capacity planning GitHub issue.
After you have estimated the costs, you are required to get in touch with the lecturer and Igor Ivkic by e-mail asking for the required number of credits. Please refer to the corresponding GitHub issue and be as specific as possible with your explanations.

### IaC
You are required to either use Terraform / OpenTofu or Pulumi as the IaC tool.
IaC code must be stored in its own public GitHub repository.

### GitOps
You can choose to use either ArgoCD or Flux as the GitOps tool.
You are free to use any plugins and/or add-ons useful to achieve the goals of the project.
GitOps “code” must be stored in its own public GitHub repository.

### DNS
You must leverage tooling such as ExternalDNS.
You need to provide a domain name which you can use with all required tools.
If this is impossible for anyone in your group, please contact the lecturer as soon as possible. You will still need to provide a nameserver which is supported by ExternalDNS and cert-manager!

### Secrets Management
You must leverage tooling such as the External Secrets Operator (ESO).
You can rely on managed cloud services to provide secrets management or self-host Hashicorp Vault or OpenBao (take care that this is done through IaC!).
In the self-hosted case, you can choose to host the required IaC code in its own public GitHub repository or combine it with the cluster IaC code.
You must not store any hard-coded and/or plaintext secrets anywhere. All secrets must be encrypted and automatically generated.
Secrets used in pipelines, e.g. to run IaC, need to be limited and options like OIDC authentication are to be preferred.
You can manually store secrets in your secrets management platform if this secret cannot be auto generated or requires a complex setup.

### SSL Certificates
You must use tools such as cert-manager to issue SSL certificates through ACME for your domain name. It is recommended to use the DNS-01 challenge.

### Crossplane
Instances of your “SaaS” application must be deployed using Crossplane (CRD, Composition, …). Each tenant gets their own isolated instance of the same application, deployed into its own namespace.
You must use Crossplane to create any resources required for the application to work, and create the “glue” between the components, like a database.
Crossplane can, in the background, leverage your GitOps tools, if required.

### Container Registry
To store the container images of your application, you can use any registry. Please take care that the frontend image must only be privately accessible and the backend one can be public.
The probably easiest approach is to leverage the GitHub Container Registry (GHCR).
Bonus points can be awarded to host the registry in the cluster.
In this case, it is apparent that a redeploy of the infrastructure/cluster will cause the deployment of the application instance to fail! Manual triggering the container image build and reconciliation after a cluster redeploy is acceptable and will not affect grading.
Additionally, you can experiment in resolving this “chicken & egg problem” or hosting the registry outside of the cluster (take care of IaC!).

### The Application
You can choose any 3-tier application which consists of a data layer (= a database), a backend (= a REST API), and a frontend (= a single-page application).
The code must be stored in separate GitHub repositories and container images must be published to the container registry. The repository for the backend can be public whereas the frontend must be private.

To deploy the database, you need to use a scalable option. You could, for example, use a
cloud provider’s service (take care of costs, especially with scale) or use tools like
CloudNativePG to deploy and manage Postgres databases. It is inherently important that
database upgrades are automated.

### Bonus
You can earn bonus points by adding the following features to your platform:
1. continuous delivery and/or rollout of applications (e.g., via Argo Rollouts or Kargo)
2. automated on-the-fly builds of the frontend with deployment to either a Google Cloud Storage Bucket (HTTP) or an AWS S3 Bucket (HTTPS) with website hosting and storing the URL in the custom component
3. effective enhancement of your security posture with Kyverno and providing regular reports
4. basic monitoring

### Day 1 / Day 2
To maintain clarity and prevent overengineering, distinguish between these two phases:

**Day 1: Foundation (Bootstrap)**
At the end of this step the platform exists.
* Scope: Provisioning the core cluster environment and management stack.
* Tooling: Use IaC (Terraform/Pulumi) to build the VPC, GKE cluster, and install/initialize the GitOps tool.
* Identity: Create the Platform Service Accounts and OIDC/Workload Identity trust required for the providers to function.

**Day 2: Service Catalog (Application)**
Day 2 includes everything to keep the platform running (operations) and use it by the various application owners and teams for which it is catered towards.
* Scope: Automated, on-the-fly provisioning for tenant-specific application instances.
* Tooling: Use Crossplane to orchestrate "SaaS" resources like databases and application-level identities.
* Workflow: A developer triggers a deployment via GitOps, which Crossplane translates into cloud infrastructure.

## Grading Criteria
1. documentation & software management hygiene (15.00%)
2. infrastructure bootstrap (35.00%)
3. application management (35.00%)
4. the presentation (15.00%)

To pass the course, you must pass all blocks and receive a passing grade over all blocks.
The rest of this chapter explains the grading criteria of each section, including their weight in
your final grade. The weighting of each pillar is shown in every section. The final grade
calculation is shown afterward.


### Documentation & Software Management Hygiene (15.00%)

#### Commit & Pull Requests
All Git commit messages must follow the Conventional Commits specification and do not
contain any merge commits.

All changes must be merged into any main branch through a (verified) pull request.

Every commit must refer to and optionally close a GitHub issue (where useful).

#### Documentation
The expectation is to draft a GitHub issue for every change that needs to be made.

The goals are to make it clear what the scope of the work is and how it links to the overall
project context and the platform. Please keep it short and precise.

The repositories must contain a documentation, and the reader needs to understand the
project’s scope and status, how to use it, where the endpoints and related repositories are
located, and how to contribute to it (e.g. adding a new application instance).
Obviously, this documentation can be distributed across the involved repositories with one
“main” repository serving as the entry point for the reader. Please keep it short, precise and
focused on the critical parts of your project.

#### Pipeline
Wherever possible and feasible you must implement GitHub Actions pipelines to validate
changes (e.g. linting Kubernetes manifests). For every pull request, it must be ensured (in
the best possible but not overengineered way) that the merged code is, at least, syntactically
correct.

#### Capacity & Cost Management
Referring to the requirements, this part grades your initial capacity and cost planning and the
comparison against the real values.

It is expected that your planning does not significantly differ from the real values; otherwise,
you must provide a root cause analysis and the learnings derived from that.

### Infrastructure Bootstrap (35.00%)

#### Infrastructure as Code (IaC)
Every required piece of infrastructure for the cluster and platform, even service accounts or
similar, must be created/provisioned through IaC. It is recommended to leverage workload
identities where possible to facilitate secure access for both platform components (e.g.,
Crossplane) and tenant applications.

You are not allowed to perform any click after the IaC tool was kicked off for the platform to
be deployed.

Exceptions are limited to glue points between infrastructure components, e.g. varying
connection data. However, these exceptions must be limited to as little as possible and
require a short description in the documentation.

#### Secret Management
Secrets are not to be stored plaintext anywhere!
You are required to use tooling which limits the usage of plaintext and hard-coded
credentials.

Keep in mind that all your repositories are public!

#### GitOps
You are required to use GitOps to deploy any application or resources to your cluster.

If available, Helm charts must be used instead of plain Kubernetes manifests.

The required credentials, configuration, and else must be provided securely.
Keep in mind that all your repositories are public!

#### DNS & TLS Management
You are required to provide publicly accessible HTTPS endpoints which are secured through
publicly valid SSL certificates (e.g. using ACME).

Any creation of DNS entries and SSL certificates must be automated through your platform.

### Application Management (35.00%)

#### Secrets Management
Secrets are not to be stored plaintext anywhere!
You are required to use tooling which limits the usage of plaintext and hard-coded
credentials.

If secrets must be provided from the “customer”, you can decide how and where to handle
this. It is permitted to use these as either encrypted or plain-text credentials unless they are
a potential attack vector compromising your entire platform.

Keep in mind that all your repositories are public!

#### Infrastructure Provisioning
Any required infrastructure, configuration, secrets, and else must be provisioned “on the fly”
through Crossplane.

#### Application Deployment
The application needs to be setup through GitOps and Crossplane.

The goal is to define/create a new tenant through GitOps providing basic tenant
configuration and for Crossplane to handle all other deployment steps. Crossplane, however,
can interact with your GitOps tool in support to provisioning infrastructure or deployments.

Bonus points can be awarded if your application internally uses a Helm chart as its
deployment method, abstracted through Crossplane to the user.

#### Application Updates
Updates must be rolled out to all tenants with a single change/click.

However, you must have the ability to test a new application version using a “staging
instance” of the application (= a staging tenant).

#### Multi-Tenancy
Since the application has one instance per tenant, you must ensure proper encapsulation
using multi-tenancy approaches. This includes, for example, network policies and proper
resource management. For this assignment, soft multi-tenancy is sufficient and it is
encouraged to not overengineer this requirement.

#### Monitoring (Bonus Task)
The application must be monitored in terms of resource consumption and healthiness.
An application owner must be able to see these metrics in a simplified and easy way. The
platform administrator needs to be able to understand healthiness and overall platform
consumption.

### Presentation (15.00%)
The presentation should showcase your platform and architecture and must not be longer
than 20 minutes.

You are expected to:
- show an overview of your capacity & cost planning and compare it to the real values
- demo creating a new tenant and explaining the background processes (show code!)
- forecast an outlook on scaling the platform to hundreds or thousands of users

Additionally, pick one of the following topics:
- show the application health and resources monitoring page
- explain the infrastructure bootstrapping process (show code!)
- multi-tenancy and security

This pillar is an exception to the required equal distribution of work.
Therefore, this pillar’s grade is applied to all team members.

## Deadline
The submission deadline is the 2026/06/26 14:00 CEST.
No changes are permitted afterward.

## Notes
### Generative AI Tools
It is explicitly expected for you to leverage generative AI tools.
The following remarks must be observed:
- Treat any outcome of such tools with caution, apply your judgment, and use it as an
inspiration for performing your work or supporting you in troubleshooting issues.
- Include your evaluation and usage of the tools.

### Code of Conduct / Plagiarism
As always, you must follow the Hochschule Burgenland code of conduct.

If plagiarism is detected across groups or to reference repositories, the affected pillar(s) will
be graded with 0 points. This also applies to Generative AI areas without any reference.

### Announcements
Derivations of the assignment or any important announcements will be made through
Moodle and in the following lecture.

Derivations for specific parts will be mentioned in the assignment document accordingly.

</details>

---
Generated by Antigravity with gemini-3-flash