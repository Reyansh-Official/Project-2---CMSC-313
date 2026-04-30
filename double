.section .data
    prompt:     .ascii "Enter a number: "
    prompt_len = . - prompt
    result_msg: .ascii "The double is: "
    res_len    = . - result_msg
    newline:    .ascii "\n"

.section .bss
    .lcomm input_buf,  32
    .lcomm output_buf, 32

.section .text
    .global _start

_start:
    mov $1, %rax
    mov $1, %rdi
    lea prompt(%rip), %rsi
    mov $prompt_len, %rdx
    syscall

    mov $0, %rax
    mov $0, %rdi
    lea input_buf(%rip), %rsi
    mov $32, %rdx
    syscall

    xor %rax, %rax
    lea input_buf(%rip), %rsi

atoi_loop:
    xor %rcx, %rcx
    mov (%rsi), %cl
    cmp $'\n', %cl
    je atoi_done
    sub $48, %cl
    imul $10, %rax
    add %rcx, %rax
    inc %rsi
    jmp atoi_loop

atoi_done:
    add %rax, %rax

    lea output_buf(%rip), %rsi
    add $31, %rsi
    movb $0, (%rsi)
    mov %rsi, %r12

itoa_loop:
    dec %rsi
    xor %rdx, %rdx
    mov $10, %rbx
    div %rbx
    add $48, %dl
    mov %dl, (%rsi)
    test %rax, %rax
    jne itoa_loop

    mov %r12, %rdx
    sub %rsi, %rdx
    mov %rsi, %r13
    mov %rdx, %r14

    mov $1, %rax
    mov $1, %rdi
    lea result_msg(%rip), %rsi
    mov $res_len, %rdx
    syscall

    mov $1, %rax
    mov $1, %rdi
    mov %r13, %rsi
    mov %r14, %rdx
    syscall

    mov $1, %rax
    mov $1, %rdi
    lea newline(%rip), %rsi
    mov $1, %rdx
    syscall

    mov $60, %rax
    xor %rdi, %rdi
    syscall
