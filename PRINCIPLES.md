<!-- see https://github.com/yzhang-gh/vscode-markdown/blob/master/README.md#table-of-contents -->
# GitOps Principles v0.1.0 <!-- omit in toc -->

## ⚠️ THIS DOCUMENT IS A WORK IN PROGRESS AND SUBJECT TO PUBLIC REVIEW BEFORE PUBLICATION <!-- omit in toc -->

This document provides a concrete definition of GitOps principles.
The GitOps Principles are vendor and implementation neutral, and aims to grow a common understanding of GitOps systems based on shared principles, rather than a matter of individual opinion. A second aim is to encourage innovation by clarifying the technical outcomes rather than the code, tests, or organizational elements needed to achieve them.

## Table of Content <!-- omit in toc -->

<!-- Insert auto-generated toc here -->
- [Summary](#summary)
- [Introduction](#introduction)
- [Scope](#scope)
- [The GitOps Principles](#the-gitops-principles)
  - [1. Declarative configuration](#1-declarative-configuration)
  - [2. Immutable configuration versions](#2-immutable-configuration-versions)
  - [3. Continuous state reconciliation](#3-continuous-state-reconciliation)
  - [4. Operations through declaration](#4-operations-through-declaration)
- [General notes on the GitOps principles](#general-notes-on-the-gitops-principles)
- [Prior Art](#prior-art)
- [See also](#see-also)

## Summary

Gitops is a set of principles for operating and managing software systems.

In essence, the desired state of a system or subsystem is defined declaratively as versioned, immutable data, and the running system's configuration is continuously derived from this data.

GitOps principles were derived from modern software operations but are rooted in pre-existing and widely adopted best practices. These principles are:

<!-- Cross-link principles here to the longer discussion notes for each below -->
1. [**The principle of declarative configuration**](#tag)

    A system managed by GitOps must have its _Desired State_ expressed declaritively as data. 
    This declarative data must be in a format writable and readable by both humans and software.

2. [**The principle of immutable configuration versions**](#tag)

    _Desired State_ is stored in a way that supports versioning, immutability of versions, and retains a complete version history.
    We call systems that store desired state in this way _State Stores_.

3. [**The principle of continuous state reconciliation**](#tag)

    Software agents continuously, and automatically, compare a system's _Actual State_ to its _Desired State_.
    If the actual and desired states differ, automated actions are immediately attempted to reconcile them.
    These differences could be due to the actual state drifting from the desired state, or the desired state changing intentionally.

4. [**The principle of operations through declaration**](#tag)

    When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly.
    Instead, the agent will create a new declarative version of the desired state in the state store.

## Introduction

The software systems that we manage vary widely; from battery powered embedded systems driven by microcontrollers, to globally distributed applications with millions of users. 
Most systems are composed of subsystems themselves made of software.
It is impossible to comprehensively outline all the specific practices for managing such a variety of systems.

However, despite the myriad differences, several important principles emerge that simplify the task of reliably managing and operating _all_ software systems at scale. GitOps attempts to capture some of these principles in a coherent framework.
The GitOps principles can be applied to managing entire software systems or applied only to parts of larger systems. 

## Scope

GitOps concerns the verifiable behaviour of computer systems and their interfaces. 
Specifically, GitOps is not about human processes, and is not intended as a model for judging human organisational designs and operational practices.

The GitOps principles are to be used as guiding principles in the development of modern software and system operations. They do not form a concrete specification. 

The GitOps principles are a direction, not a destination. They should be applied pragmatically. For example, whilst they can be applied strictly to an entire software systems, they can also be applied loosely to selected parts of larger systems as part of a progressive adoption.

## The GitOps Principles

### 1. Declarative configuration

<div style="border: 1px solid black; padding:5px; font-weight:bold">
A system managed by GitOps must have its <em>Desired State</em> expressed declaritively as data. 
 This declarative data must be in a format writable and readable by both humans and software.
</div>

<!--
We've gone back and forth to try to find a really good single-word term for what we mean by "immutable, versioned, declarations of the desired system state".
"Configuration" is used below for now, though we understand this may be confusing since the rules that govern the behavior of the system can be much broader than what most software means by "configuration".
Good placeholder for now.
Bring back to the working group to discuss better terminology.
-->

_Configuration_ is a common feature of most software systems.
By Configuration, we mean data that defines how a system or subsystem will behave and operate.
This configuration data is distinct and separate from the data a system will process.
For example, the same web server code may be running on thousands of different servers managed by hundreds of different companies.
The behaviour of an individual webserver will differ based on how it is configured.
Configuration data is typically in the form of files or arguments to a computer program, but some systems may also currently use configuration databases or remote configuration services.

Configuration also includes data about what version of code a software system should run, so software version information is also considered configuration.
Together, the aggregate of all configuration data for a system form its "Desired State". The "Desired State" of a system is defined as data sufficient to recreate the system from nothing so that instances are behaviorally indinstinguishable.



- Ensure we clarify that the entire system need not be declared to qualify as "gitops". This is an ideal, most likely never to be reached (is your entire organization fully governed by git?). Rather this is meant as a progressive approach.
- the ideal is that the entire system can be recreated from the configuration.
- Formal definition of what we mean by "Configuration" is probably warranted here.
- three ideas: 1) declarative data, 2) Desired State 3) system under management can be part of larger systems (apply to subsystem))
- data > code because verification
- a format readable by machines and humans

### 2. Immutable configuration versions

> _Desired State_ is stored in a way that supports versioning, immutability of versions, and retains a complete version history.
> We call systems that store desired state in this way _State Stores_.


- Desired configuration should be immutably versioned
- Only uniquely named new versions of the system configuration can be created and all configuration info is retained
- The only exception being in the case of sensitive information leaks due to error.
  (I would agrue that key rotation is always better option in this case, but for PII and proprietary info this isn't possible).
- In addition, state stores must preserve information regarding the identity of agents that create new versions.
- What Why, who when. 
- state store should
- Business rules and security rules about the acceptable state of the system shoudl be checked against any new proposed version of the desired configuration before such changes are accepted as a new version. (Gates before version)
- where human process is integrated
- changes as transactions
- Even though we say git, it's actually only true when configured in a very particular way.
- For reliable software operations, It's insufficient to have code define the infrastructure, it must instead be data.



### 3. Continuous state reconciliation

> Software agents continuously, and automatically, compare a system's _Actual State_ to its _Desired State_.
> If the actual and desired states differ, automated actions are immediately attempted to reconcile them.
> These differences could be due to the actual state drifting from the desired state, or the desired state changing intentionally.

- If the software agents fail to bring the system's state in line with its desired state, a human operator is notified.
- Software agents continuously check that the running system under management matches the desired state configuration, and if it does not, immediately either take remedial action to bring the system back in line with stated expectations or, if this cannot be done, alert a human operator that the system is no longer meeting expectations
- Automated delivery: Delivery of the declarative descriptions, from the repository to runtime environment, is fully automated.
- Software Agents: Reconcilers maintain system state and apply the resources described in the declarative configuration.
- Closed loop: Actions are performed on divergence between the version controlled declarative configuration and the actual state of the target system.
<!-- Please emphasize the following point to aid adoption of GitOps to risk-averse teams (i.e., almost everyone in Enterprise) -->
- This automation should serve it's human users.
  To this point, reconciliation automation for GitOps should include a way for humans to temporarily take back the reins as needed.

### 4. Operations through declaration

> When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly.
> Instead, the agent will create a new declarative version of the desired state in the state store.

- All normal operations should occur via the creation of a new uniquely named version, not through direct interaction ith the system under management
- Break glass - exceptions are acceptable and quite likely. and credentials to access and mutate the system must still be available in almost all cases.

## General notes on the GitOps principles

- Tool and system agnosticicsm.
  
- It's ok to be pragmatic with implementations - We recognise that few real systems can be “100% GitOps”.
  Real world systems have a lifetime measured in years and must interact with many other systems created under alternative paradigms.
  As such they involve compromises and workarounds.
  
- lowest turtle isn't declarative, because the real world isn't.
  We aim for the lowest turtle to be as small as possible (imperative surface area )

- Git as a satte store: - the "state store" can be a subfolder in a particular branch, and repo.
  Principles only applies to the data used to configure a running system, not other data in the same git repository.

- The human interface can be whatever - GitOps doesn't mean the absence of a rich user experience or restrictions to the CLI

## Prior Art

- Whitehorse: https://www.zdnet.com/article/microsoft-places-bet-on-whitehorse/
- IaC
- Functional-Reactive programming (http://conal.net/papers/icfp97/icfp97.pdf)
- OODA loop

For naming discussion see <https://github.com/gitops-working-group/gitops-working-group/issues/8>

## See also

- [Key Benefits of GitOps]()
- [RATIONALE]()
- [Common GitOps Practices]()
- [GitOps Compared to Other Practices]()
- [The GitOps adoption Journey]()
- [GitOps Patterns]()
- [Glossary]()


