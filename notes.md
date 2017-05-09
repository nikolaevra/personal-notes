There are slides to the course that the prof used to use a lot before. However, this time he is not 
going to use the slides in the class anymore, he will do more blackboard stuff explaining everything 
on the board

He will assign a pre-lecture reading to students to be more productive in class


# CS 241 #

You have 3 release tokens, each token has 12 hours cool down

Assignments:
        25%
Midterm:
        25% written on Wednesday on June 21, 7:00-8:20pm
Final Exam:
        50% written sometime in August

Instructors:
        Dan Holtby djholtby@ueaterloo.ca
        Kevin Lanctot kevin.lanctot@uwaterloo.ca
ISA:
        Pierre-Louis Guidez cs241@ueaterloo.ca

This week's tutorial is a review of C++

## Purpose of a course ##

* A compiler is a program that reads a program and writes another program

* Foundations of Sequential Programs:
        - What really happens when i compile and run a program?
        - By the end of the course, there should be very little mystery left about
        computers or computer programs

* What is a computer? (to learn more, take CS250)
    - CPU
        - Control Unit `brain of the CPU`
        - ALU Arithmetic-Logic Unit `the thing that knows how to add numbers and compute boolean logic`
        - Memory Unit `talks to the RAM`
        - Registers `very fast, very little memory we will use registers to write machine code just a much of transistors`
        - Magic Smoke
    - RAM
        - Just a bunch of bytes

* What is a compiler?
    - Input (C++ )
        - program written in C++, sequence of ASCII characters
        - Its fed into a scanner
            - Scan thought the text and turn it into tokens // sometimes its
            // called a tokenizer or lexer
            - Scanner returns c++ tokens
        - Next, everything goes into a parser
            - Parser analyzes lines of code and breaks it into a tree of commands
            and subcommands
            - returns a tree of the entire program
        - Next we have to make sure that the tree makes sense
            - check code for errors, make sure commands can be executed
            - S.V. Semantic Validation. Making sure you are following the rules
            of the language. You already checked the syntax rules of programming
            language, but now you have to make sure that it makes sense
            - returns tree++, you have the same tree, but annotated with with
            extra information and details
        - CodeGen
            - Traversing the tree and generating machine code
            - Generate assembly language -> compile assembly language
            - Still need linker to use multiple files
        - Output (Machine Code)
            - program written in Machine code
        `If all goes right, the output/input is the same program or atleast behaves the same way`

* What is Machine Language?
    - von Neumann Architecture
        - programs are stored in the same memory as data
    - Machine specific language
    - Binary
        - easy for computers to read, but not humans

* What is Binary Data?
    - means base 2, everything is 0 or 1
    - bit is short for binary digit
        - byte is 8 bits
        - nibble is 4 bits

* What does `0110 1010` mean?
    - it could be ab 8bit integer `64 + 31 + 8 + 2 = 106`
* What does `1111 0001` mean?
    - means `128 + 64 + 32 + 16 + 1 = 241`

* How do we deal with negatives in binary?
    - In binary -42 => does not equal to `-0010 1010`
    we have to use a bit to represent the negativity so instead of using 8 bits
    to represent a number, we use 7 bits and the leading number represents
    negativity
    - `(1)010 1010` // in this case the first 1 represent minus
    - this is called signed magnitude method
    - so for 32-bit number 31 bits is a number and 1 bit is magnitude

**One's Compliment**: (meaning that you change ones to ones compliments, which is 0)
```
 0                                  |                                    255
 |----------------------------------|-------------------------------------|
 0                              127 | -0                                -127
```
This creates a problem because you will need different hardware for signed and
unsigned bytes

So we have `42 = 0010 1010` We flip all of the bits and we get `42 = 1101 0101`

```
But now since we flipped everything, it looks more like this:
 0                                                                       255
 |----------------------------------|-------------------------------------|
 0                              127 | -127                               -0
```
So if we have `-2 + 3` we move from `-2 -> -1 -> -0 -> 0 -> 1` // we need 4 steps to get 1
// which is a problem because because we still can't use the same hardware

**Two's Compliment:**
You flip all of the bits, but also add 1 to the magnitude
```
 0                                                                       255
 |----------------------------------|-------------------------------------|
 0                              127 | -128                               -1
```
Now `-2 + 3`, we move from `-2 -> -1 -> 0 -> 1` // we only need 3 steps
So we can recycle hardware for addition and subtraction

Lets look at this number:
- if this is our two's complement `1100 1000`
- to find its magnitude:
we have to flip all bits => `0011 0111` and you have to add 1 to account for
negativity, which is a lot of work
- instead, we start from the end and keep all of the 0s and the first 1 the same
and flip everything  after that
- so `1100 1000 => 0011 1000`

<a src="https://youtu.be/lKTsv6iVxV4">
Here is a video that will explain this all signed/unsigned business in greater detail
</a>

## Characters ##

We use ASCII
        - there are many ways to encode stuff, but most popular is UTF
        - utf-32, means that 1 to 32-bits per code point
        - utf-16, means that 1 to 16-bits per code point
        - utf-8, means that 1 to 8-bits per code point. All ASCII characters are
        the same in utf-8

Hexadecimals:
- Binary sucks, good for computers and bad for humans
- its too long and slow to read
- hexadecimal is base 16, so `241 == 1111 0001 == 0xF1`
> in this case out binary number is unsigned, so leading 1 does not imply negativity

Maybe more examples?
- In computer every file is a sequence of bits, usually arranged into bytes
    - in Linux, you can easily see bits and bytes
    - in Windows you will suffer
	
Program called xxd:
- xxd foo.c will print the whole file in hex and the string in ASCII line by line
> if something is not printable at all, it will give you a dot .
	
- xxd -c 4 foo.c // will dump data with 4 bytes per line
> by default it will dump in hex and 10 bytes per line

`you never know what a byte means in a file if you don't know what the file is`
  
## CPU ##
<img src="http://www.it4nextgen.com/wp-content/uploads/2017/01/cpu-block-diagram.png">

* CU - Control Unit
* ALU - Arithmetic-Logic Unit
* MEM - Memory
* IR - Instruction Register
* RAM - Random Access Memory
* Registers - general purposes registers from `$0` to `$31`

Data Path:
1) `PC` holds the address of the current instruction
2) `IR` holds the instruction that is being executed
3) `ALU` performs the arithmetic and logic operations
4) General Purpose registers temp storage in processor

Program is stored in `RAM`, then the `CU` is taking program from `MEM` 
and puts it into a `IR`. 

* MIPS has 18 instructions
    - 2 basic formats and we will have a cheat sheet to remember them
 
* Registers:
     - `$0` is read-only 
     - `$31` is supposed to be used for a return address
     - There are also 2 types of registers in our machine:
        + we actually have two types of registers low and high, because we need to store the result and the remainder in division
        + also we need to store result of the multiplication inside 64 bits, so we need 2 32-bit registers
     - **Note:** in Assembly, we have one instruction for add / subtract
     - But for multiply and divide we have 2 different versions for unsigned and signed values

## Hexadecimal Numbers ##
Long string of binary is very hard to read and remember, so people came up with grouping numbers in groups of 4.
- So each of those groups of 4 will be replaced with a decimal #
- but we want to use #s from 0 - 9 so that we don't reuse numbers like 12 (where 1 can be a # on its own and 2 can be a separate # too)
- So instead we introduce 6 letters from `a` to `f`
- now we have a variety, because we can use capital and lower case letters, both will work
- we also specify that we have a a hex value, by adding a `0x` at the beginning
- There is a table in the notes that can help you understand each conversion
- Hex is like a compromise between human's decimal understanding and computers binary understanding

> Why does hex not need to work with negative/positive?
- because hex does not care if your # is +/-, its just a bunch of #s (i.e. 0s and 1s)
- hex does not know what the binary sting mean, it just encodes it nicely
 
## Data Representation ##
* Bit:
    - a single 1, 0
* Nibble:
    - 1 hex digit = 4 bits
* Byte:
    - 2 hex digits = 8 bits
    - 1 char (in utf-8)
* Word:
     - in a x32 bit architecture, there is 32-bits per word
     - in a x64 bit architecture, there is 64-bits per word `// so we can transfer 64-bit long words at a time`
 
## ASCII ##
* Developed after teletype.
     - they used machines and radio waves to send out messages.
     - each letter on the keyboard needed its own encoding
     
> When computers were developing, and they needed a way to store text, they just
> reused the teletype keyboard characters

To store a character from ASCII, we need 7 bits.

The biggest limitation of ASCII is that there is a language limitation
 - so one day a guy came along as asked can we have a single standard for every country?
 - yes, they invented the magical utf-8 (8 bits instead of 7 for extra characters)
 - 1 extra bit adds so many more options, since they are like left most bits

* ASCII for next line is:
    - Linux: `\n`
    - Windows: `\r\n`
    
> That's why text files have different encoding in linux and Windows and marmoset is often complaining

* Unicode:
    - currently has 110000 characters from 100 scripts
 
> Some other high-level languages like python use unicode, but we will be using ASCII in this course

## MIPS Assembly Language ##
* References: CO&D chapter 2 instructions: Language of the Compiler

Link: <a src="https://www.student.cs.uwaterloo.ca/~cs241/mips/mipsasm.html"> MIPS Tutorial </a>

* High Level Languages:
     - C++, Racket, Python
     - Meant to make it as conveniently as possible to read code
     - meant to be process independent, where it will compile appropriately for each machine
* Assembly Language:
     - MIPs, ARMv7
     - compromise between `HLL` and `MC`
     - one statement in `AL` means to one statement in `MC`
     - can run assembly on multiple processors by using a simulator
    - used for device drivers like hard-drive driver, cdRom driver
* Machine Code:
     - sequence of 0s and 1s
     - meant to be executed by computer
     - uses 0, 1s to make it as convenient for computers as possible
     - processor dependent, meant to be convenient to a specific computer
     - also called machine language

> Just like in numbers, we leave a comma after ever 3 digits, we will add a space between every 4 bits

* What is MIPS?
    - one particular family of processors
    - we are doing word size of 32 bits

## C++ vs. MIPS ##
* C++:
```
a = 10;
b = 15;
c = a + b;
```

MIPS:
```
lis $5         // load the next word into register 5
.word 0xa      // a is a hexadecimal for 10
lis $7         // load the next word into register 7
.word 0xf      // f is a hex for 15
add $3, $5, $7 // addition operation
jr $31         // return result destination
```

Assembly language is one statement per line

## MIPS language ##

* Design Principle 1:
    - Simplicity favors regularity   
* Design Principle 2:
    - Smaller is faster
* Design Principle 3:
    - Make the common case fast
* Design Principle 4:
    - Good design demands good compromises

> Arithmetic operations my occur on the registers, that's why in MIPS you must include instructions to transfer 
> date between memory and registers. Those operations are called data transfer instructions

* To access a word in memory, you must supply the memory address, which is just like a long one dimensional array
    - Memory's locations start with 1 and go on until you run out of memory
    - The operation of getting something from memory is called **load**

> Example: Compiling an assignment when an operand is in memory. Assume characters g, h are in `$s1` and `$s2` respectively
> and the starting address of the array is in `$s3`.
 
C code:
```
 g = h + A[8];
``` 
MIPS code:
```
 # We know that one of the operands is in memory and we have to load it.
 lw $t0,32($s3)       # Temporary reg $t0 gets A[8]
 # we entered 32 above and not 8, because we have 8 * 4 = 32
 add $s1,$s2,$t0     # g = h + A[8]
```

> In MIPS, words must start at address that is multiples of 4. This requirement is called *alignment restriction*.
> Meaning that data has to be aligned in memory on natural boundaries

*So apparently, alignment restriction allows for faster data transfers.... maybe something related to the channel of transfer?*

What if we want to write into memory now?

C code:
```
A[12] = h + A[8]
```
MIPS code:
```
lw $t0,32($s3)       # Temporary reg $t0 gets A[8]
add $t0,$s2,$t0      # Temporary reg $t0 gets h + A[8]

# now we have to save this ting (it's all habibis ting)
sw $t0,48($s3)       # storing result of calculation in A[48] (4*12 = 48)
```

Often, programs have more variables than computer has registers in that case, the compiler tries to store most frequently used
variables in registers and the rest in the memory.

* Constant or immediate operands

> Example: Add the constant 4 to register $s3
```
lw $t0, AddrConstant4($s1)   # $t0 = constant 4
add $s3,$s3,$t0              # $s3 = $s3 + $t0 ($t0 == 4)
```
> Note: here we are assuming that our constant is already loaded into memory

Another approach could be using `addi` command, which stands for immediately add
```
addi $s3,$s3,4     # $s3 = $s3 + 4
```


### Translating MIPS into machine code ###
* Since registers re referred by almost all instruction there must be a convention to map those registers to numbers
    - registers `$s0 - $s7` map onto registers `16 - 23`
    - registers `$t0 - $t7` map onto registers `8 - 15`
    
Example:
```
add $t0,$s1,$s2
```
Now we convert to binary MIPS representation
```
0000 0010 0011 0010 0100 0000 0010 0000 
```
| 6-bits  | 5-bits | 5-bits | 5-bits | 5-bits | 6-bits |
|:-------:|:------:|:------:|:------:|:------:|:------:|
| 000000  | 10001  | 10010  | 01000  | 00000  | 100000 |
| Tells MIPS that this is an addition operation | Denotes the # of register `$s1 = 17 = 10001`, which is the first source operand | Denotes the # of register `$s2 = 18 = 10010`, which is the second source operand | Denotes the # of register `$t0 = 8 = 01000`, which receives the result | Unused in this instruction, so its set to 0 | Tells MIPS that this is an addition operation |

> Note that the size of the instruction is exactly 32-bit long, which is caused by the length of the word

! **WARNING:** Entering territory of mind blowery !
 > Since we do not want to write these long strings of 0s and 1s, we are going to use HEX instead. Hex works nicely in computers because each group of 4-bit binary digits can be easily encoded in a 16-bit hex digit

MIPS fields are given names to make them easier to read and stuff:

| 6-bits  | 5-bits | 5-bits | 5-bits | 5-bits | 6-bits |
|:-------:|:------:|:------:|:------:|:------:|:------:|
| 000000  | 10001  | 10010  | 01000  | 00000  | 100000 |
| op - basic operation of the instruction (opcode) | rs - the first register source operand | rt - the second register source operand | rd - the register destination operand | shamt - shift amount (will be discussed later) | funct - function or function code. Selects the specific variant of the operation in the op field |

We have a problem here though. Sometimes we want to have longer operations because we have to use larger numbers then 32.
> For example: the load word instruction must specify 2 registers and a constant. Since we are constrained to a 5-bit value, we can only load a value up to 32. The constant is used to select elements from arrats or data structures, which means we will often need values more then 32.

This is where the Design principle #4 kicks in:
*(Good Design demands good compromises)*

The solution was to make all instructions the same length, but require different kinds of instruction formats for different kinds of instructions

> For example: the format we discussed before is called R-type, but there is also I-type. The fields of the I-type are:

| 6-bits  | 5-bits | 5-bits | 16-bits |
|:-------:|:------:|:------:|:------:|
| op | rs | rt | constant or address |

I-type command in MIPS will now look like this:
```
lw $t0,1200($s3)         ; Temporary reg $t0 gets A[300]
; Note how we are using 1200 to get arr value of 300, because remember memory alignment restriction?
```
<a scr="https://en.wikipedia.org/wiki/Data_structure_alignment">if not, check this link out to learn more about alignment restriction </a>

And the same command in machine code will look like this:
```
1000 1101 0010 1000 0000 0100 1011 0000
```

### Logical Operations ###
Logical operations include operations such as shift left `sll`, shift right `srl`, bit-by-bit AND `and, andi`, bit-by-bit OR `or, ori`, bit-by-bit NOT `nor`.

**Shift left example:**
```
0000 0000 0000 0000 0000 0000 0000 1001 = 9 
; after calling sll command, we get
0000 0000 0000 0000 0000 0000 1001 0000 = 144 
```

> Another example
```
sll $t2,$s2,4     # reg $t2 = reg $s0 << 4 bits
# so we are shifting value from $t2 into $s2 and we are shifting it by 4 bits
# we can easily calculate the new value because shifting by 4 bits tot he left is like myltiplying by 2^4 (or 16)
```

Also, we can now define what `shamt` stands for in our machine functions field. It means the shift amount

**And example:**
```
register $t2 = 0000 0000 0000 0000 0000 1101 1100 0000
register $t1 = 0000 0000 0000 0000 0011 1100 0000 0000
and $t0,$t1,$t2  # reg $t0 = reg $t1 & reg $t2
register $t0 = 0000 0000 0000 0000 0000 1100 0000 0000
```
Look at it like its a table, if both registers have 1 => result will have 1 too at that binary location

**Or example:**
```
register $t2 = 0000 0000 0000 0000 0000 1101 1100 0000
register $t1 = 0000 0000 0000 0000 0011 1100 0000 0000
or $t0,$t1,$t2  # reg $t0 = reg $t1 | reg $t2
register $t0 = 0000 0000 0000 0000 0011 1101 1100 0000
```

**Not Example**
```
register $t2 = 0000 0000 0000 0000 0000 0000 0000 0000
register $t1 = 0000 0000 0000 0000 0011 1100 0000 0000
nor $t0,$t1,$t2  # reg $t0 = ~ (reg $t1 | reg $t3)
register $t0 = 1111 1111 1111 1111 1100 0011 1111 1111
```

### Instruction for making decisions ###
**beq example**
```
beq register1, regiter2, L1
```
means to go to the statement labeled L1 if the value in register1 equals the value in register2

**bne example**
```
bne register1, regiter2, L1
```
means to go to the statement labeled L1 if the value in register1 does not equal the value in register2

> Big Example boys:

Lets say you want to rewrite this in MIPS:
```
if (i == j) {
    f = g + h;
} else {
    f = g - h;
}
```

Note: our code will be more efficient if we test for the opposite condition to branch over the code that performs the *then* part of the *if*.

```
bne $s3,$s4,Else # go to else if i != j
add $s0,$s1,$s2  # f = g + h (skipped if i != j)
j Exit # go to (jump) to Exit
Else:sub $s0,$s1,$s2    # f = g - h (skipped i == j)
Exit:
```

**LOOPS**
```
while (save[i] == k) {
    i += 1;
}
```
In MIPS: Assume that `i` and `k` corresponds to registers `$s3` and `$s5` and the base of the array save is in `$s6`
```
Loop: sll $t1,$s3,2    # Temp reg $t1 = i * 4. Remember how shifting left multiplies, in our case it multiplies by 4, 
                       # which is what we need to traverse array, since we have to remember about alignment problem
    add $t1,$t1,$s6    # $t1 = address of save[i]
    lw $t0,0($t1)      # temp reg $t0 = save[i]
    bne $t0,$s5,Exit   # go to exit if save[i]!=k
    addi $s3,$s3,1     # i = i + 1
    jr Loop             # go to Loop
Exit:
```
## Lecture 3: Assembly language ##
Going over the MIPS reference sheet:
<a src="https://www.student.cs.uwaterloo.ca/~cs241/mips/mipsref.pdf">MIPS reference sheet</a> 

> Note: in branching commands, the `pc` is incremented before the equality comparison is completed, so that by the time 
> the comparison is done, we already have a complete incremented `pc`

In many commands, the destination comes first and then teh two variables which are used to perform the operation. 
This is done so that we have a similar order as in the regular notation `x = y + z` where destination is first and the 
two variables come after

* Review:
    * Our MIPS has 18 instructions:
    * CPU contains 32 `32-bit` registers
    * `cs241.wordasm` is used to create binary files
    * `mips.twopoints` to start MIPS machine
    
* Special purpose registers:
    * `$0` - read only register contains the value 0 always. Very useful for `beq` and `bne` commands. Very useful for a copy instruction, we can just `add $3, $7, $0`. This way we put the value of register `$7` into register `$3`
    * `$30` - Stores the end of your memory. You can also use it as stack because you `started from the bottom` and go `all the way up`
    * `$31` - stores the return address
    * `$29` - is also special, but we will cover it later

> Question: `Can we translate directly from assembly to hex? Or do we go to binary first and then to hex?`

> Example: `add 2 numbers and put them into register 9`
```
add $9, $5, $7 ; = 0000 0000 1010 0111 0100 1000 0010 0000 = 0x00a74820 // note, you dont have to include the 0s between 0x and a
jr $31         ; = 0x03e00008
```
> Note: `Leading 0s between 0x and first any non-zero values can be ignored and they don't change the actual value`

> Example: `Get value from register $1 and put it's absolute value in register $3`
```
; $1 - x
; $3 - |x|
; $4 - flag
; Good style to document things

add $3,$1,$0  ; moving to $3 is purely for convenience
slt $4,$3,$0
beq $4,$0,1
sub $3,$0,$3
jr $31
```

The logic could have been done with `Labels`.
```
; $1 - x
; $3 - |x|
; $4 - flag
; Good style to document things

add $3,$1,$0  ; moving to $3 is purely for convenience
slt $4,$3,$0
beq $4,$0,return
sub $3,$0,$3
return:
jr $31
```
> Question: `Can we use labels when encoding into hex?`

> Answer: `No, we can't usually when we use assembler it does the work for us of changing labels into the address of the 
next instruction after the label`

> Note: `Labels are litt fam!`

> Error notes: `Unaligned access- memory reads have to be aligned, and unaligned access means that its trying to read something that is not divisible by 4`

The thing with branching, is you never want to branch by `-1`, that will make an infinite loop

Lets make a loop now:
> Example: `Add numbers 1 through 13 and put it into register $3`
```
; $1 == 1
; $2 == i
; $3 : return value

lis $1
.word 1
lis $2
.word 13
add $3,$0,$0 ; we can't assume that registers are initialized. 
             ; In our env. it will work, but in others, it might not
loop:
    beq $2,$0,end
    add $3,$3,$2
    sub $2, $2, $1
    beq $0,$0,loop
end:
    jr $31
```

