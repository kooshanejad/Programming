# Quiz 3

```asm
section .data
    space db 0xA    ; newline character

section .bss
    result resb 1

section .text
    global _start

_start:
    mov eax, 5
    mov ebx, eax     ;move eax into ebx to store the variable
    dec eax

loop:
    cmp eax, 1
    jl done         ;jump to done if eax is less than 1
    imul ebx, eax         ;ebx * eax
    dec eax
    jmp loop        ;repeat loop

done:
    mov eax, ebx    ; move 120 into eax
    cmp eax, 9
    jg calculate
    call display_2
    call exit

calculate:
    mov ebx, 10
    div ebx
    push edx     ; save remainder
    cmp eax, 9
    jg calculate
    push eax     ; save quotient

    pop eax
    add eax, 48
    mov [result], eax
    call display

    pop eax
    add eax, 48
    mov [result], eax
    call display

    pop eax
    add eax, 48
    mov [result], eax
    call display

    call linefeed
    call exit

display:
    mov eax, 4
    mov ebx, 1
    mov ecx, result
    mov edx, 1
    int 0x80
    ret

linefeed:
    mov eax, 4
    mov ebx, 1
    mov ecx, space
    mov edx, 1
    int 0x80
    ret

display_2:
    add eax, 48
    mov [result], eax
    call display
    call linefeed
    ret

exit:
    mov eax, 1
    int 0x80
```
