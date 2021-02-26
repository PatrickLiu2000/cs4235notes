# Mandatory Access Control (MAC)
- alternative to MAC: discretionary access control
    - owner of resource can choose how it is shared
    - problems: 
        - cannot control information flow (person you shared it with can also share to other people)
        - users should not control how control how data is shared (in enterprise environments)
- MAC - company controls how data should be shared
    - regulatory requirements limit sharing
    - for intelligence agencies, different classification levels for data (multilevel security)
        - top secret, secret, confidential, etc
## Implementing MAC
- Labels
    - indicate sensitivity/category of data or clearance
    - TCB associates labels with each user and object and checks the labels when access request made
    - depends on what policy is implemented
    - example of labels in a DoD env:
        - Label = `(sensitivity level, compartment)`
            - sensitivity level = top secret, secret, confidential, restricted, unclassified
            - Label1 =  (TS, {nuclear, chemical})
- sensitivity levels are totally ordered (Top secret > secret, etc)
- compartments can be partially ordered
### Comparing Labels
- pretty simple: if sensitivity level 1 > sensitivity level 2 AND both compartments are comparable, then L1 is more sensitive/dominates L2
    - even if sensitivity level dominates another, cannot compare unless both compartments are comparable

## Bell and La Padua Model (BLP Model)
- uses top secret, secret, etc for clearances
- *No read up, no write down rules*
    - a person cannot write to a document that is below their clearance level, and cannot read a document that is of higher clearance level than them
- focuses on integrity instead of confidentiality (as top secret documents can be written to by anyone)

## Biba Model
- opposite of BLP model
- *No read down, no write up rules*
- focuses on confidentiality rather than integrity

## Policies for Commercial Envs
- Clark-Wilson Policy:
    - same user cannot execute 2 programs that require separation of duty
- Chinese wall policy:
    - objects are put into conflict classes, and can access any object as long as they have not accessed another object in that class
    - can only select 1 object from each conflict class

# TCB Review
- TCB requires all software/hardware to operate securely 

1. Functional correctness
2. Maintain data integrity (even for bad input)
3. Protect disclosure of sensitive data
4. Confidence
5. Statement giving security we expect system to enforce

- *TCB design principles*
    - least privelage
    - economy
        - keep trusted code small (easy to analyze/test)
    - open design
        - security by obscurity doesnt work 
    - complete mediation
        - every access is checked
    - fail-safe defaults
        - deny requests by default
    - ease of use
        - users avoid security if it gets in their way
- Note: TCB only provides high assurance, not guarantee

## How to Build TCB
- support key security features
    - implement key security functions
        - authentication
        - access control to files
        - mandatory access control
        - discretionary access control
    - protection of data used by OS
        - object reuse protection
        - secure file deletion
        - secure disk destruction
    - complete mediation of accesses
    - trusted path from user to secure system
    - audit log showing object accesses
### Kernel Design
- kernel enforces all security mechanisms
- good isolation, small size
- tamper-proof (cannot be broken/disabled)
- un-bypassable (always invoked)
- analyzable

## Assurance
- convincing ourselves that an implementation is correct
- done by using 
    - pen testing
        - ethical hackers attempt to expose vulnerabilities
        - downside: cannot demonstrate absence of problem
    - formal verification validation
    - requirement checking, code reviews
- regression testing
    - ensure that new changes do not break existing functionality
- testing
    - challenges: creating test cases, code coverage, different execution envs
- Formal verification validation
    - mathematically checking program to ensure that security assertions hold
    - done using model checking
    - downside: exponential time/space complexity, not very realistic on actual OS kernel