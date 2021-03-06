# Learn gdb

Using a debugging tool will be extremely useful on your missions. Can you run this [program](run) in [gdb](https://en.wikipedia.org/wiki/GNU_Debugger) and find the flag? You can find the file in /problems/learn-gdb_2_32e08c18932eb88649e9b97f3020b9f5 on the shell server.

## Solution
The flag is written to a global variable called `flag_buf`. All we have to do is find a place to set a breakpoint after the flag is written to the buffer and then use `printf` to print the string in that buffer.

```
$ gdb run
(gdb) disassemble main
Dump of assembler code for function main:                                                                                                                   
   0x00000000004008c9 <+0>:     push   %rbp                                                                                                                 
   0x00000000004008ca <+1>:     mov    %rsp,%rbp                                                                                                            
   0x00000000004008cd <+4>:     sub    $0x10,%rsp                                                                                                           
   0x00000000004008d1 <+8>:     mov    %edi,-0x4(%rbp)                                                                                                      
   0x00000000004008d4 <+11>:    mov    %rsi,-0x10(%rbp)                                                                                                     
   0x00000000004008d8 <+15>:    mov    0x200af9(%rip),%rax        # 0x6013d8 <stdout@@GLIBC_2.2.5>                                                          
   0x00000000004008df <+22>:    mov    $0x0,%ecx                                                                                                            
   0x00000000004008e4 <+27>:    mov    $0x2,%edx                                                                                                            
   0x00000000004008e9 <+32>:    mov    $0x0,%esi                                                                                                            
   0x00000000004008ee <+37>:    mov    %rax,%rdi                                                                                                            
   0x00000000004008f1 <+40>:    callq  0x400650 <setvbuf@plt>                                                                                               
   0x00000000004008f6 <+45>:    mov    $0x4009d0,%edi                                                                                                       
   0x00000000004008fb <+50>:    callq  0x400600 <puts@plt>                                                                                                  
   0x0000000000400900 <+55>:    mov    $0x0,%eax                                                                                                            
   0x0000000000400905 <+60>:    callq  0x400786 <decrypt_flag>                                                                                              
   0x000000000040090a <+65>:    mov    $0x400a08,%edi                                                                                                       
   0x000000000040090f <+70>:    callq  0x400600 <puts@plt>                                                                                                  
   0x0000000000400914 <+75>:    mov    $0x0,%eax                                                                                                            
   0x0000000000400919 <+80>:    leaveq                                                                                                                      
   0x000000000040091a <+81>:    retq   
End of assembler dump.
```

We see that the next instruction, after `decrypt_flag`, is at `*main + 65`. So this is a good place to put a breakpoint and print the buffer.

```
(gdb) break *main+65
Breakpoint 1 at 0x40090a
(gdb) run
Starting program: /home/perry/git/self/picoCTF/learn_gdb/run 
Decrypting the Flag into global variable 'flag_buf'
.....................................

Breakpoint 1, 0x000000000040090a in main ()
(gdb) printf "%s", flag_buf 
picoCTF{gDb_iS_sUp3r_u53fuL_66d5464d}(gdb)
```

Thus the flag is `picoCTF{gDb_iS_sUp3r_u53fuL_66d5464d}`.


## Hints
- Try setting breakpoints in gdb
- Try and find a point in the program after the flag has been read into memory to break on
- Where is the flag being written in memory?
