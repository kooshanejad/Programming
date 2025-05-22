# Project

```asm
section .data
    message     db "HELLO"          ; Plaintext message
    key         db "world"          ; Key (same length)
    msg_len     equ 5               ; Length of both message and key
    out_file    db "output.txt", 0  ; Output file name
    newline     db 10               ; Newline character

section .bss
    fd_out      resd 1              ; File descriptor
    onebyte     resb 1              ; Single reusable byte for writing

section .text
    global _start

_start:
    ; === Create the file ===
    mov eax, 8              ; sys_creat
    mov ebx, out_file
    mov ecx, 0644
    int 0x80
    mov [fd_out], eax

    ; === Write original message ===
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, message
    mov edx, msg_len
    int 0x80

    ; Newline
    call newline_out

    ; === Write key ===
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, key
    mov edx, msg_len
    int 0x80

    ; Newline
    call newline_out

    ; === Encrypt: XOR message + key and write each char ===
    xor esi, esi
encrypt_loop:
    mov al, [message + esi]
    xor al, [key + esi]
    mov [onebyte], al
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, onebyte
    mov edx, 1
    int 0x80
    inc esi
    cmp esi, msg_len
    jl encrypt_loop

    ; Newline
    call newline_out

    ; === Decrypt: XOR encrypted output with key again ===
    xor esi, esi

decrypt_loop:
    mov al, [message + esi]
    xor al, [key + esi]
    xor al, [key + esi]       ; Decrypt again
    mov [onebyte], al
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, onebyte
    mov edx, 1
    int 0x80
    inc esi
    cmp esi, msg_len
    jl decrypt_loop

    ; newline
    call newline_out

    ; Exit
    mov eax, 1
    xor ebx, ebx
    int 0x80

newline_out:
    mov eax, 4
    mov ebx, [fd_out]
    mov ecx, newline
    mov edx, 1
    int 0x80
    ret
```
