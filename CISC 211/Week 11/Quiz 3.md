# Quiz 3

```asm
section .data 
    num dd 5

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [num] 
    mov ebx, eax     ;move eax into ebx to store the variable
    dec eax 

loop:
    cmp eax, 1
    jl done         ;jump to done if eax is less than 1
    imul ebx, eax   ;ebx * eax        
    mov ebx, eax    ;move result back to ebx
    dec eax
    jmp loop        ;repeat loop
    
done:
    mov [result], ebx

    mov eax, 1
    int 0x80
```
