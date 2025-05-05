# Functions

1. Flowchart:   

2. This lab was pretty simple. I didn't really face any major challenges.
3. Code:
```asm
section .data
    even_msg db "Even", 10        ; Message + newline
    even_len equ $ - even_msg     ; Calculate string length

    odd_msg db "Odd", 10
    odd_len equ $ - odd_msg

section .text
    global _start

_start:
    mov eax, 6            ; Change this number to test different values
    call check_even_odd   ; Call the function

    call exit             ; Exit the program

; Function: check_even_odd
; Input: eax = number to check
check_even_odd:
    test eax, 1           ; Bitwise AND operation to check it even or odd
    jz print_even         ; If zero, number is even
    jmp print_odd         ; Else, it's odd

print_even:
    mov eax, 4            ; sys_write
    mov ebx, 1            ; stdout
    mov ecx, even_msg
    mov edx, even_len
    int 0x80
    ret

print_odd:
    mov eax, 4            ; sys_write
    mov ebx, 1            ; stdout
    mov ecx, odd_msg
    mov edx, odd_len
    int 0x80
    ret

exit:
    mov eax, 1            ; sys_exit
    int 0x80
```
