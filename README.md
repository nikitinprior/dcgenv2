# dcgenv2
Second version of the decompiled C code of the CGEN.COM from HI-TECH C compiler V3.09

This repository contains the second version of the decompiled C code of the CGEN.COM from HI-TECH C compiler V3.09.

During the initial decompilation, I ran into a number of problems that I could not overcome. Desperate and deciding that this work was beyond my strength, I turned to Mark Ogden for help.

He managed to overcome my problems and I am glad to present a new code with his fixes and comments. Many thanks to Mark Ogden for the bug fixes. He did a great job and put a lot of effort into it.

The second version of the C code for the CGEN.COM was provided to me by Mark Ogden and posted in this repository unchanged.

If you want to compile using Mark Ogden makefile to create a CP/M version you will need to get the patched version zxcc from Tony's site (https://github.com/agn453/ZXCC).  You will also need perl.

Perl script unpack.pl automatically split the cgen.c file so that it can be built with zxcc and the makefile will run with zxcc.

Note you need patches for zxcc so that the redirect from stdin works for link. Also optim needs to be built on your platform and accessible via PATH.

Since the stripped-down library is not used, then cgen.com (or xcgen.com to avoid problems with assembly), it turns out more of the original.

If you want to compile as a Linux (os x) executable you can just do 

gcc -o xcgen -O3 cgen.c 

Andrey Nikitin   24.12.2021
