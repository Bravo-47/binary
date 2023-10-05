Поставить на домашний ноут Ubuntu 16.04 не получается, VirtualBox при установке зависает... это печально. НО, и сижу на линухе 22.04 и впринципе многое получается, prog1 и prog3 скомпилировались нормально, по методичке с ними отработал. Вот prog2 скомпилировался с ошибкой.
В общем методом(тыка, проб и ошибок) что-то движется... пока застрял на том что регистр RAX пустой
![image](https://github.com/Bravo-47/binary/assets/52736408/0b3b4a66-2153-48fc-bd01-33211268be71)

пока еще в процессе разбора...

```
(gdb) disassemble main 
Dump of assembler code for function main:
   0x00005555555551a9 <+0>:	endbr64 
   0x00005555555551ad <+4>:	push   rbp
   0x00005555555551ae <+5>:	mov    rbp,rsp
   0x00005555555551b1 <+8>:	sub    rsp,0x30
=> 0x00005555555551b5 <+12>:	mov    DWORD PTR [rbp-0x4],0x1
   0x00005555555551bc <+19>:	mov    DWORD PTR [rbp-0x8],0x2
   0x00005555555551c3 <+26>:	mov    DWORD PTR [rbp-0xc],0x3
   0x00005555555551ca <+33>:	mov    edi,0xe
   0x00005555555551cf <+38>:	call   0x5555555550b0 <malloc@plt>
   0x00005555555551d4 <+43>:	mov    QWORD PTR [rbp-0x18],rax
   0x00005555555551d8 <+47>:	lea    rax,[rbp-0x27]
   0x00005555555551dc <+51>:	lea    rdx,[rip+0xe21]        # 0x555555556004
   0x00005555555551e3 <+58>:	mov    rsi,rdx
   0x00005555555551e6 <+61>:	mov    rdi,rax
   0x00005555555551e9 <+64>:	call   0x555555555090 <strcpy@plt>
   0x00005555555551ee <+69>:	mov    rax,QWORD PTR [rbp-0x18]
   0x00005555555551f2 <+73>:	lea    rdx,[rip+0xe1a]        # 0x555555556013
   0x00005555555551f9 <+80>:	mov    rsi,rdx
   0x00005555555551fc <+83>:	mov    rdi,rax
   0x00005555555551ff <+86>:	call   0x555555555090 <strcpy@plt>
   0x0000555555555204 <+91>:	mov    edi,DWORD PTR [rbp-0xc]
   0x0000555555555207 <+94>:	mov    esi,DWORD PTR [rbp-0x8]
   0x000055555555520a <+97>:	mov    ecx,DWORD PTR [rbp-0x4]
   0x000055555555520d <+100>:	mov    rdx,QWORD PTR [rbp-0x18]
   0x0000555555555211 <+104>:	lea    rax,[rbp-0x27]
   0x0000555555555215 <+108>:	mov    r9d,edi
   0x0000555555555218 <+111>:	mov    r8d,esi
   0x000055555555521b <+114>:	mov    rsi,rax
   0x000055555555521e <+117>:	lea    rax,[rip+0xdfc]        # 0x555555556021
   0x0000555555555225 <+124>:	mov    rdi,rax
   0x0000555555555228 <+127>:	mov    eax,0x0
   0x000055555555522d <+132>:	call   0x5555555550a0 <printf@plt>
   0x0000555555555232 <+137>:	mov    rax,QWORD PTR [rbp-0x18]
   0x0000555555555236 <+141>:	mov    rdi,rax
   0x0000555555555239 <+144>:	call   0x555555555080 <free@plt>
   0x000055555555523e <+149>:	mov    eax,0x0
   0x0000555555555243 <+154>:	leave  
   0x0000555555555244 <+155>:	ret    
End of assembler dump.
(gdb) i r
rax            0x5555555551a9      93824992235945
rbx            0x0                 0
rcx            0x555555557da8      93824992247208
rdx            0x7fffffffddf8      140737488346616
rsi            0x7fffffffdde8      140737488346600
rdi            0x1                 1
rbp            0x7fffffffdcd0      0x7fffffffdcd0
rsp            0x7fffffffdca0      0x7fffffffdca0
r8             0x7ffff7f94f10      140737353699088
r9             0x7ffff7fc9040      140737353912384
r10            0x7ffff7fc3908      140737353890056
r11            0x7ffff7fde6c0      140737354000064
r12            0x7fffffffdde8      140737488346600
r13            0x5555555551a9      93824992235945
r14            0x555555557da8      93824992247208
r15            0x7ffff7ffd040      140737354125376
rip            0x5555555551b5      0x5555555551b5 <main+12>
eflags         0x206               [ PF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
(gdb) b *0x000055555555522d
Breakpoint 3 at 0x55555555522d: file prog3.c, line 16.
(gdb) c
Continuing.
Warning:
Cannot insert breakpoint 2.
Cannot access memory at address 0x122d

Command aborted.
(gdb) d
Delete all breakpoints? (y or n) y
(gdb) b main 
Breakpoint 4 at 0x5555555551b5: file prog3.c, line 6.
(gdb) c
Continuing.
HelloFromStack, HelloFromHeap - 1, 2, 3 
[Inferior 1 (process 683384) exited normally]
(gdb) r
Starting program: /media/roman/f/private/Learn_IB/binary/test/prog3 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 4, main () at prog3.c:6
6	  int a = 1;
(gdb) b *0x000055555555522d
Breakpoint 5 at 0x55555555522d: file prog3.c, line 16.
(gdb) c
Continuing.

Breakpoint 5, 0x000055555555522d in main () at prog3.c:16
16	  printf("%s, %s - %d, %d, %d \n", str_1, str_2, a, b, c);
(gdb) x/8xw $rsp
0x7fffffffdca0:	0x00000002	0x00000000	0x6c6548ff	0x72466f6c
0x7fffffffdcb0:	0x74536d6f	0x006b6361	0x555592a0	0x00005555
(gdb) x/16xw $rsp
0x7fffffffdca0:	0x00000002	0x00000000	0x6c6548ff	0x72466f6c
0x7fffffffdcb0:	0x74536d6f	0x006b6361	0x555592a0	0x00005555
0x7fffffffdcc0:	0x00001000	0x00000003	0x00000002	0x00000001
0x7fffffffdcd0:	0x00000001	0x00000000	0xf7da3d90	0x00007fff
(gdb) x/8xw $rsp
0x7fffffffdca0:	0x00000002	0x00000000	0x6c6548ff	0x72466f6c
0x7fffffffdcb0:	0x74536d6f	0x006b6361	0x555592a0	0x00005555
(gdb) x/s 0x00000002
0x2:	<error: Cannot access memory at address 0x2>
(gdb) x/s 0x6c6548ff
0x6c6548ff:	<error: Cannot access memory at address 0x6c6548ff>
(gdb) x/s 0x5555555551a9
0x5555555551a9 <main>:	"\363\017\036\372UH\211\345H\203\354\060\307E\374\001"
(gdb) x/s 93824992235945
0x5555555551a9 <main>:	"\363\017\036\372UH\211\345H\203\354\060\307E\374\001"
(gdb) x/s 0x06c6548ff
0x6c6548ff:	<error: Cannot access memory at address 0x6c6548ff>
(gdb) x/s 0x7fffffffdca0
0x7fffffffdca0:	"\002"
(gdb) x/s 0x7fffffffdcb0
0x7fffffffdcb0:	"omStack"
(gdb) x/s 0x5555555550a0
0x5555555550a0 <printf@plt>:	"\363\017\036\372\362\377%\035/"
(gdb) x/5i $rip
=> 0x55555555522d <main+132>:	call   0x5555555550a0 <printf@plt>
   0x555555555232 <main+137>:	mov    rax,QWORD PTR [rbp-0x18]
   0x555555555236 <main+141>:	mov    rdi,rax
   0x555555555239 <main+144>:	call   0x555555555080 <free@plt>
   0x55555555523e <main+149>:	mov    eax,0x0
(gdb) i r rax
rax            0x0                 0
(gdb) i r eax
eax            0x0                 0
(gdb) i r
rax            0x0                 0
rbx            0x0                 0
rcx            0x1                 1
rdx            0x5555555592a0      93824992252576
rsi            0x7fffffffdca9      140737488346281
rdi            0x555555556021      93824992239649
rbp            0x7fffffffdcd0      0x7fffffffdcd0
rsp            0x7fffffffdca0      0x7fffffffdca0
r8             0x2                 2
r9             0x3                 3
r10            0xfffffffffffff000  -4096
r11            0x7ffff7f93ce0      140737353694432
r12            0x7fffffffdde8      140737488346600
r13            0x5555555551a9      93824992235945
r14            0x555555557da8      93824992247208
r15            0x7ffff7ffd040      140737354125376
rip            0x55555555522d      0x55555555522d <main+132>
eflags         0x206               [ PF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
(gdb) c
Continuing.
HelloFromStack, HelloFromHeap - 1, 2, 3 
[Inferior 1 (process 683430) exited normally]
```
