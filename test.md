http://www.student.cs.uwaterloo.ca/~cs245

There are slides to the course that the prof used to use a lot before
however this time he is not going to use the slides in the class anymore, 
he will do more blackborad stuff explaining everyhing on the board

He will assign a prelecture reading to students to be more productive in class


---------------------------------------CS 241-----------------------------------

You have 3 release tokens, each token has 12 hours cooldown

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
                - Control Unit // brain of the CPU
                - ALU Arithmetic / Logic Unit // the thing that knows how to add numbers
                and compute boolean logic
                - Memory Unit // talks to the RAM
                - Registers // very fast, very little memory
                // we will use registers to write machine code
                // just a much of transistors
                - Magic Smoke
        - RAM
                - Just a bynch of bytes

* What is a compiler?
        - Input (C++ )
                - program written in C++, sequense of ASCII characters
                - Its fed into a scanner
                        - Scan throught the text and turn it into tokens // sometimes its
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
                        - Generate assebly language -> compile assembly language
                        - Still need linker to use multiple files
        - Output (Machine Code)
                - program written in Machine code

        // If all goes right, the output/input is the same program or atleast
        // bahves the same way

* What is Machine Language?
        - von Neumann Architecture
                - programms are stored in the same memory as data
        - Machine specific language
        - Binary
                - easy for computers to read, but not humans

* What is Binary Data?
        - means base 2, everything is 0 or 1
        - bit is short for binary digit
                - byte is 8 bits
                - nibble is 4 bits

* What does 0110 1010 mean?
        - it could be ab 8bit integer 64 + 31 + 8 + 2 = 106
* What does 1111 0001 mean?
        - means 128 + 64 + 32 + 16 + 1 = 241

* How do we deal with negatives in binary?
        In binary -42 => does not equal to -0010 1010
        we have to use a bit to represent the negativity so isntead of using 8 bits
        to represent a number, we use 7 bits and the leading number represents
        negativity
        - (1)010 1010 // in this case the first 1 represent minues
        - this is called signed magnitude method
        - so for 32 bit number 31 bits is a number and 1 bit is magnitude

One's Compliment: (meaning that you change ones to ones compliments, which is 0)
 0                                                                       255
 |----------------------------------|-------------------------------------|
 0                              127 | -0                                -127

This creates a problem because you will need different hardware for signed and
unsigned bytes

So we have
 42 = 0010 1010
We flip all of the bits
 42 = 1101 0101

But now since we flipped everything, it looks more like this:
 0                                                                       255
 |----------------------------------|-------------------------------------|
 0                              127 | -127                               -0

So if we have -2 + 3 we move from -2 -> -1 -> -0 -> 0 -> 1 // we need 4 steps to get 1
// which is a problem because becasue we still can't use the same hardware

Two's Compliment:
You flip all of the bits, but also add 1 to the magnitude

 0                                                                       255
 |----------------------------------|-------------------------------------|
 0                              127 | -128                               -1

Now -2 + 3, we move from -2 -> -1 -> 0 -> 1 // we only need 3 steps
So we can recycle hardware for addition and subtraction

Lets look at this number:
        - if this is our two's complement 1100 1000
        - to find its magnitude:
        we have to flip all bits => 0011 0111 adn you have to add 1 to account for
        negativity, whcih is a lot of work
        - instead, we start from the end and keep all of the 0s and the frist 1 the same
        and flip everything  after that
        - so 1100 1000 => 0011 1000

## Characters ##

We use ASCII
        - there are many ways to encode stuff, but most popular is UTF
        - utf-32, means that 1 to 32-bits per code point // character
        - utf-16, means that 1 to 16-bits per code point
        - utf-8, means that 1 to 8-bits per code point. All ASCII characters are
        the same in utf-8

Hexadecimals:
        - Binary sucks, good for computers and bad for humans
        - its too long and slow to read
        - hexadecimal is base 16, so 241 == 1111 0001 == 0xF1
        // in this case out binary number is unsigned, so leading 1 does not imply negativity

Maybe more exmaples?
	In computer every file is asequence of bits, usualyl arranged into bytes
 - in Linux, you can easily see bits and bytes
 - in Windows you will suffer
	
Program called xxd:
 - xxd foo.c will print the whole file in hex and the string in ASCII line by line
	// if something is not printable at all, it will give you a dot .
	
 - xxd -c 4 foo.c // will dump data with 4 bytes per line
 `// by default it will dumpp in hex and 10 bytes per line`
 
 `you never know what a byte means in a file if you dont know what the file is`
  
## CPU ##

cpu image: <a src="http://imgur.com/MC4yMA6">CPU Diagram</a>

* CU - Control Unit
* ALU - Arithmetica / Logic Unit
* MEM - 
* IR - instruction register
* RAM - Random Access Memory

Program is stored in `RAM`, then the `CU` is taking program from `MEM` 
and puts it into a `IR`. 

* MIPS has 18 instructions
 - 2 basic formats and we will have a cheat sheet to remember them
 - 
 
* Registers:
 - 0 is read-only 
 - 31 is supposed to be used for a return address
 - There are also 2 types of registers in our machine:
 	+ we actually have two types of registers low and high, because we need the 
 		result and the remainder in devision
 	+ also we need to store result of the multiplication inside 64 bits, so we need
 		2 32 bit registers

 - Note in Assembly, we have one struction for add / substract
 - But for multiply and divide we have 2 different versions for unsigned and signed
values

## Hexadecimal Numbers ##
* Long string of binary is very hard to read and remember, so people came up with
	grouping numebrs in groups of 4.
 - So each of those groups of 4 will be replaced with a decimal #
 - but we want to use #s from 0 - 9 so that we dont reuse numbers like 12 (where 1 can be a # on its own and 2 can be a separate # too)
 - So instead we intoroduce 6 letters from `a` to `f`
 - now we have a variety, becuase we can use capital and lower case letters, both will work
 - we also specify that we havea a hex value, by adding a `0x` at the beginning

 + There is a table in the notes that can help you understand each onversion
 + Hex is like a compromize between human's decimal undesrtanding and computers binary understanding

Why does hex not need to work with negative/postive?
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
 - in a x64 bit architecture, there is 64-bits per word
 `so we can transfer 64 bits long words at a time`
 
## ASCII ##
Developed after teletype.
 - they used machines and radio waves to send out messages.
 - each letter on the keyboard needed its own encoding
 
When computers were developing, and they needed a way to store text, they just
reused the teletype keyboard characters

To store a character from ASCII, we need 7 bits.

The biggest limitation of ASCII is that there is a language limitation
 - so one day a guy came along as asked can we have a single standart for every country?
 - yes, they inveneted the magical utf-8 (8 bits instead of 7 for extra characters)
 - 1 extra bit adds so many more options, sicne they are like left most bits

ASCII for next line is:
 - Linux: `\n`
 - Windows: `\r\n`
Thats why text files have different encoing in linux and Windows and marmoset is often complaining

Unicode:
 - currently has 110000 characters from 100 scripts
 
Some other high-level languages like python use unicode, but we will be using ASCII in this course

## MIPS Assembly Language ##
* References: CO&D chapter 2 instructions: Language of the Compiler
 /~cs241/mips

High Level Languages:
 - C++, Racket, Python
 - Meant to make it as conveniently as possible to read code
 - meant to be process independed, where it will compile appropriately for each machine
Assembly Language:
 - MIPs, ARMv7
 - compromise between HLL and MC
 - one statement in AL maos to one statement in MC
 - can run assembly on multiple processors by using a simulator
 - used for device drivers like hardrive driver, cdRom driver
Machine Code:
 - sequence of 0s and 1s
 - meant to be executed by computer
 - uses 0, 1s to make it as convenient for computers as possible
 - processor dependednt, meant to be convenient to a specific computer
 - also called machine language

Just like in numbers, we leave a comma after ever 3 digits, we will add a space between every 4 bits

What is MIPS?
 - one particular family of processors
 - we are doing word size of 32 bits

## C++ vs. MIPS ##
C++:
a = 10;
b = 15;
c = a + b;

MIPS:
lis $5 => load the next word into register 5
.word 0xa => a is a hexadecimal for 10
lis $7 => load the next word into register 7
.word 0xf => f is a hex for 15
add $3, $5, $7 => addition operation
jr $31 => return result destination

Assembly language is one statement per line 

## What is Machine Code? ##
- binary code
- directly executed by processor







