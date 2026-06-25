# Final Demo Storyline: Monitoring Deep Dive

This outline prepares the 20-minute final presentation and demo for the Group F
Infrastructure Engineering project with the application health and resource
monitoring page as the selected deep-dive topic.

## Selected deep dive

**Application health and resource monitoring** is the selected deep-dive topic.

This topic connects directly to the tenant demo and lets the team show how an
application owner and platform administrator can check whether a tenant instance
is healthy and how much CPU, memory and platform capacity it consumes. Capacity
and cost planning is still covered as a required presentation topic, but it is
not the optional deep dive.

## Presentation flow

| Time | Section | Speaker | Main points |
| :--- | :--- | :--- | :--- |
| 0:00-1:00 | Opening and project goal | Max | Explain the platform goal: a GitOps-driven Kubernetes platform for tenant-specific weather app instances. |
| 1:00-4:00 | Platform and architecture overview | Ralf | Show the repository split, GKE foundation, ArgoCD, Crossplane, External Secrets Operator, cert-manager, Gateway API, backend, frontend and tenant namespace flow. |
| 4:00-6:30 | Capacity and cost planning vs actuals | Ajdin | Summarize the initial GCP estimate, actual cost evidence and the reason for any meaningful deviation. |
| 6:30-12:30 | Live demo: create a tenant | Julian and Ralf | Show the tenant declaration change, explain what ArgoCD reconciles, what Crossplane creates, how secrets are delivered and how the frontend/backend/database become reachable. |
| 12:30-16:30 | Deep dive: application health and resource monitoring | Ralf and Max | Show the monitoring page, explain the tenant health signals, resource consumption view, platform-level capacity indicators and how the dashboard supports operations. |
| 16:30-18:30 | Scaling outlook | Julian | Explain what changes when scaling to hundreds or thousands of tenants: GitOps structure, Crossplane composition reuse, database scaling, release rollout strategy, cost controls and observability. |
| 18:30-20:00 | Wrap-up and questions | Max | Recap assignment requirements, current status, known limitations and next improvements. |

## Demo flow

1. Start from the organization profile and repository overview to show where
   each responsibility lives.
2. Open the `gitops` tenant declaration area and show the minimal tenant input.
3. Create or review a tenant change that represents a new weather app instance.
4. Explain the reconciliation path:
   `gitops` commit or pull request -> ArgoCD Application -> Crossplane tenant
   composite -> namespace, database binding, application Helm releases,
   ExternalSecret resources and HTTPRoute.
5. Show the resulting tenant namespace resources and application endpoint.
6. Show one code view during the demo, preferably the tenant claim or
   composition, to satisfy the assignment requirement to show code.
7. Confirm the staging tenant or validation checklist used before rolling out
   application updates to all tenants.

## Demo fallback

- Keep a pre-created tenant ready in case live reconciliation takes too long.
- Keep terminal output or screenshots for ArgoCD sync status, Crossplane
  resource status and the public HTTPS endpoint.
- If the Gateway or certificate stack is still settling, explain the intended
  reconciliation chain and use the latest successful tenant evidence.
- If private frontend image pull validation is not live, show the documented
  tenant image-pull Secret contract and the related frontend issue.
- If the monitoring page is not live, show the latest screenshots or manifests
  behind the monitoring approach and explain which health and resource signals
  are expected.
- If cost evidence is incomplete, clearly mark the missing data and link the
  open tracking issue instead of guessing values.

## Current preparation context

This context was checked on 2026-06-25 and should be refreshed before the final
presentation.

| Repository | Relevant state for the storyline |
| :--- | :--- |
| `.github` | Issue [#5](https://github.com/Infrastructure-Engineering-PT-Group-F/.github/issues/5) tracks this storyline. Issue [#8](https://github.com/Infrastructure-Engineering-PT-Group-F/.github/issues/8) tracks generative AI usage documentation. |
| `infrastructure` | Issue [#14](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure/issues/14) tracks the initial GCP capacity and cost estimate. Issues [#6](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure/issues/6) and [#12](https://github.com/Infrastructure-Engineering-PT-Group-F/infrastructure/issues/12) track cost monitoring and AI tool documentation. Recent commits cover Secret Manager and ESO IAM work. |
| `gitops` | Issue [#39](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/39) and PR [#75](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/pull/75) are central for tenant provisioning. Issue [#80](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/80) and PR [#81](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/pull/81) track Gateway ArgoCD sync. Issue [#13](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/13) is the selected monitoring deep-dive anchor. Issues [#4](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/4), [#6](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/6), [#7](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/7), [#9](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/9), [#10](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/10) and [#11](https://github.com/Infrastructure-Engineering-PT-Group-F/gitops/issues/11) support the security, onboarding, runbook and staging parts. |
| `backend` | PR [#34](https://github.com/Infrastructure-Engineering-PT-Group-F/backend/pull/34) prepares release 1.4.0. Issue [#33](https://github.com/Infrastructure-Engineering-PT-Group-F/backend/issues/33) tracks chart/appVersion synchronization. Recent commits include Gateway API HTTPRoute chart work. |
| `frontend` | Issue [#34](https://github.com/Infrastructure-Engineering-PT-Group-F/frontend/issues/34) tracks private GHCR image-pull validation. Issue [#23](https://github.com/Infrastructure-Engineering-PT-Group-F/frontend/issues/23) tracks the optional cloud-storage SPA hosting bonus. |

## Open preparation tasks

- Refresh the issue and PR state shortly before presenting, especially the
  `gitops` tenant provisioning and Gateway sync work.
- Fill in actual cost numbers and screenshots from the cost planning and cost
  monitoring issues.
- Decide whether the live demo creates a brand-new tenant or walks through a
  prepared tenant pull request.
- Confirm the exact tenant name, endpoint and staging tenant used in the demo.
- Confirm the monitoring page URL, access path and the tenant health/resource
  panels to show.
- Prepare one fallback screenshot set for ArgoCD, Crossplane, tenant namespace
  resources, the application endpoint and the monitoring page.
- Assign the final speaker list to the actual attendees and adjust the table if
  someone cannot present.
