Commands to debug a c source file using GDB:
1. Compile source file gcc -g -o test1 test
2. run executable: ./test1
3. debug source file: gdb test1
==> Reads Symbols from test1.....
GNU gdb (Ubuntu 7.9-1ubuntu1) 7.9
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from test1...done.

4. (gdb) will start apprearing
   further commands are:
   i)   start 
   ii)  list (Lists Source code in steps of 10 instructions)
   iii) step (Single step execution -  starts from 1st executable instruction)
   iv)  print varname using 'print' or 'p' command
   v)   Examine instructions using below command (returns 'n' assembly instructions starting from 'addr') 
        Syntax: x/'n'i 'addr'
		Examples: i) x/5i $pc       ii) x/10i 0x4005bc
		
   vi)Examine Memory using x command: x varname
                                      x
									  x/10b varname (return 10 bytes starting from var address)
   vii) watch i: sets hardware watchpoint and returns old and new value
   
   viii) Below given is the example of using watch, rwatch and break

	   (gdb) list
	1	#include<stdio.h>
	2	#include<string.h>
	3	int square(int big, int temp);
	4	void main()
	5	{
	6		int sum, i;
	7		char string[120];	
	8		sum = 0;
	9		strcpy(string, "Hello!");
	10		for( i=1; i <= 10; i++){
	(gdb) watch sum
	Hardware watchpoint 6: sum
	(gdb) rwatch i
	Hardware read watchpoint 7: i
	(gdb) break 11
	Breakpoint 8 at 0x4005ea: file test.c, line 11.
	(gdb) cont
	Continuing.
	Hardware read watchpoint 7: i

	Value = 1
	0x000000000040061f in main () at test.c:10
	10		for( i=1; i <= 10; i++){
	(gdb) cont

		
   ix) display watch point and breakpoint info and delete break point
   
   (gdb) info watch
	Num     Type            Disp Enb Address            What
	6       hw watchpoint   keep y                      sum
		breakpoint already hit 1 time
	7       read watchpoint keep y                      i
		breakpoint already hit 2 times
	(gdb) info break
	Num     Type            Disp Enb Address            What
	2       breakpoint      keep y   0x00000000004005f6 in main at test.c:12
		breakpoint already hit 1 time
	3       breakpoint      keep y   0x00000000004005f6 in main at test.c:12
		breakpoint already hit 1 time
	6       hw watchpoint   keep y                      sum
		breakpoint already hit 1 time
	7       read watchpoint keep y                      i
		breakpoint already hit 2 times
	8       breakpoint      keep y   0x00000000004005ea in main at test.c:11
		breakpoint already hit 1 time
	(gdb) dele 12
	No breakpoint number 12.
