.data
A: .word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

.text
main:
li $t0, 0 ## counter starts at 0

la $a3, A ## loading word
li $a1, 2 ## lower boundary of array
li $a2, 8 ## upper boundary of array

arrayLoop:
    bge $a1, $a2, end ## loops until lower boundary reaches upper boundary

    lw $t1, 0($a3)
    andi $t1, $t1, 0x0001 # check if odd leaves 0 if even 1 if odd

    beqz $t1, even ## branches if equal to 0 so even
    addi $t0, $t0, 1 ## if not equal to 0 then odd counter is incremented

    even: 
    addi $a1, $a1, 1 # next array index
    addi $a3, $a3, 4 #next word
    j arrayLoop

end:
addi $a2, $t0, 0 ## result is left in this register

li $v0, 10
syscall