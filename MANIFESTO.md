# GitOps Principles and Practices

For naming discussion see <https://github.com/gitops-working-group/gitops-working-group/issues/8>

# ⚠️ WORK IN PROGRESS

## Summary

This document defines GitOps. Gitops is an operation model for managing software system based a set of defining principles. GitOps principles were derived from modern software operations but are rooted in pre-existing widely adopted best practices. 

> XXX - digestible definiton of gitops, link to pillars/principles/practices.



1. Declarative Configuration: All resources managed through a GitOps process must be completely expressed declaratively.
2. Version controlled, immutable storage: Declarative descriptions are stored in a repository that supports immutability, versioning and version history. For example, git.
3. Automated delivery: Delivery of the declarative descriptions, from the repository to runtime environment, is fully automated.
4. Software Agents: Reconcilers maintain system state and apply the resources described in the declarative configuration.
5. Closed loop: Actions are performed on divergence between the version controlled declarative configuration and the actual state of the target system.

## Introduction
Modern software operations 


GitOps is a model for operating software systems made up of principles and practices. When using GitOps the desired state of a system is immutably defined in a versioned configuration store, often Git, and tools are used to automatically reconcile operations based on versioned changes to those definitions.

<!--
Language question: "code"? "definitions"? "declarations"? "configuration"? "data"?

Law as defined vs law as intended.

Consider how to not alienate the configuration as code community.
-->

## Terminology

Versioned
: When referencing "Git" in GitOps, we take it to mean a shorthand for "immutably versioned configuration store". It's important to note that use of git alone is not sufficient to meet criteria for GitOps. git or other versionable system must be configured in specific ways to meet the [principles](#principles).

Operations
: When referencing "ops" in GitOps, this is intended to broadly refer to "operations," which can include any part automatable system.

Definitions
: By GitOps "definitions", what is meant are Immutable declarations of whatever kind.

Reconciliation
: A continuously running attempt to reconcile _Definition_ of desired state with the current state.

System under management
: The system whose state is managed via GitOps.

## Principles

Software systems that we manage vary widely; from embedded systems driven by microcontrollers, to globally distributed applications with millions of users. 

Hopwever, there are some common principleHowever, operating these systems 
Distinction that what we talk about here is universally applicable, and will not change, whereas practices will.

1. Desired configuration should be fully declared in a format readable by machines and humans so that the entire system can be recreated from the configuration.

2. Desired configuration should be immutably versioned, so that only uniquely named new versions of the system configuration can be created and all configuration info is retained - The only exception being in the case of sensitive information leaks due to error. (I would agrue that key rotation is always better option in this case)

3. Software should be continuously checking that the running system under management matches the desired state configuration, and if it does not, immediately either take remedial action to bring the system back in line with stated expectations or, if this cannot be done, alert a human operator that the system is no longer meeting expectations

4. Business rules and security rules about the acceptable state of the system shoudl be checked against any new proposed version of the desired configuration before such changes are accepted

5. All normal operations should occur via the creation of a new uniquely named version, not through direct interaction ith the system under management

Tool and system agnosticicsm.

## Author's intent
It's ok to be pragmatic with implementations

## Benefits
- Rollback for free
- Easy to statically verify (data vs code)

## Practices

Include referenced example. 

### Patterns

- Pull requests review/ conformance
- Change from SW and humans takes the same verification path

### Antipatterns

These exclude practices from being defined as "GitOps".

- IaC with shell scripts - Note that this also breaks the intent of IaC

## Model Compatibility

### GitOps and IaC
How the models map to each other if at all

### GitOps and DevOps
How the models map to each other if at all

### GitOps and Agile
<!-- Desirable? -->
How the models map to each other if at all


## Glossary


## Prior art
- Whitehorse: https://www.zdnet.com/article/microsoft-places-bet-on-whitehorse/
- IaC
- Functional-Reactive programming (http://conal.net/papers/icfp97/icfp97.pdf)

Manifesto
 -> Glossary
 -> Personas
 -> FAQ
 - -> GitOps Pattern 
     - -> Implementation on AWS
     - -> Implementation on Azure
     - -> Implementation on Metal
