# Logical Instructions

1. Flowchart:   
![Logical Instructions](https://github.com/user-attachments/assets/fc75a769-3601-4d95-a75b-1d7cbb7b8fad)
2. I did not really struggle with this lab. It was pretty easy.
3. Code:
```asm
section .data
    x dd 5

section .bss
    result resd 1

section .text
    global _start

_start:
    mov eax, [x]
    xor eax, eax
    mov [result], eax

    mov eax, 1
    int 0x80
```
