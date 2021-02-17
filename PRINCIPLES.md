<!-- see https://github.com/yzhang-gh/vscode-markdown/blob/master/README.md#table-of-contents -->
# GitOps Principles v0.1.0 <!-- omit in toc -->

## ⚠️ THIS DOCUMENT IS A WORK IN PROGRESS AND SUBJECT TO PUBLIC REVIEW BEFORE PUBLICATION <!-- omit in toc --> ⚠️ 

This document provides a concrete definition of GitOps principles.

The GitOps Principles are vendor and implementation neutral, and aim to provide a common understanding of GitOps systems, to enable a common framework of understanding beyond individual opinion. A second aim is to encourage innovation by clarifying the technical outcomes rather than the code, tests, or organizational elements needed to achieve them. 

## Table of Content <!-- omit in toc -->

<!-- Insert auto-generated toc here -->
- [Summary](#summary)
- [Introduction](#introduction)
- [Scope](#scope)
- [The GitOps Principles](#the-gitops-principles)
  - [1. Declarative configuration](#1-declarative-configuration)
    - [What is a system's Desired State?](#what-is-a-systems-desired-state)
    - [Why must the Desired State be declarative data?](#why-must-the-desired-state-be-declarative-data)
    - [Why is human readability required?](#why-is-human-readability-required)
    - [How much of a system must be declared?](#how-much-of-a-system-must-be-declared)
  - [2. Immutable configuration versions](#2-immutable-configuration-versions)
    - [What forms a version?](#what-forms-a-version)
  - [3. Continuous state reconciliation](#3-continuous-state-reconciliation)
  - [4. Operations through declaration](#4-operations-through-declaration)
- [See Also](#see-also)

## Summary

GitOps is a set of principles for operating and managing software systems.

When using GitOps, the desired state of a system or subsystem is defined declaratively as versioned, immutable data, and the running system's configuration is continuously derived from this data.

GitOps principles were derived from modern software operations but are rooted in pre-existing and widely adopted best practices. These principles are:

1. [**The principle of declarative configuration**](#1-declarative-configuration)

    A system managed by GitOps must have its _Desired State_ expressed declaritively as data.
    This declarative data must be in a format writable and readable by both humans and software.

2. [**The principle of immutable configuration versions**](#2-immutable-configuration-versions)

    _Desired State_ is stored in a way that supports versioning, immutability of versions, and retains a complete version history.
    We call systems that store desired state in this way _State Stores_.

3. [**The principle of continuous state reconciliation**](#3-continuous-state-reconciliation)

    Software agents continuously, and automatically, compare a system's _Actual State_ to its _Desired State_.
    If the actual and desired states differ, automated actions are immediately attempted to reconcile them.
    These differences could be due to the actual state drifting from the desired state, or the desired state changing intentionally.

4. [**The principle of operations through declaration**](#4-operations-through-declaration)

    When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly.
    Instead, the agent will create a new declarative version of the desired state in the state store.

## Introduction

The software systems that we manage vary widely; from battery powered embedded systems driven by microcontrollers, to globally distributed applications with millions of users. 
Most systems are composed of subsystems themselves made of software.
It is impossible to comprehensively outline all the specific practices for managing such a variety of systems.

However, despite the myriad differences, several important principles emerge that simplify the task of reliably managing and operating _all_ software systems at scale. GitOps attempts to capture some of these principles in a coherent framework.
The GitOps principles can be applied to managing entire software systems or applied only to parts of larger systems.

See also the [Rationale for GitOps](RATIONALE.md).

## Scope

GitOps concerns the verifiable behaviour of computer systems and their interfaces.
Specifically, GitOps is _not_ about human processes, and is not intended as a model for judging human organisational designs and operational practices.

The GitOps principles are to be used as guiding principles in the development of modern software and system operations. They do not form a concrete specification.

The GitOps principles are a direction, not a destination. They should be applied pragmatically. For example, whilst desirable to apply them strictly to an entire software systems, they can also be applied loosely to selected parts of larger systems as part of a progressive adoption.

## The GitOps Principles

### 1. Declarative configuration

<div style="background: #E3F2FD; border-left: 3px solid #0D47A1; padding:10px; margin-bottom:5px; font-style:italic">
A system managed by GitOps must have its <em>Desired State</em> expressed declaritively as data.
This declarative data must be in a format writable and readable by both humans and software.
</div>

#### What is a system's Desired State?

_Configuration_ is a common feature of most software systems.
By "Configuration", we mean _data that defines how a system or subsystem should behave_.
This configuration data is distinct and separate from the data a system will process.

For example, the same web server code may be running on thousands of different servers managed by hundreds of different companies.
The behaviour of an individual webserver will differ based on how it is configured.
Configuration data is typically in the form of files or arguments to a computer program, but some systems may also currently use configuration databases or remote configuration services. Configuration also includes data about what version of code a software system should run, so software version information is also considered configuration.

Together, the aggregate of all configuration data for a system form its "Desired State". The "Desired State" of a system is defined as data sufficient to recreate the system from nothing so that instances of the system are behaviorally indinstinguishable.

#### Why must the Desired State be declarative data?

This is a subtle but important point.
In deference to the work done by the Infrastructure as Code community (IaC), we believe that this was the intent of that movement to begin with.
However, we have in practice seen a misunderstanding in this area, and many implementations have considered imperative scripts or programatic definitions for provisioning infrastructure to be a sufficient implementation of Infrastructure as Code. We disagree.

We make the distinction explicitly for two important reasons:

Firstly, it forces a separation of concerns between the Desired State (_what_ a system is) and _how_ the system is made to reach that state.
This modular approach enables the implementation details of operations (the _how_) to be separated and iterated on independently from the system configuration (the _what_). 
It also enables different tools and implementations to use the same Desired State declaration and interoperate against a common data language. 
These modular systems are more flexible.
For example, a Python program could verify a configuration file, while a C++ executable actually implements the declaration into a running system. Encoding the Desired State with a programming language ties the implementation to it, or forces other components to create a fully featured interpreter.

Secondly, verifying the correctness and self-consistency of data is significantly less complex than verifying the correctness of a program's behaviour, which is fundamentally undecidable. 
Verifying that a set of declarations is correct, however, _is_ decidable, even if sometimes computationally expensive.
As a general rule, this implies that the data language used to defined the Desired State should have no control flow structure, and consist exclusively of referentially transparent expressions without side effects. 
In other words, a human-readable data-serialization format.

It is also preferrable to use a widely supported language to define the Desired State for the sake of interoperability. For example, YAML, XML, JSON and TOML all have broad support and well defined specifications, although there are many other suitable candidates.

#### Why is human readability required?

Operationally, it has been proven time and time again that the canonical Desired State of a system should be human-readable and writable.

The Desired State encodes the _intent_ of a system. For example, where internet traffic should be routed. The collection of decisions about a system captured in its Desired State are of particular interest to its human operators. They must be able to directly describe their intent about the state of a system; and similarly, must be able to decipher the intended state of a system from its configuration.

This principles not only capture a requirement about the format of the configuration, but also the qualitative readability of configuration _in practice_. For example, a simple YAML or XML file can be easily read, understood and modified by human operators, but experience has taught us that these formats also allow the creation of complex self-referential documents beyond the ability of most humans to interpret. Such complex document would violate this principles, even though the formats are, on the surface, human-readable.

This relative readability also implies that the users are relevant when evaluating whether a system follows this principle. For example, the Desired State defined with a rich grammar of S-Expressions would suit a team of developers with a background in functional programming but would violate this principle if the majority of the team found the format incomprehensible.

Having a human-readable Desired State does not in any way preclude the use of rich tooling or graphical interfaces that facilitate Desired State generation and interpretation. It only require that the canonical source of truth be human readable and writable plain text.

#### How much of a system must be declared?

Ideally, all of it; and the entire system can be recreated exclusively from its Desired State.

That said, the definition of a "computer systems" can be quite broad and strays into human processes and systems as well. 
For example, is a company's sales process a "computer system"? 
Likely in parts. 
Should GitOps be applied to the entire sales process including the human processes (without prejudice as to what those processes are)? 
Whilst such a vision is compelling, a more pragmatic approach is preferrable, otherwise we risk trying to boil the ocean.

Instead, we should focus on subsystems where the Desired State is well defined, implement the GitOps principles there, and grow out to capture more systems from that initial subsystem. <!-- This progressive approach to GitOps is elaborated further in [the guide to adopting GitOps.md](ADOPTING_GITOPS.md). -->

### 2. Immutable configuration versions

<div style="background: #E3F2FD; border-left: 3px solid #0D47A1; padding:10px; margin-bottom:5px; font-style:italic">
<em>Desired State</em> is stored in a way that supports versioning, immutability of versions, and retains a complete version history.
We call systems that store Desired State in this way <em>State Stores</em>.
</div>

#### What forms a version?

A version is the Desired State for a system as a whole. It is the canonical form of what we desire the system to be at a point in time.

It is insufficient to version part of the Desired State or to version these parts in separate State Stores. Real software systems often have overarching behaviour that is the result of coupling between components. If the Desired State of these components were to change independently, it would be difficult to map a change in observed behaviour of our system to a single change in Desired State. Being able to make this 1:1 mapping is operationally beneficial, as we can then map behavioural issues of our system directly to the changes that occured. The utility of having the entire system defined in a single canonical location grows in proportion to the complexity and internal coupling of the system. A web of references to configuration data located in different locations is undesirable, as it makes understanding the desired state particularly difficult.

Versions should be uniquely named. This need not be a semantically meaningful name. It is sufficient that each new version is attributed a name that identifies it uniquely. Once a new version has been created, it should be immutable. By this we mean that it should be impossible to modify the relationship between a version's unique name and its value of the Desired State. 

All but the very first version should reference a predecessor or parent, which is another uniquely named version. This enables us to retain a history of the changes.

<!--
#### Why is it necessary to have versions be immutable and retained indefinitely?



- only verb is to create a new version.
This - Only uniquely named new versions of the system configuration can be created and all configuration info is retained (forward only)
- rollback
- Audit
The only exception being in the case of sensitive information leaks due to error.
  (I would agrue that key rotation is always better option in this case, but for PII and proprietary info this isn't possible).
- changes as transactions

#### What are the responsibilities of a State store?
- In addition, state stores must preserve metadata information regarding the identity of agents that create new versions.
The Desired State of the new version, Who created it, when it was created and ideally, also _why_ it was created. - What Why, who when. 

- Even though we say git, it's actually only true when configured in a very particular way.

#### State stores as coordination points/ collab via common data interface
- Collab point. 
- Business rules and security rules about the acceptable state of the system shoudl be checked against any new proposed version of the desired configuration before such changes are accepted as a new version. (Gates before version)
- where human process is integrated
- the place where collaboration can be synchronised.
-->

### 3. Continuous state reconciliation

<div style="background: #E3F2FD; border-left: 3px solid #0D47A1; padding:10px; margin-bottom:5px; font-style:italic">
Software agents continuously, and automatically, compare a system's <em>Actual State</em> to its <em>Desired State</em>.
If the actual and desired states differ, automated actions are immediately attempted to reconcile them.
These differences could be due to the actual state drifting from the desired state, or the desired state changing intentionally.
</div>

<!--
- If the software agents fail to bring the system's state in line with its desired state, a human operator is notified.
- Software agents continuously check that the running system under management matches the desired state configuration, and if it does not, immediately either take remedial action to bring the system back in line with stated expectations or, if this cannot be done, alert a human operator that the system is no longer meeting expectations
- Automated delivery: Delivery of the declarative descriptions, from the repository to runtime environment, is fully automated.
- Software Agents: Reconcilers maintain system state and apply the resources described in the declarative configuration.
- Closed loop: Actions are performed on divergence between the version controlled declarative configuration and the actual state of the target system.
- This automation should serve its human users.
  To this point, reconciliation automation for GitOps should include a way for humans to temporarily take back the reins as needed.
- Implies observability. State of the running system must be observable. Ideally in same format as the configuration so we can compare like to like. 
- >I agree. I think of this as an observability requirement and tend to say that "the current state of a running system must be observable" to mean the same thing. This is, in my opinion, required for state reconciliation. I didn't add a note there explicitly though, as that section was unfinished.
-->


### 4. Operations through declaration

<div style="background: #E3F2FD; border-left: 3px solid #0D47A1; padding:10px; margin-bottom:5px; font-style:italic">
When wishing to operate on a software system, a human or software agent will not interact with the running system and modify it directly.
Instead, the agent will create a new declarative version of the desired state in the state store.
</div>
<!--
- All normal operations should occur via the creation of a new uniquely named version, not through direct interaction ith the system under management
- Break glass - exceptions are acceptable and quite likely. and credentials to access and mutate the system must still be available in almost all cases.
-->

<!--
## General notes on the GitOps principles

- Tool and system agnosticicsm.
  
- It's ok to be pragmatic with implementations - We recognise that few real systems can be “100% GitOps”.
  Real world systems have a lifetime measured in years and must interact with many other systems created under alternative paradigms.
  As such they involve compromises and workarounds.
  
- lowest turtle isn't declarative, because the real world isn't.
  We aim for the lowest turtle to be as small as possible (imperative surface area )

- Git as a state store: - the "state store" can be a subfolder in a particular branch, and repo.
  Principles only applies to the data used to configure a running system, not other data in the same git repository nor runtime application data.

- The human interface can be whatever - GitOps doesn't mean the absence of a rich user experience or restrictions to the CLI

## Prior Art

- Whitehorse: https://www.zdnet.com/article/microsoft-places-bet-on-whitehorse/
- IaC
- Functional-Reactive programming (http://conal.net/papers/icfp97/icfp97.pdf)
- OODA loop

For naming discussion see <https://github.com/gitops-working-group/gitops-working-group/issues/8>


- [Common GitOps Practices](PRACTICES.md)
- [GitOps Compared to Other Practices]()
- [The GitOps adoption Journey]()
- [GitOps Patterns]()

-->

## See Also

- [The GitOps Glossary](GLOSSARY.md)
