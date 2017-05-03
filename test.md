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

## Assembly Language ##

