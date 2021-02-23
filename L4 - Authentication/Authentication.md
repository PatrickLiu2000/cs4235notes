# Authentication
## What is Authentication?
- TCB needs to know who makes request for a protected resource
- a process makes this request on behalf of a user
  
## Authentication Implementations
- Something a user knows
    - a password
- Something a user has
    - 2 factor authentication code
- Something a user is
    - biometric scanner

- problems with just a password
    - guessing password, impersonating login program to steal pwd, or keylogging
- hardware needs a trusted path
    - example: CTRL-ALT-DEL

## Implementing Password Authentication
- use one way hash function to store passwords
    - problem: attackers can use common passwords to determine the hash function, and can brute force easily
    - attackers can try popular passwords and create a rainbow table to find hash function
        - solution: use a random salt before hashing to make brute forcing more difficult
        - store this salt along with the hashed value
## Problems with Passwords
- as password length increases, usability suffers
- phishing/social engineering
- once password is stolen, can be used many times (people use same password for many things)
- human have a hard time remembering lots of passwords
- sysadmin tips:
    - never store passwords without any form of security
    - only store hashed values with a random salt and limit access
    - avoid general hash functions (slower = better)
- user tips:
    - use password managers