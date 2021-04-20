# Unsolved Problems in GitOps

While the GitOps ecosystem is maturing and adoption is growing rapidly, there are still a number of unsolved problems that are slowing it down.

## Templating

The breadth of the [tooling](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/declarative-application-management.md) available for templating declarative Kubernetes manifests (from both within and outside of a GitOps workflow) indicates a lack of maturity or consensus

### Exit Criteria

* Broad consensus on a templating approach(es) that enables templating and variables to be treated consistent across developer tooling

## Open Loops

Most if not all GitOps implementations are [Open Loops](https://en.wikipedia.org/wiki/Control_theory#Open-loop_and_closed-loop_(feedback)_control) that at best hide the difference between desired vs actual state from Git and at worst cause destructive actions based on a lack of awareness of how how state changes impact the system as a whole.


### Exit Criteria

* Most GitOps implementations default to closed loops and provide support for PID loops


## Controlled and safe promotion of changes across environments

Using multiple environments like "Sandbox", "Staging" and "Production" is standard practice. Referencing those environments in an IaC repo could be done by using conditionals(`if env = prod...`) and parameterizing (Helm `values.yaml`/Terraform `.tfvars`) or by using different folders/branches to describe different environments.

The parameters/conditionals approach has safety and timing control issue:
* Wrong env could be changed with an erroneous conditional or parameter override.
* Lack of timing control -  If I want to change part of the shared code, it happens in all environments at once, missing the point of pre-production environments.

The folders/branches reduce visibility, add toil and increase the chances of drift between environments:
* Syncing all the environments is laborious and error-prone
* Syncing of all environments is not enforced or encouraged = high reliance on cooperation of users
* The difference between the environments is not easily visible

A combination of both approaches can mitigate some of the issues but adds complexity.
