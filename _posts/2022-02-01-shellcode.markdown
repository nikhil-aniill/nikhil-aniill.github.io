---
layout: post
title:  "Creating a Shellcode to execute /bin/bash"
date: 01-02-2022 12:32:45 +0100
category: Assembly
---
# Creating a Shellcode to execute /bin/bash
```nasm
global _start
section .text
_start:
xor rax, rax
push rax
mov rdx, rsp
mov rbx, 0x68732f6e69622f2f 
push rbx
mov rdi, rsp
push rax
push rdi
mov rsi,rsp
add rax, 59
syscall
```
### Explanation
This is a piece of x86_64 Assembly code written in the AT&T syntax.

It is essentially a shellcode that performs the following actions:

1. XORs the value of register RAX with itself to set its value to zero.
2. Pushes the zero value onto the stack.
3. Moves the stack pointer (RSP) into the RDX register.
    1. Loads the value 0x68732f6e69622f2f (which is the ASCII representation of "/bin//sh") into the RBX register. The value is in little endian format.
4. Pushes the value of RBX onto the stack.
5. Moves the stack pointer (RSP) into the RDI register.
6. Pushes another zero value onto the stack.
7. Pushes the value of RDI (which now points to "/bin//sh") onto the stack.
8. Moves the stack pointer (RSP) into the RSI register.
9. Adds 59 to the value of RAX.
10. Calls the syscall instruction to perform the specified system call (in this case, execve("/bin//sh", 0, 0)).

#### Which registers are used to make a Syscall ?
In x86_64 architecture, the following registers are used to execute a syscall:

- **`rax`**: contains the syscall number, which specifies the desired system call.
- **`rdi`**, **`rsi`**, **`rdx`**, **`r10`**, **`r8`**, **`r9`**: used as arguments to the syscall, depending on the number of arguments required by the specific syscall.
- **`rcx`** and **`r11`** may also be used as additional arguments by some syscalls.

After executing the syscall, the return value is stored in **`rax`**. If the syscall returns an error, the **`rax`** register contains a negative value indicating the error code.