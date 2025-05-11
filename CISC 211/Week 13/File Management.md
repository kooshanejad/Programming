# File Management

```asm
section .data
    file db 'quotes.txt', 0h ; create file

    quote1 db "To be, or not to be, that is the question.", 10
    len1 equ $ - quote1      ; get length of quote1
    quote2 db "A fool thinks himself to be wise, but a wise man knows himself to be a fool.", 10
    len2 equ $ - quote2
    quote3 db "Better three hours too soon than a minute too late.", 10
    len3 equ $ - quote3
    quote4 db "No legacy is so rich as honesty.", 10
    len4 equ $ - quote4

section .text
    global _start
    mov edx, 0644     ; permissions: rw-r--r--
    int 0x80          

    mov esi, eax      ; store file descriptor which allows stdin, stdout, and stderr

    ; write first quote
    mov eax, 4        ; call sys_write()
    mov ebx, esi      ; file descriptor
    mov ecx, quote1   ; pointer to message
    mov edx, len1     ; get message length
    int 0x80

    ; write second quote
    mov eax, 4                   
    mov ebx, esi
    mov ecx, quote2
    mov edx, len2
    int 0x80

    ; seek to end of file before appending quote3 and quote4
    mov eax, 19       ; sys_lseek  
    mov edx, len1     ; get message length
    int 0x80
    mov edx, 2        ; SEEK_END (start counting from end of file)
    ; write second quote
    mov eax, 4                   
    mov ebx, esite3 
    mov ecx, quote2
    mov edx, len2
    int 0x80 quote3
    mov edx, len3
    ; seek to end of file before appending quote3 and quote4
    mov eax, 19       ; sys_lseek  
    mov ebx, esi      ; file descriptor
    mov ecx, 0        ; offset 0    
    mov edx, 2        ; SEEK_END (start counting from end of file)
    int 0x80 quote4
    mov edx, len4
    ; append quote3 
    mov eax, 4
    mov ebx, esi
    mov ecx, quote3   ; sys_close
    mov edx, len3
    int 0x80

    ; append quote4
    mov eax, 4
    mov ebx, esi
    mov ecx, quote4
    mov edx, len4
    int 0x80

    ; close file
    mov eax, 6        ; sys_close
    mov ebx, esi
    int 0x80

    ; exit program
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
