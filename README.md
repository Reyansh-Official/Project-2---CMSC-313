# Project-2---CMSC-313

Overview
double.s is an x86-64 Linux assembly program written in GAS (GNU Assembler) AT&T syntax.
It reads an integer from standard input, doubles it, and prints:
The double is: <result>

Files
FileDescriptiondouble.sx86-64 GAS assembly sourceREADME.mdThis file

Platform
ItemValueArchitecturex86-64OSLinux (gl-server)AssemblerGAS (as)SyntaxAT&T

Build Instructions
bashas -o double.o double.s
ld -o double double.o
No output means success. The executable double is created in the current directory.

Run Instructions
Interactive (type a number, press Enter)
bash./double
Enter a number: 7
The double is: 14
Pipe input
bashecho "21"  | ./double    # The double is: 42
echo "500" | ./double    # The double is: 1000
echo "0"   | ./double    # The double is: 0

How It Works

Print prompt – write syscall (#1) sends "Enter a number: " to stdout.
Read input – read syscall (#0) reads up to 32 bytes from stdin into input_buf.
atoi_loop – Walks the input buffer byte by byte, converting ASCII digits to an integer in %rax (digit = byte - 48, accumulate with *10 + digit). Stops on newline.
Double – add %rax, %rax doubles the value.
itoa_loop – Converts the integer back to ASCII by repeatedly dividing by 10, storing remainders as characters in reverse into output_buf, then printing from the correct start position.
Print result – write syscalls for "The double is: ", the number string, and a newline.
Exit – exit syscall (#60) with status 0.
