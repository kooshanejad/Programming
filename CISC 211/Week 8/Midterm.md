# Midterm

```asm
section .data
    var1 dd 5
    var2 dd 6
    var3 dd 7
    line1 db "Result: ", 0
    len1 equ $ - line1
    result db "0", 0xA
    len_result equ $ - result

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

    mov eax, 4
    mov ebx, 1
    mov ecx, result
    mov edx, len_result
    int 0x80

    mov eax, 1
    int 0x80
```

Table:   
Register    Value   
EAX         7   
EDX         0   

2. Simplify equation: Y = a + b

```asm
section .data
    odd_msg db "odd number", 0
    even_msg db "even number", 0

section .bss
    num resd 1  ; Reserve space for the input number

section .text
    global _start

_start:
    mov eax, [num]    

    ; Divide by 2
    ; If remainder is 0, it's even. If it's 1, it's odd.
    mov ebx, 2        
    div ebx           

    ; check the remainder
    ; If remainder is 0, print "even number"
    jz print_even     ; If it's even, jump to print_even

    ; If it's odd, print "odd number"
    mov eax, 4        
    mov ebx, 1        
    mov ecx, odd_msg  
    mov edx, 11       
    int 0x80          

    ; Exit program after printing "odd number"
    mov eax, 1
    int 0x80

print_even:
    ; If it's even, print "even number"
    mov eax, 4        
    mov ebx, 1        
    mov ecx, even_msg 
    mov edx, 12       
    int 0x80          

    ; Exit program after printing "even number"
    mov eax, 1
    int 0x80 
```
