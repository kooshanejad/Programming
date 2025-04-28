# Procedures

1. Flowchart:   
![Procedures](https://github.com/user-attachments/assets/25b385d7-f137-44d4-81f7-b8b676fd5d5f)
2. My main challenges were learning how to make use of the push and pop commands as well as making a plan for the code before writing it.
3. Code:
```asm
section .data
    newline db 10      ;newline character

section .bss
    result resb 1      ;reserve one byte for current letter

section .text
    global _start

_start:
    mov eax, 65        ;move 65 (ASCII for A) into eax

loop1:
    mov byte [result], al
    mov ecx, result
    push eax           ;save eax
    call output        ;print character
    pop eax            ;restore eax

    mov ecx, newline   ;ecx = pointer to newline
    push eax
    call output        ;print newline
    pop eax

    inc eax
    cmp eax, 'Z' + 1   ;compare eax with 'Z' + 1
    jne loop1
    call exit

output:
    mov edx, 1         ;output length
    mov ebx, 1         ;stdout
    mov eax, 4         ;system call (sys_write)
    int 0x80
    ret

exit:
    mov eax, 1
    int 0x80
```
