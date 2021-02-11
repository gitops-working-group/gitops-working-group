<!-- omit in toc -->
# GitOps Working Group

- [About GitOps](#about-gitops)
  - [What is GitOps?](#what-is-gitops)
  - [Who is GitOps for?](#who-is-gitops-for)
  - [Growing Adoption of GitOps](#growing-adoption-of-gitops)
  - [Using GitOps](#using-gitops)
- [About the Working Group](#about-the-working-group)
  - [WG Mission](#wg-mission)
  - [WG Origin](#wg-origin)
  - [WG Participation](#wg-participation)
  - [WG Timeline (WIP)](#wg-timeline-wip)

## About GitOps

### What is GitOps?

Gitops is a set of principles for operating and managing software systems.

In essence, the desired state of a system or subsystem is defined declaratively as versioned, immutable data, and the running system's configuration is continuously derived from this data.

GitOps principles were derived from modern software operations but are rooted in pre-existing and widely adopted best practices. These principles are:

1. The principle of declarative configuration
2. The principle of immutable configuration versions
3. The principle of continuous state reconciliation
4. The principle of operations through declaration

See the full [PRINCIPLES.md](PRINCIPLES.md) and [Glossary](GLOSSARY.md).

### Who is GitOps for?

<!-- Short summary here, similar to the above, once we get farther along with these documents. -->
GitOps [builds and iterates](https://www.weave.works/blog/gitops-operations-by-pull-request) on ideas drawn from DevOps and Infrastructure as Code that started with [Martin Fowler’s comprehensive Continuous Integration overview](https://martinfowler.com/articles/continuousIntegration.html) and provides the freedom to choose the tools that you need for your specific use cases.

Individuals, teams, and organizations who implement GitOps experience many benefits, including:

- Increased Developer & Operational Productivity
- Enhanced Developer Experience
- Improved Stability
- Higher Reliability
- Consistency and Standardization
- Stronger Security Guarantees

See [BENEFITS.md](BENEFITS.md), [USE_CASES.md](USE_CASES.md) and [PERSONAS.md](PERSONAS.md)

### Growing Adoption of GitOps

The creation of the GitOps Working Group was driven by the accelerating adoption of GitOps tools and methodologies by users of services from Amazon, Codefresh, GitHub, Microsoft, Weaveworks, and hundreds of other leading global companies that are adopting GitOps.
This, combined with the recommendation by the Cloud Native Computing Foundation (CNCF) [user community to adopt Flux](https://radar.cncf.io/2020-06-continuous-delivery), made it clear that GitOps is fast becoming the methodology of choice for operating modern cloud native infrastructure and applications.
The CNCF user community reported that development, DevOps, and operations teams who adopt GitOps tooling and follow best practices experience improvements in productivity, stability, reliability, and security for their cloud native environments.

See [RATIONALE.md](RATIONALE.md)

### Using GitOps

See [CASE_STUDIES.md](CASE_STUDIES.md), [PATTERNS.md](PATTERNS.md), [TOOLS.md](TOOLS.md), and [RELATIONSHIP_TO_OTHER_PRACTICES.md](RELATIONSHIP_TO_OTHER_PRACTICES.md).

## About the Working Group

### WG Mission

The GitOps Working Group is a neutral organization of interested parties to clearly define a principle-lead meaning of GitOps, in order to better enable interoperability between tools.
With a clear definition, GitOps Certification Programs for individuals will also be possible.

**Question (Scott):** Is this actually a goal of this working group?
> A further goal is to provide companies and individuals with skills, knowledge and competency to implement GitOps tooling and methodologies which simplify the operation and management of infrastructure and cloud native applications.

### WG Origin

On November 19, 2020, Amazon, Codefresh, GitHub, Microsoft, and Weaveworks announced the creation of the GitOps Working Group.
This will be an open CNCF community project created inside the CNCF [gitops-working-group GitHub organization](https://github.com/gitops-working-group) as the initial venue for collaboration and open governance.
<!-- Farther below it said:
"Documenting the GitOps principles, and supporting WG GitOps in CNCF App Delivery SIG as an OSS project."
We shoudl clarify this as soon as possible. -->
For current status of the Working Group, see [issue #32](https://github.com/gitops-working-group/gitops-working-group/issues/32).

### WG Participation

The Working Group is inviting companies and individuals who are actively participating in the rapidly growing GitOps ecosystem to join this new community and help contribute to its success as a standard across the cloud native landscape.

Specific roles and processes for getting involved are still being defined.
If you are interested in participating – please follow this issue rather than opening a new one: [Clarify WG roles and process for getting involved #38](https://github.com/gitops-working-group/gitops-working-group/issues/38).

In the meantime, you can:

- Watch or star this repo if you are interested in keeping abreast of any new developments
- Attend working group [MEETINGS.md](MEETINGS.md) (schedule coming soon), where we'll review all open issues and PRs.
- [Open an issue](/../../issues/new) and let us know how you're using GitOps and any important considerations we should include.
- Join `#wg-gitops` on [CNCF Slack](https://slack.cncf.io/)
- Join the [SIG App Delivery](https://github.com/cncf/sig-app-delivery) mailing list, and watch or participate in topics prefixed with `[gitops-wg]`
- See [Working Group project boards](https://github.com/orgs/gitops-working-group/projects) for status of work, or for ideas on areas that could use additional participation

The GitOps Working Group is governed by the [governance document](GOVERNANCE.md).
We as a community follow the [code of conduct](CODE_OF_CONDUCT.md).

### WG Timeline (WIP)

| | |
| - | - |
| **Q4 of 2020** | Form the Working Group |
| **End of March, 2021** | Establish V1 of the GitOps PRINCIPLES |

<!--
### Additional Information

**Question (Scott):** Should we move this to "Prior Art" in the new PRINCIPLES.md?
Please see [GitOps WG Charter](https://docs.google.com/document/d/11EZfvB2FFI837nMmArnyv-wizsIJvc-4_xdgfoUXF4o/view)
and [Draft Definition](https://docs.google.com/document/d/11EZfvB2FFI837nMmArnyv-wizsIJvc-4_xdgfoUXF4o/view)
for initial details.
-->
