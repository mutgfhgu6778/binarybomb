# 留学生日常作业/课程设计/代码辅导/CS/DS/商科，仅为漂洋过海的你❥
标签：Computer Science、Data Science、Business Administration，留学生编程作业代写&&辅导

## 个人介绍:
本人是一名资深码农，酷爱投资。

为您提供 CS , DS , 商科 编程作业代写

<img src="design2023866.jpg"  width="200" />

PKU-ICS
Bomb Lab: Defusing a Binary Bomb
1 Introduction
The nefarious Dr. Evil has planted a slew of “binary bombs” on our 64-bit linux machines. A binary bomb
is a program that consists of a sequence of phases. Each phase expects you to type a particular string on
stdin. If you type the correct string, then the phase is defused and the bomb proceeds to the next phase.
Otherwise, the bomb explodes by printing "BOOM!!!" and then terminating. The bomb is defused when
every phase has been defused.
There are too many bombs for us to deal with, so we are giving each student a bomb to defuse. Your
mission, which you have no choice but to accept, is to defuse your bomb before the due date. Good luck,
and welcome to the bomb squad!
Step 1: Get Your Bomb
You can obtain your bomb from the Autolab site
https://autolab.pku.edu.cn
After logging in to Autolab, select Bomblab -> Download your bomb. The Autolab server will
build your bomb and return it to your browser in a tar file called bombk.tar, where k is the unique
number of your bomb.
Save the bombk.tar file to a (protected) working directory in which you plan to do your work. Then login
to a linux machine and give the command: tar -xvf bombk.tar. This will create a directory called
./bombk with the following files:
• README: Identifies the bomb and its owner.
• bomb: The executable binary bomb.
• bomb.c: Source file with the bomb’s main routine and a friendly greeting from Dr. Evil.
You should only download one bomb. If for some reason you download multiple bombs, choose one bomb
to work on and delete the rest.
1
Warning: If you expand your bombk.tar file on a PC, you’ll risk resetting the bomb’s execute bit. You
can undo this with the chmod +x bomb command.
Step 2: Defuse Your Bomb
Your job for this lab is to defuse your bomb.
You must do the assignment on one of the 64-bit class linux machines.
In fact, there is a rumor that Dr. Evil really is evil, and the bomb will always blow up if run elsewhere.
There are several other tamper-proofing devices built into the bomb as well, or so we hear.
You can use many tools to help you defuse your bomb. Please look at the Hints section for some tips and
ideas. The best way is to use your favorite debugger to step through the disassembled binary.
Each time your bomb explodes it notifies the Autolab server, and you lose 1/2 point (up to a max of 20
points) in the final score for the lab. So there are consequences to exploding the bomb. You must be careful!
The first four phases are worth 10 points each. Phases 5 and 6 are a little more difficult, so they are worth
15 points each. So the maximum score you can get is 70 points.
Although phases get progressively harder to defuse, the expertise you gain as you move from phase to phase
should offset this difficulty. However, the last phase will challenge even the best students, so please don’t
wait until the last minute to start.
The bomb ignores blank input lines. If you run your bomb with a command line argument, for example,
linux> ./bomb psol.txt
then it will read the input lines from psol.txt until it reaches EOF (end of file), and then switch over
to stdin. In a moment of weakness, Dr. Evil added this feature so you don’t have to keep retyping the
solutions to phases you have already defused.
To avoid accidentally detonating the bomb, you will need to learn how to single-step through the assembly
code and how to set breakpoints. You can safely exit your bomb at any time by typing ctrl-c (simultaneously pressing the ctrl and c keys).
You will also need to learn how to inspect both the registers and the memory states. One of the nice sideeffects of doing the lab is that you will get very good at using a debugger. This is a crucial skill that will pay
big dividends the rest of your career.
Warning: You should never use your debugger to jump directly to a particular phase. Doing so can cause
your bomb to explode silently.
Handin
There is no explicit handin. The bomb will notify Autolab automatically about your progress as you work
on it. You can keep track of how you are doing by looking at the Autolab class scoreboard (From Auto2
lab, follow Bomblab -> View scoreboard). This Web page is updated continuously to show the
progress for each bomb.
Note: Please don’t submit defusing strings to your bomb that contain apostrophes. There is a known bug in
the backend autograder that causes it to get confused by defusing strings with apostrophes.
Hints (Please read this!)
There are many ways of defusing your bomb. You can examine it in great detail without ever running the
program, and figure out exactly what it does. This is a useful technique, but it not always easy to do. You
can also run it under a debugger, watch what it does step by step, and use this information to defuse it. This
is probably the fastest way of defusing it.
We do make one request, please do not use brute force! You could write a program that will try every
possible key to find the right one. But this is no good for several reasons:
• You lose 1/2 point (up to a max of 20 points) every time you guess incorrectly and the bomb explodes.
• Every time you guess wrong, a message is sent to the Autolab server. You could very quickly saturate
the network with these messages, and cause the system administrators to revoke your computer access.
• We haven’t told you how long the strings are, nor have we told you what characters are in them. Even
if you made the (incorrect) assumptions that they all are less than 120 characters long and only contain
letters, then you will have 26120 guesses for each phase. This will take a very long time to run, and
you will not get the answer before the assignment is due.
• The answer of phase5 should only consist of digits and letters! Input string with not supported characters may cause strange results which we won’t bear the responsibility.
There are many tools which are designed to help you figure out both how programs work, and what is wrong
when they don’t work. Here is a list of some of the tools you may find useful in analyzing your bomb, and
hints on how to use them.
• gdb
The GNU debugger is a command line debugger tool available on virtually every platform. You can
trace through a program line by line, examine memory and registers, look at both the source code and
assembly code (we are not giving you the source code for most of your bomb), set breakpoints, set
memory watch points, and write scripts.
The CS:APP textbook Web page at
http://csapp.cs.cmu.edu/3e/students.html
has a handy 1-page gdb command summary for x86-64 that you can print out and use as a reference.
It also contains a link to Prof. Norm Matloff’s gdb GDB tutorial.
Here are some other tips for using gdb.
3
– To keep the bomb from blowing up every time you type in a wrong input, you’ll need to learn
how to set breakpoints.
– For online documentation, type “help” at the gdb command prompt, or type “man gdb”,
or “info gdb” at a Unix prompt. Some people also like to run gdb under gdb-mode in
emacs.
• objdump -t
This will print out the bomb’s symbol table. The symbol table includes the names of all functions and
global variables in the bomb, the names of all the functions the bomb calls, and their addresses. You
may learn something by looking at the function names! For example, you could discover a function
called “explode bomb”, which would be a good place to set a breakpoint to keep the bomb from
blowing up.
• objdump -d
Use this to disassemble all of the code in the bomb. You can also just look at individual functions.
Reading the assembler code can tell you how the bomb works.
Although objdump -d gives you a lot of information, it doesn’t tell you the whole story. Calls to
system-level functions are displayed in a cryptic form. For example, a call to sscanf might appear
as:
8048c36: e8 99 fc ff ff call 80488d4 <_init+0x1a0>
To determine that the call was to sscanf, you would need to disassemble within gdb.
• strings
This utility will display the printable strings in your bomb.
Looking for a particular tool? How about documentation? Don’t forget, the commands apropos, man,
and info are your friends. In particular, man ascii might come in useful. info gas will give you
more than you ever wanted to know about the GNU Assembler. If you get stumped, feel free to ask the
teaching staff for help.
2 Secret phase
As you may have heard, Dr. Evil always has a card up his sleeve, and it is indeed the case this time. But he
left some words most elusive to you, which we quoted verbatim as follows:
Dreaming of breaking through the Sustainer of Heavenly Principles’s formidable barrier? Deluding yourself into thinking you can open the gates to another world? Just you? What an
absurdity! Teyvat shall forever remain confined to the realms of your mere reverie!
Can you solve this conundrum? But we would be remiss if we did not mention that this task earns you no
credits. Since the administrator’s schedule is crammed, we can only count on you now to figure these all
out and safeguard our vulnerable little linux machines. Please do help us!
## 作业代写价格:

|类型|美元|人民币|
|-----:|-----:|-----:|
|Assignment|$60-$120|¥400-¥800|

### 为了方便快速定价和确定是否代做，麻烦提供私聊的时候提供以下信息：
如果是作业，提供本次作业要求文档；如果是考试，提供考试范围和考试时间
一两句话概括一下作业任务或者考试任务，比如”可以帮忙实现一个决策树算法吗？”、”网络安全选择题考试，范围是内网横向移动知识点”
### 作业定价有两种方式：
    - 根据定价标准进行
    - 通过微信我们一起协商
## 联系方式

微信（WeChat）：design2023866

<img src="design2023866.jpg"  width="200" />
