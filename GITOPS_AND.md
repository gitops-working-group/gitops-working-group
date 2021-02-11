
## GitOps and … (GitOps in relation to...)

### GitOps and IaC

GitOps is a superset of the ideas of Infrastructure as code and build on previosu work done in the filed of IaC.
We see IaC as essentially principles 1&2.
In practice, many people have taken IaC to mean imperatively defined infrastructure with scripting languages, although we believe it was always the intent of the IaC originator to have this mean Data.
This difference between IaC as broadly defined and IaC as intended is why we were stricter with our definition, and this issue with IaC is the reason we created this document, to ensure that the definition of GitOps would not be sybject to the same dilution as a learning from what happend with IaC <!--Law as defined vs law as intended.-->

Principles 1 and 2 encode concpets that are several decades old.
Specifically, we look at the work done around IaC and find that a stricter set of principles is necessary to embody the intent of IaC.

### GitOps and DevOps

DevOps is a set of human practices around ownership of code development and operations.
It doesn't talk about software system configuration, although discipline in such practcies is common with practicioners of devops.
DevOps and GitOps are compatible, as they relate to different domains.
We see GitOps as greatly facilitating the task of devops, and we praise the effort of devops of bringing development tools and practices to operations, and feel thatlike Gitops, as define with a strong background in developer tools, practcies and CS theory is a natural fit for a devops team to adopt.

### GitOps and OODA

- **Observe** - gather info on running system
- **Orient** - compare to desired state / diff
- **Decide** - derive a set of remedial actions (maybe nothing, maybe act on system, maybe notify human)
- **Act** - implement the actions

### GitOps and Agile
<!-- Desirable? -->
Agile is about development, GitOps about operations. Radically different concerns and domain. 

### GitOps and Functional Reactive Programming

React. No suprise that flux is a name that crops up in both domains.
