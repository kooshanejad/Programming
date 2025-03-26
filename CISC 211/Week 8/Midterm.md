# Midterm

```asm
section .data
    var1 dd 5
    var2 dd 6
    var3 dd 7
    line1 db "Result: ", 0
    len1 equ $ - line1

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [var1]
    add eax, 2      ; eax = var1 + 2
    mov ebx, [var3]
    sub ebx, [var2] ; ebx = var3 - var2
    cdq
    idiv ebx
    mov [result], eax

    ; print result    
    mov eax, 4
    mov ebx, 1
    mov ecx, line1
    mov edx, len1
    int 0x80

    mov eax, 1
    int 0x80
```
