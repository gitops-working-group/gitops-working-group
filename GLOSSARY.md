# Glossary

- Desired state
- State Store
- 

the configuration of a system under management

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

### Software System

One or more Runtime environments consisting of resources under management
In each Runtime, management Agents to act on resources according to security policies.
One or more software Repositories for storing deployable artifacts that may be loaded into the runtime environments, eg. configuration files, code, binaries and packages. 
One or more Administrators who are responsible for operating the runtime environments ie. installing, starting, stopping and updating software, code, configuration, etc.
A set of policies controlling access and management of repos, deployment, runtimes.
