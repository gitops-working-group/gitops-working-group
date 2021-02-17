# Glossary

- **Desired State**

    The aggregate of all configuration data for a system form its "Desired State".  The "Desired State" of a system is defined as data sufficient to recreate the system so that instances of the system are behaviourally indistinguishable.

- **State Store**
    
    A system for storing versioned, immutable Desired States that provides access control and auditing on the changes to the Desired State. Git may be configured as a State Store, but special precautions must be taken.

- **Reconciliation**
  
  The process by which the current state of a system is compared against and made consistent with the system's desired state as declared in the state store

- **Software System**

    One or more Runtime environments consisting of resources under management.
    In each Runtime, management Agents to act on resources according to security policies.
    One or more software Repositories for storing deployable artifacts that may be loaded into the runtime environments, eg. configuration files, code, binaries and packages. 
    One or more Administrators who are responsible for operating the runtime environments ie. installing, starting, stopping and updating software, code, configuration, etc.
    A set of policies controlling access and management of repositories, deployments, runtimes.
