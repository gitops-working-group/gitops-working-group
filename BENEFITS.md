# Benefits of GitOps

- continuous delivery (of configuration)
- Rollback for free (or cheap)
- Easy to statically verify (data vs code)


We have observed improvements in the following areas -  

- Automation: Correct, reproducible systems and lifecycle operations at scale
- Security: Runtime isolation and Policies for automation (including manual checks)
- Simplified operations, improved developer agility, faster mean time to recovery, all due to automation that uses the Repositories as a single source of truth.
- Reliable deployment, patching and update of applications (“the whole stack”)
- Remote management - Runtimes can be physically separate from Repos.

## Automated vs Manual operations

GitOps is a paradigm for automated runtime system operations.  

This is to be contrasted with previous “manual” paradigms, in which management exclusively proceeds by making step by step changes to a system using a CLI or GUI with direct access.  In manual systems it is hard to make correct changes repeatedly, as errors creep in with various increasingly negative effects at scale.  Automation has been attempted using scripting and batching, eg. using a CI tool, but this is too brittle to scale.
