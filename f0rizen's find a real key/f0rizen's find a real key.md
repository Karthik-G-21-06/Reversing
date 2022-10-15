# f0rizen's find a real key

## Description
find a real key and recover a flag

[link to site for challenge](https://crackmes.one/crackme/629e1e5833c5d4251e72375f)

## Solution

Firstly I used GDB to get the main function. while reading thorugh the main function and at <main+92> saw eax getting compared to 0x15 or 21. this happens just after calling strlen function that means rax contains the lenght of the input string. from there he code jumps to <main+120> here in <main+134> variable [rbp-0x90] is given value zero and jump to the following statement:

```
<+185>:	add    DWORD PTR [rbp-0x90],0x1
<+192>:	cmp    DWORD PTR [rbp-0x90],0x14
```
which means it is a for loop and the iterative variable is taking values from 0 to 20 which means its doing something to the input value.

now I jumped to radare and checked for human readable strings and found a string "sup3r_s3cr3t_k3y_1337" which is conviniently 21 letters long,also found another set of 21 random letters.

Now i jumped to ghidra and while analysing the decompiled code found that some operation is been done between both the string i found.

from the above picture it is clear that 0x22 is decreased from each letter in the "super secret" ,ASCII wise, and the result of this is XORed with our input to get the other string. So if i just XORed the result and the second string i will get the input. so made this python script which reverse this process.

On running the process u will get a string "flag{_y0upf0undwkey_}". Just change p and w to '_' and u will the key.
