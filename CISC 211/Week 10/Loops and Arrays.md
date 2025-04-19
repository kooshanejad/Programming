# Loops and Arrays

```asm
section .data
    array dd 3, 8, 7, 10  ;array of 4 integers (4 bytes each)

section .bss
    max resd 1            ;reserve space to store max value

section .text
    global _start

_start:
    mov eax, 4            ;array length
    mov ecx, array        ;ecx points to the start of the array
    mov ebx, [ecx]        ;ebx = first element of array (3), assume it's the max 
    mov [max], ebx        ;store first element (3) in max variable
    add ecx, 4            ;move ecx to point to 2nd element 
    dec eax               ;decrement counter

top:
    mov edx, [ecx]        ;move next array element into edx
    cmp edx, [max]        ;compare current element with current max
    jle skip              ;jump to skip if edx is less than or equal to max
    mov [max], edx        ;update max

skip:
    add ecx, 4            ;move to next element
    dec eax               ;decrement counter
    jnz top               ;if there are more elements, jump back to top
 
    mov eax, 1
    int 0x80
```
