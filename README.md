# dcgenv2
Second version of the decompiled C code of the CGEN.COM from HI-TECH C compiler V3.09

This repository contains the second version of the decompiled C code of the CGEN.COM from HI-TECH C compiler V3.09.

During the initial decompilation, I ran into a number of problems that I could not overcome. Desperate and deciding that this work was beyond my strength, I turned to Mark Ogden for help.

He managed to overcome my problems and I am glad to present a new code with his fixes and comments. Many thanks to Mark Ogden for the bug fixes. He did a great job and put a lot of effort into it.

The second version of the C code for the CGEN.COM was provided to me by Mark Ogden and posted in this repository unchanged.

If you want to compile using Mark Ogden makefile to create a CP/M version you will need to get the patched version zxcc from Tony's site (https://github.com/agn453/ZXCC).  You will also need perl.

Perl script unpack.pl automatically split the cgen.c file so that it can be built with zxcc and the makefile will run with zxcc.

Makefile and unpack.pl should be in a subdirectory relative to the location of the cgen.c and cgen.h files so as not to mess them up when unpacking. 

Note you need patches for zxcc so that the redirect from stdin works for link. Also optim needs to be built on your platform and accessible via PATH.

Since the stripped-down library is not used, then cgen.com (or xcgen.com to avoid problems with assembly), it turns out more of the original.

If you want to compile as a Linux (os x) executable you can just do 

gcc -o xcgen -O3 cgen.c 

Andrey Nikitin   24.12.2021


While testing the capabilities of the recovered first-pass C program code, I found that the cross compiler initializes the bit fields incorrectly. The native Hi-Tech C compiler v3.09 behaved in exactly the same way. Hi-Tech C compiler v3.09 incorrectly initializes the structure of bit fields. The error is present in CGEN.COM.

Program
 
        #include <stdio.h>
 
        struct point {
            unsigned int x:5;   // 0-31
            unsigned int y:3;   // 0-7
        };
 
        struct point center = {2, 5};
 
        int main(void) {
 
            printf("x = %d y = %d\n", center.x, center.y);
            center.x = 2;
            center.y = 5;
            printf("x = %d y = %d\n", center.x, center.y);
            return 0;
        }
 
after compilation and run for execution, it produces different results, although the bit fields are assigned the same values.
 
        x = 7 y = 0
        x = 2 y = 5

A further search for the source of the error showed that the first-pass programs of compilers generated almost identical code, which is then processed by the code generation program. The Hi-Tech C compiler v3.09 code generation program CGEN.COM misinterprets the Intermediate code created by the program P1.COM, and incorrectly generates assembly language code to initialize the bit field structure, which leads to erroneous printing of the first printf statement.

Code generation program CGZ80.EXE HI-TECH Z80 C Compiler 7.80PL2 outputs the correct code in assembly language, that is, in the program CGEN.COM Hi-Tech C compiler v3.09 has an error.

In the restored C code in the sub_808() function, Mark Ogden fixed this error.

Andrey Nikitin   19.08.2022
