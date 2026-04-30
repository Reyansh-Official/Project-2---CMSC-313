# Project-2---CMSC-313

**Overview**

double.s is an x86-64 Linux assembly program that reads an integer from standard input, doubles it, and prints: The double is: result 

**Build Instructions**

as -o double.o double.s
ld -o double double.o

**Run Instructions**

./double

**How It Works**

1. Print prompt – write syscall (#1) sends "Enter a number: " to stdout.
2. Read input – read syscall (#0) reads up to 32 bytes from stdin into input_buf.
3. atoi_loop – Walks the input buffer byte by byte, converting ASCII digits to an integer in %rax. Stops on newline.
4. Double – add %rax, %rax doubles the value.
5. itoa_loop – Converts the integer back to ASCII by repeatedly dividing by 10, storing remainders as characters in reverse into output_buf, then printing from the correct start position.
6. Print result – write syscalls for "The double is: ", the number string, and a newline.
7. Exit – exit syscall (#60) with status 0. 
