# Conditional Instructions

1. Flowchart:   

2. My main challenge in performing this lab was making a plan of what I needed to do to compare the numbers and find the largest one.
3.
```asm
section .data
    num1 dd 2
    num2 dd 4
    num3 dd 8
    num4 dd 12
    num5 dd 20

section .bss
    largest resd 1

section .text
    global _start

_start:
    mov eax, [num1]     ;move num1 (2) to eax
    mov [largest], eax  ;move eax (2) to largest
    mov ebx, [num2]     ;move num2 (4) to ebx
    cmp ebx, [largest]  ;compare num2 (4) with largest (2)
    jle part2           ;jump to part2 if ebx (4) is less than or equal to largest (2)
    mov [largest], ebx  ;move ebx (4) to largest

part2:
    mov ebx, [num3]     ;move num3 (8) to ebx
    cmp ebx, [largest]  ;compare ebx (8) with largest (4)
    jle part3           ;jump to part3 if ebx (8) is less than or equal to largest (4)
    mov [largest], ebx  ;move 8 to largest

part3:
    mov ebx, [num4]     ;move num4 (12) to ebx
    cmp ebx, [largest]  ;compare ebx (12) with largest (8)
    jle part4           ;jump to part4 if ebx (12) is less than or equal to largest (8)
    mov [largest], ebx  ;move 12 to largest

part4:
    mov ebx, [num5]     ;move num5 (20) to ebx
    cmp ebx, [largest]  ;compare ebx (20) with largest (12)
    jle exit            ;jump to exit if ebx (20) is less than or equal to largest (12)
    mov [largest], ebx  ;move 20 to largest

exit:
    mov eax, 1
    int 0x80
```
