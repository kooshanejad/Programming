# Mock Midterm

```asm
section .text
    global _start

_start: 
    mov eax, 60
    add eax, 70
    add eax, 90
    add eax, 40
    add eax, 65

    mov ebx, 5
    div ebx

    mov eax, 1
    int 0x80
```
