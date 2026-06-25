# Repository Overview and Ownership

The purpose, visibility, ownership and assignment mapping of every repository in
the Group F organization. This is the detailed companion to the
[organization landing page](https://github.com/Infrastructure-Engineering-PT-Group-F/.github/blob/main/profile/README.md).

## Ownership at a glance

| Repository                                                                                  | Visibility | Lead                                  | Assignment area                          |
| :------------------------------------------------------------------------------------------ | :--------- | :------------------------------------ | :--------------------------------------- |
| [`infrastructure`](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure) | public     | Ajdin (`@ajdinvelic11`)               | Infrastructure Bootstrap                 |
| [`gitops`](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops)                 | public     | Ralf (`@R41f-K`), Max (`@2510781020`) | GitOps, Application Management, Security |
| [`backend`](https://github.com/Infrastructure-Engineering-PT-Group-F/backend)               | public     | Julian (`@hochschule-jz`)             | Application Management                   |
| [`frontend`](https://github.com/Infrastructure-Engineering-PT-Group-F/frontend)             | private    | Julian (`@hochschule-jz`)             | Application Management                   |
| [`.github`](https://github.com/Infrastructure-Engineering-PT-Group-F/.github)               | public     | Max (`@2510781020`)                   | Documentation & Hygiene                  |

The `frontend` repository is private because the assignment requires the
frontend container image to be privately accessible. All other repositories are
public.

## Repository details

### `infrastructure`

- **Purpose:** Provisions the GCP foundation and the platform management plane
  with Terraform
- **Typical contents:** Terraform root modules (`bootstrap/` and `platform/`),
  the VPC and GKE cluster, IAM and Workload Identity, Secret Manager resources,
  the ArgoCD bootstrap and the access and permission model documentation

### `gitops`

- **Purpose:** The declarative source of truth that ArgoCD reconciles onto the
  cluster, including the Crossplane service catalog and the per-tenant resources
- **Typical contents:** ArgoCD `Application` resources under `platform/`,
  Crossplane XRDs and Compositions under `catalog/`, per-tenant composite
  resources under `tenants/` and the security and secret-handling documentation

### `backend`

- **Purpose:** The Weather App REST API, published as a Helm chart and a public
  container image
- **Typical contents:** The Spring Boot service, its Helm chart, the Dockerfile,
  the OpenAPI specification, the release-please configuration and the CI
  workflows

### `frontend`

- **Purpose:** The Weather App single-page application, published as a private
  container image
- **Typical contents:** The Vite single-page application, the runtime
  configuration entrypoint, its Helm chart, the Dockerfile and the CI workflows

### `.github`

- **Purpose:** The organization entry point and shared GitHub configuration
- **Typical contents:** The organization profile README, the shared issue and
  pull request templates, the contribution workflow and cross-repository
  documentation

## Where to create issues

Create each issue in the repository where the main change will happen. A
Terraform change belongs in `infrastructure`, a tenant or ArgoCD change in
`gitops`, a backend API change in `backend`, a frontend change in `frontend` and
organization-level documentation in `.github`.

## Tracking cross-repository work

Some changes touch more than one repository. A new platform capability, for
example, can need an IAM grant in `infrastructure` and a consuming resource in
`gitops`. In that case open one issue in each affected repository where its
change lands and link the related issues and pull requests to each other by
their full URL. Track overall progress from the issue in the leading repository,
meaning the one that owns the outcome.
