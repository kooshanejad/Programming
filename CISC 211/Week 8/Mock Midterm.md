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

Convert 575 Decimal into Binary:

575 ÷ 2 = 287 remainder 1   
287 ÷ 2 = 143 remainder 1   
143 ÷ 2 = 71 remainder 1   
71 ÷ 2 = 35 remainder 1   
35 ÷ 2 = 17 remainder 1   
17 ÷ 2 = 8 remainder 1   
8 ÷ 2 = 4 remainder 0   
4 ÷ 2 = 2 remainder 0   
2 ÷ 2 = 1 remainder 0   
1 ÷ 2 = 0 remainder 1   

Result: 1000111111

Convert 575 Decimal into Hexadecimal:

575 ÷ 16 = 35 remainder 15 (F in hexadecimal)   
35 ÷ 16 = 2 remainder 3   
2 ÷ 16 = 0 remainder 2   

Result: 0x23F

Convert -10 into binary using 1's and 2's complements:

1's complement:   
10 in binary: 00001010   
Invert: 11110101   
Result: 11110101   

2's complement:   
Add one to 11110101:   
Result: 11110110   

Transfer bits into cache memory:   
Index: 0, V: 1, Tag: 10111   
Index: 1, V: 1, Tag: 10000   
Index: 2, V: 1, Tag: 11101
