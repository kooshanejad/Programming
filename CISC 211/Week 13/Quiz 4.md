# Quiz 4

```
section .data
    x dd 3
    y dd 7
    z dd 5

section .bss
    result dd 1

section .text
    global _start

_start:
    call addNumbers
    mov eax, 1
    int 0x80

addNumbers:
    push ebp     ; save base pointer
    mov ebp, esp ; set up new stack frame

    mov eax, [x]
    add eax, [y]
    add eax, [z]
    mov [result], eax

    mov esp, ebp ; restore stack pointer
    pop ebp      ; restore base pointer
    ret
```
