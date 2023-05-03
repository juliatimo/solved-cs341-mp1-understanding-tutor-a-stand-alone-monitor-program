Download Link: https://assignmentchef.com/product/solved-cs341-mp1-understanding-tutor-a-stand-alone-monitor-program
<br>
The purpose of this assignment is to gain some experience with our LINUX system, the StandAlone PCs (SAPCs), and makefiles. At the same time, you will learn how to understand and modify existing C code.

<ol>

 <li>Read, compile, run, understand, and modify a C program that runs a monitor program “tutor”. We call it tutor because it mimics the Tutor monitor/debugger that we have installed on the SAPCs. You will build a LINUX version as well as a version that runs on SAPC VM.</li>

 <li>Use your monitor program to explore memory locations on the PC – including the locations in which your program resides.</li>

 <li><u><strong> INTRODUCTION:</strong></u></li>

</ol>

You should work on this assignment alone and turn in your own individual report and source code including test results. The LINUX dates on your files will determine whether the work was completed on time or not.

You should already have a cs341 logical link in your LINUX home directory. Type in command:

cd cs341 to go into your homework directory. Use that subdirectory for all your work in this class. It has the right protection setup so that other students cannot access your files but instructors and graders can via group cs341-1G.

Copy files from /courses/cs341/f20/cheungr/mp1/ to your cs341 folder using:

<table width="178">

 <tbody>

  <tr>

   <td width="178">Space between  / and .</td>

  </tr>

 </tbody>

</table>




cp  –r  /courses/cs341/f20/cheungr/mp1/   .

cd mp1        ls




You should see all the files I supplied for this project. I’ll call mp1 your project directory in what follows. Use your project directory for all work for this assignment. All files referred to below are in that project directory unless otherwise specified.

*NOTE*: YOU MUST USE THE DIRECTORIES AND FILE NAMES SPECIFIED SO THAT

THE GRADERS AND I CAN FIND YOUR FILES AND TEST YOUR HOMEWORK, IF NEEDED. IF YOU DO NOT DO SO, YOU WILL BE PENALIZED AND YOUR OVERALL PROJECT GRADE WILL BE LESS.

<strong><u>III. DESCRIPTION:</u> </strong>




You will write your own “tutor” program, which mimics Tutor. It’s a tiny single user terminal monitor system, which we will compile and run both on the SAPC and on the LINUX system. In later assignments you’ll add to its capabilities. For now it should accept the commands:




md &lt;hexaddress&gt;

(SAPC and LINUX) Memory Display

Display contents (in hex) of 16 bytes at the specified address.

(Present in the same format as the “real” Tutor program – 16 pairs of hex characters followed by 16 characters interpreting each byte as a printable character for ASCII codes

0x20 through 0x7e or a fixed ‘.’ for all other (non-printable) ASCII codes values.)




ms &lt;hexaddress&gt; &lt;new_val&gt;

(SAPC and LINUX) Memory Set

Stores byte new_val (two hex characters) at specified address.  h &lt;cmd&gt;

(SAPC and LINUX) Help

Help on the specified command, for ex., “h ps”, or all commands if no argument.   s

(SAPC and LINUX) Stop

Stop running your tutor and return to the regular SAPC TUTOR (or back to the shell if running on LINUX).




The files you need to build tutor are found in my directory /courses/cs341/f20/cheungr/mp1/. Most of the program has been written for you for two reasons. First, by reading the code provided, you can learn how a standard “table-driven” command processor design works. Second, providing you with a framework allows you to concentrate on the part of the programming that’s important in this course.




The main program for tutor is in tutor.c. That driver calls a lexical analyzer (parser) called slex.c. The parser finds the command on the command line and calls the appropriate procedure by consulting the command table. File cmds.c contains that table and the code that implements the various commands. The file makefile builds them into an executable file.




Start by copying all files to your project directory. The makefile will build the executable files from your local directory. Read the makefile and learn how it does that.




<ol>

 <li>Build and run the LINUX version:</li>

</ol>

itserver6: make tutor                                         # creates an executable tutor to run on LINUX

itserver6: ./tutor                                                      # runs the program locally under LINUX       itserver6:




<ol>

 <li>Build the SAPC version:</li>

</ol>




itserver6: make                                                 # creates a tutor.lnx to download to the SAPC




Use the Virtualized SAPC environment to debug the SAPC version. Log in into the tutor-vserver VM using the provided credentials. Transfer the SAPC version to tutor-vserver VM using:




vserver$ scp <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="295c5a4c5b4748444c695c5a4c5b5a074a5a075c444b074c4d5c">[email protected]</a>:cs341/mp1/tutor.*  .

vserver$ mtip -f  tutor.lnx                                  # always use board #1




click on the “Send Cntl-Alt-Del” button at the tutor VM to reset the SAPC VM. Hit &lt;CR&gt; at the tutor-vserver VM to get the tutor prompt. Then download the tutor program to the SAPC VM and run it:




Tutor&gt; ~d                                                         # download tutor.lnx

Tutor&gt; go 100100                                            # start your program on SAPC VM







<ol>

 <li><strong><u>MODIFY PROGRAM:</u> </strong></li>

</ol>

<strong> </strong>

Read tutor.c, slex.h, slex.c, cmds.c, and the makefile in order to understand the structure of the tutor program. (We will be going over that structure in lecture.) When you’re ready,




<ol>

 <li><u>edit cmds.c to implement the required new commands (md, ms and h)</u></li>

</ol>

Use sscanf to convert the argument passed md or ms from a character string of hex digits to an integer. Use the return value from sscanf to check if it really worked. Study the makefile — be sure you understand how it works. Study the output of make as it runs — what are the program-building steps?




Sample Output




itserver6:  ./tutor

<u>command</u>         <u>help message</u>       md                  Memory display: MD &lt;addr&gt;       ms                   Memory set: MS &lt;addr&gt; &lt;value&gt;

h                      Help: H &lt;command&gt;       s                      Stop




LINUX-tutor&gt; md 10000

00010000 7f 45 4c 46 01 02 01 00 00 00 00 00 00 00 00 00 .ELF…………  LINUX-tutor&gt;




<ol>

 <li><u>play with the tutor programs that you’ve built</u></li>

</ol>

This is a central part of the assignment. If your code is elegant and perfect but you do not test it, exercise it, and think about the results it generates you will have learned less than half of what you should – so will get less than half the credit.




You must create a file discussion.txt. Write clear, grammatically correct English. Consider showing drafts to your friends (or your English teacher) to find out if your writing is clear.







<ol>

 <li><strong><u>DISCUSSIONS:</u> </strong></li>

</ol>

<strong> </strong>

In your discussion.txt file, answer all of the following questions:




<ul>

 <li>Describe how you tested your code. Try the following experiments. Write several sentences about what you found or learned working on each, and on any other similar kinds of questions that occur to you.</li>

</ul>




<ul>

 <li>What happens if you call md for an address that does not correspond to a physical memory address? What if you write to an address that’s part of your tutor code or an address in ROM area of memory? Do these questions have the same answers on LINUX and the SAPC?</li>

</ul>




<ul>

 <li>Read the makefile to see where it puts the symbol table (nm output) for your tutor code. Use that symbol table to figure out:</li>

</ul>




<ul>

 <li>the address for test global variable xyz, which has value 6. Use tutor with that address to verify the value in memory.</li>

</ul>




<ul>

 <li>the address of the pointer variable pxyz. This address should be close to the one you determined in a, but not equal to it, since pxyz is the next variable in memory after xyz. Find the value of pxyz in memory. This should be equal to the address you found in (a) because of the initialization of this variable to &amp;xyz. Note that you need to get 4 bytes of data for the value here. See IMPORTANT NOTE just below.</li>

</ul>




<ul>

 <li>the address of the cmds array. Use this address to determine the very first pointer in the array, the string pointer to “md”. Then find the ‘m’ and ‘d’ and terminating null of this string.</li>

</ul>




<ul>

 <li>change the stop command from ‘s’ to ‘x’ while the tutor program is running. Can you change the tutor prompt the same way?</li>

</ul>




<u>IMPORTANT NOTE:</u> When you try to access a 32-bit value (a pointer for example) in SAPC memory via Tutor, you need to reverse the displayed byte order, because of the little-endian representation of numbers in the Intel architecture.




Example: Suppose a pointer (or any 32-bit numeric quantity) is at address 0x100200 with value 0x00100abc. It would show up as:




Tutor&gt; md 100200

100200   bc 0a 10 00




because of “little-endian” storage of numbers in memory in the Intel architecture. See the lecture notes.




To help with displays, there is an “mdd” command (memory-display-doubleword) in the

“real” Tutor monitor. This command reorders the bytes for you and displays four bytes at a time as a doubleword value:




Tutor&gt; mdd 100200      (for same memory contents as with md command above)

100200   00100abc …




<ul>

 <li>Read the nm output to determine where in memory the code resides, on SAPC and LINUX. Hint: code symbols are marked t or T. Similarly determine where the data (set of variables) resides.</li>

</ul>




<ul>

 <li>Try to change the code itself so that tutor crashes (any random change that actually takes effect should do this). What happens on SAPC? on LINUX?</li>

</ul>




<ul>

 <li>You can’t find the program stack using the nm output, but you can find it by looking at the stack pointer, called ESP on the SAPC and LINUX. Record your observations. Use “i reg” (info on registers) to see sp in gdb and “rd” to see registers in Tutor.</li>

</ul>




<ul>

 <li>What other interesting things have you tried?</li>

</ul>




<ul>

 <li>(optional) More questions you should consider answering. What did you learn from this project? Was it worth the time it took? What parts were the hardest, what parts the easiest, what parts most surprising, most interesting?</li>

</ul>




What idiosyncrasies of C or LINUX or the SAPC or our installation slowed you down or helped you out? How might the assignment be improved?


