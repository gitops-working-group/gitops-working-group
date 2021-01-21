**⚠️ THIS DOCUMENT IS A WORK IN PROGRESS AND SUBJECT TO PUBLIC REVIEW BEFORE PUBLICATION.**

# GitOps

## Summary

Gitops is an operation model for managing software system based a set of defining principles. GitOps principles were derived from modern software operations but are rooted in pre-existing and widely adopted best practices. These principles are:

1. **The principle of declarative configuration**

    All systems managed by GitOps are configured declaratively as data and all resources managed through a GitOps process must be expressed declaratively. The sum of configuration data for a system forms the _Desired State_ of a system.

2. **The principle of immutable configuration versions**

    The declarative system configuration is stored in a way that supports versioning, immutability of versions, and retains a complete version history. We call systems that store desired state in this way _State Stores_.

3. **The principle of continuous state reconciliation**

    Software agents continuously, and automatically, compared a system's actual state to its desired state. If the actual state differs from the desired state – which could be because the actual state has drifted from the desired state, or because the desired state has changed – automated actions are immediately attempted to bring the system's state in alignment with the desired state.

    If the software agents fail to bring the system's state in line with its desired state, a human operator is notified.

4. **The principle of operations through declaration**

    When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly. Instead, the agent will create a new declarative version of the desired state in the state store.

## Introduction

The software systems that we manage vary widely; from battery powered embedded systems driven by microcontrollers, to globally distributed applications with millions of users. It is impossible to outline specific practices for managing such a variety of systems. However, despite the differences in software systems, several important principles emerge that significantly simplify reliably managing and operating all software systems at scale.

_Configuration_ is a common feature of most software systems. By Configuration, we mean data that defines how the system will behave and operate. This data is distinct and separate from the data the system will process. For example, the same web server code may be running on thousands of different servers managed by hundreds of different companies. The behaviour of an individual webserver will differ based on how it is configured. 

Configuration is typically in the form of files or arguments to a computer program, but some systems may also currently use configuration databases or remote configuration services.

Configuration also includes data about what version of code a software system should run, so software version information is also considered configuration. Together, the sum of configuration data for a system form its "Desired State".

Currently, many software system's desired state is not defined separately from the running system. When we desire the behaviour of a software system to change, we modify the system directly, either through human action, or by running scripts that take a set of predetermined action on the system.

This leads to several serious issues.

Firstly, if a defect is perceived in the system's behaviour, it is impossible to determine whether the defect is due to the system having entered an incorrect state, or the defect is in our expectations about the system's behaviour. A person may have made incorrect assumption about the state of the system, or two people may have different excpectations about a system's behaviour and what one perceives as an error, may be correct for the other. Making the desired state of a system explicit avoids this issue altogether. As a concrete example, imagine logging into an administration console and seeing that 28 machines are healthily running. Is this good? Is this bad? That very much depends on what the desired number of machines is. For example, these could be test machines that should have been deleted and are now incurring a significant cost for no reasons, or all that remains of a 100 machine datacenter. We could consult the documentation, or expect the human operator to know, but by the time this occurs, our system has been in an incorrect state for a significant period of time.

Secondly, if the desired state of a system is not defined outside of the running system itself, how do we handle a failure that occurs whilst we are modifying its state directly? Such failures are extremely common and the likelihood of failure grows algebraically with the number of components in our system. In the failure case, we no longer know what the correct state of our system is. We are left with the option of backing up or system state before a change so that we can restore a known good state if something goes wrong. Such an approach is painful in practice and leads to an aversion to changing the system's state.

Thirdly, access control.

<!-- software system is a function curried over its configuration  a function is also data. A software system is a function: f Code, Configuration => Data => output -->

We believe these principles of software operations to be universally applicable, and independent of any particular tool, solution or practice. 
Modern software operations 


When using GitOps the desired state of a system is immutably defined in a versioned configuration store, often Git, and tools are used to automatically reconcile operations based on versioned changes to those definitions.

<!--
Consider how to not alienate the configuration as code community.
-->
However, there are some common principles that applu However, operating these systems 
Distinction that what we talk about here is universally applicable, and will not change, whereas practices will.

Tool and system agnosticicsm.

## Principles

### The principle of declarative configuration

> All systems managed by GitOps are configured declaratively as data and all resources managed through a GitOps process must be expressed declaratively. The sum of configuration data for a system forms the _Desired State_ of a system.

- data > code because verification
- a format readable by machines and humans 
- entire system can be recreated from the configuration.

### The principle of immutable configuration versions

> The declarative system configuration is stored in a way that supports versioning, immutability of versions, and retains a complete version history. We call systems that store desired state in this way _State Stores_.

- Desired configuration should be immutably versioned, 
- only uniquely named new versions of the system configuration can be created and all configuration info is retained 
- The only exception being in the case of sensitive information leaks due to error. (I would agrue that key rotation is always better option in this case)
- In addition, state stores must preserve information regarding the identity of agents that create new versions.
- state store should 
- Business rules and security rules about the acceptable state of the system shoudl be checked against any new proposed version of the desired configuration before such changes are accepted as a new version. (Gates before version)
- where human process is integrated
- changes as transactions


### The principle of continuous state reconciliation

> Software agents continuously, and automatically, compared a system's actual state to its desired state. If the actual state differs from the desired state – which could be because the actual state has drifted from the desired state, or because the desired state has changed – automated actions are immediately attempted to bring the system's state in alignment with the desired state.
>
> If the software agents fail to bring the system's state in line with its desired state, a human operator is notified.

- Software agents continuously check that the running system under management matches the desired state configuration, and if it does not, immediately either take remedial action to bring the system back in line with stated expectations or, if this cannot be done, alert a human operator that the system is no longer meeting expectations

### The principle of operations through declaration

> When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly. Instead, the agent will create a new declarative version of the desired state in the state store.

- All normal operations should occur via the creation of a new uniquely named version, not through direct interaction ith the system under management



## Notes on the GitOps principles
- Tool and system agnosticicsm. Even though we say git, it's actually only true when configured in a very particular way.
- The definition describes the verifiable behaviour of computer systems and their interfaces.  It is not intended as a model for judging human organisational designs and operational practices.
- It's ok to be pragmatic with implementations - We recognise that few real systems can be “100% GitOps”.  Real world systems have a lifetime measured in years and must interact with many other systems created under alternative paradigms.  As such they involve compromises and workarounds.  
- lowest turtle isn't declarative, because the real world isn't. We aim for the lowest turtle to be as small as possible (imperative surface area )

- Principles 1 and 2 encode concpets that are several decades old. Specifically, we look at the work done around IaC and find that a stricter set of principles is necessary to embody the intent of IaC. For relaible software operations, It's insufficient to have code define the infrastructure, it must instead be data.

- Git as a satte store: - the "state store" can be a subfolder in a particular branch, and repo. Principles only applies to the data used to configure a running system, not other data in the same git repository.

## Benefits

- continuous delivery (of configuration)
- Rollback for free (or cheap)
- Easy to statically verify (data vs code)


## Practices

Include referenced example. 

### Patterns

- Pull requests review/ conformance
- Change from SW and humans takes the same verification path

### Antipatterns

These exclude practices from being defined as "GitOps".

- IaC with shell scripts - Note that this also breaks the intent of IaC

## GitOps and ...

### GitOps and IaC

GitOps is a superset of the ideas of Infrastructure as code and build on previosu work done in the filed of IaC. We see IaC as essentially principles 1&2. In practice, many people have taken IaC to mean imperatively defined infrastructure with scripting languages, although we believe it was always the intent of the IaC originator to have this mean Data. this difference between IaC as broadly defined and IaC as intended is why we were stricter with our definition, and this issue with IaC is the reason we created this document, to ensure that the definition of GitOps would not be sybject to the same dilution as a learning from what happend with IaC <!--Law as defined vs law as intended.-->

### GitOps and DevOps

devops is a set of human practices around ownership of code development and operations. It doesn't talk about software system configuration, although discipline in such practcies is common with practicioners of devops. DevOps and GitOps are compatible, as they relate to different domains. We see GitOps as greatly facilitating the task of devops, and we praise the effort of devops of bringing development tools and practices to operations, and feel thatlike Gitops, as define with a strong background in developer tools, practcies and CS theory is a natural fit for a devops team to adopt.

### GitOps and OODA

- **Observe** - gather info on running system
- **Orient** - compare to desired state / diff
- **Decide** - derive a set of remedial actions (maybe nothing, maybe act on system, maybe notify human)
- **Act** - implement the actions

### GitOps and Agile
<!-- Desirable? -->
How the models map to each other if at all




## Prior art
- Whitehorse: https://www.zdnet.com/article/microsoft-places-bet-on-whitehorse/
- IaC
- Functional-Reactive programming (http://conal.net/papers/icfp97/icfp97.pdf)
- OODA loop

Manifesto
 -> Glossary
 -> Personas
 -> FAQ
 - -> GitOps Pattern 
     - -> Implementation on AWS
     - -> Implementation on Azure
     - -> Implementation on Metal


For naming discussion see <https://github.com/gitops-working-group/gitops-working-group/issues/8>
