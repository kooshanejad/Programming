# Loops and Arrays
1. Flowchart:   
![Loops and Arrays](https://github.com/user-attachments/assets/9cd5b537-6eea-4676-911c-698838b96635)
2. This lab was honestly pretty challenging at first. I had to make plans of what I needed to do for each task in order to make it easier.
3. Task 1:
```asm
section .text
    global _start

_start:
    mov ecx, 10   ;using ecx as counter register
    xor ebx, ebx  ;clear out ebx

label:
    inc ebx
    loop label

    mov eax, 1    ;exit code
    int 0x80
```

Task 2:
```asm
section .text
    global _start

_start:
    xor eax, eax  ;clear out all registers before us
    xor ebx, ebx
    xor ecx, ecx
    mov eax, 0
    mov ebx, 1
    mov ecx, 10   ;looping 10 times         

label:
    mov edx, eax  ;holding onto previous index
    add eax, ebx  ;ebx + eax
    mov edx, ebx  ;move ebx into edx
    loop label 

    mov eax, 1
    int 0x80
```

Task 3:
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
