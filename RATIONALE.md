# Rationale for GitOps

Currently, many software system's desired state is not defined separately from the running system.
When we desire the behaviour of a software system to change, we modify the system's configuration directly, either through human action, or by running scripts that take a set of predetermined action on the system.

This leads to several serious issues:

- **Detecting drift from desired state**

    If the desired state of a system is not explicitly defined, it is impossible to verify if the system in a correct state. The state of a running system itself does not provide sufficent information to determine its correctness. 
    
    Consider logging into an administration console and seeing that 28 machines are healthily running.
    Is this good? Is this bad? That very much depends on what the desired number of machines is.
    For example, these could be test machines that should have been deleted and are now incurring a significant cost for no reasons, or all that remains of a 100 machine datacenter.
    We could consult the documentation, or expect the human operator to know, but by the time this occurs, our system has been in an incorrect state for a significant period of time. _The validity of the state of our system is not automatically verifiable_.

    This problem leads to the conclusion that the canonical source of truth for desired state cannot be the actual state. 
    Making the desired state of a system explicit prevents this problem.
    
- **Recovering from transitional states**

    If we have no record of the desired state of our system, how can we recover from failures that occur in the transition between states? 
    Such transitions are very common lifecycle events, such as upgrades, new features being released or scaling our resources. These are where the majority of hard software defects and transient errors occur.
    Not only are such failures extremely common, but their likelihood grows algebraically with the number of components in our system.
    
    When these failures occur, they leave our system in an indeterminate transitional state. Going back to a known good state or forward to a new desired states is difficult, as we don't have a record of what these should be, only lists of instructions
    
    We are left with the option of backing up our system state before a change so that we can restore a known good state if something goes wrong.
    This doesn't solve the problem of how to change our system to move to a new desired state. The best we can do is restore and retry. 
    This becomes extremely common in complex distributed systems, where transient failures are common.
    Such an approach is painful in practice and leads to an aversion to changing the system's state.
    
    This problem can be solved by having software agents that continuously converge the system towards a well-defined state. 
    
- **Controlling and auditing actors, access and actions**
    
    In most cases, we not only require the ability to change a running system safely, but we must also record what was changed, when, by whom, and why and enforce rules about which changes we allow.
    If our systems are changed through direct access, the surface area of the interface to control and monitor can quickly become overwhelmingly large. 
    
    Access control at different levels, from the network to the application layer must be controlled and audited. A coherent set of access control rules must be applied across varied systems configured in completely different, and sometimes incompatible, ways. 
    An audit trail may or may not be required for regulatory or governance reasons, but it is such a common requirement of managing software systems that it must be also be addressed.
    
    Having a single source of truth regarding the desired state of our system becomes a ledger of transactions between states and a single point of operation. This leads to a natural place to enforce rules regarding access and to audit changes. 

    Furthermore, by removing direct access, the credentials used to manage a system can be constrained to exist only within the security boundary of the system itself, which can poll its desired state. This greatly reduces the security surface area.

These are only a small sample of the issues that arise if we do not define the desired state of our software systems explicitly and declaratively. We believe GitOps is a solution to these many issues that plague software operations at scale. 

Since these issues occur so universally when operating software systems, we also believe that GitOps is fundamentally agnostic about specific tools. that is, the GitOps principles are universally applicable, and independent of any particular tool, solution or practice, including Git itself, after which they are named.
