# Buffer Overflows
- Can have stack and heap buffer overflows
- stack review:
    - used for function calls
    - stores local variables, parameters, return address, old frame pointer
    - as we call more functions, a new "stack frame" is added
- stack grows down - from high to low addresses
    - top of stack == smallest address
- in C, strings grow up in memory
    - this presents a problem:
    - example: program that takes string input and has a password local variable
```C
int main() {
    login();
}
void login() {
    int allow_login = 0;
    char pwdstr[12]; // user entered password buffer
    char targetpwd[12] = "MyPwd123";
    gets(pwdstr); // takes user input as string and stores it into pwdstr buffer
    if (strcmp(pwdstr, targetpwd, 12) == 0) {
        allow_login = 1;
    }
    if (allow_login == 0) {
        printf("login failed");
    } else {
        printf("login accepted");
    }
}
```
  
- many problems with this code!
    - since strings grow up in memory, and we do not have any bounds checking on the `pwdstr` buffer, we can overwrite the value of allow_login, and login even when we do not have the correct password!
- stack looks like this:

```
BOTTOM OF STACK/HIGH MEMORY
argc
argv
return address
allowlogin
pwdstr[8]
pwdstr[4]
pwdstr[0]
targetpwd[8]
targetpwd[4]
targetpwd[0]
TOP OF STACK/LOW MEMORY
```
- we can see that since strings grow upward, if we supply a password that is 13 characters or greater (cannot be 12, because strings are null terminated, and the 13th null character byte would overflow and still set `allowlogin` to 0), that we can overwrite the value of allowlogin and return address!

## Buffer Overflow Variations
- shell injection - return address is overwritten to point to shell code (allowing attacker to execute any command they would like)
- return to libc - return address is overwritten to point to a libc function
- heap overflow - data stored in heap is overwritten (heap stores tables of function pointers, so can overwrite function point to point to desired code location)

## Defense Against Buffer Overflows
- *Strongly typed languages*
- *Automatic bounds checking*
- *Automatic memory management (garbage collection)*
- some languages safe due to runtime checks, with the drawbacks of worse performance
- when using unsafe language, check all user input, use functions that perform bounds checking, and use automatic tools to detect unsafe functions

### More Buffer Overflow Defenses
- stack canaries - randomized values that are placed before functions, so that if overwritten, then program will throw error and code will not be executed any further
- Address layout space randomization (ASLR) - randomizes memory location of stack/heap, and more so that it is much more difficult to locate vulnerable memory locations
- Non-executable stack - means that code that is injected onto stack cannot be executed
- DOES NOT PREVENT BUFFER OVERFLOW, SIMPLY MAKES IT MUCH MORE DIFFICULT TO DO SO