# Module Index

## pwnlib.adb

`pwnlib.adb` — <font color="00a0ff">Android Debug Bridge</font>

## pwnlib.args

`pwnlib.args` — <font color="00a0ff">Magic Command-Line Arguments</font>

## pwnlib.asm

`pwnlib.asm` — <font color="00a0ff">Assembler functions</font>

### Function make_elf()

<font color="00a0">make_elf</font>

这段代码非常有趣

```python
>> context.clear(arch='i386')
>> bin_sh = unhex('6a68682f2f2f73682f62696e89e331c96a0b5899cd80')
>> filename = make_elf(bin_sh, extract=False)
>> p = process(filename)
>> p.interactive()
```

结果：

```python
Python 3.8.10 (default, May 26 2023, 14:05:08) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pwn import *
>>> context.clear(arch='i386')
>>> bin_sh = unhex('6a68682f2f2f73682f62696e89e331c96a0b5899cd80')
>>> filename = make_elf(bin_sh, extract=False)
>>> p = process(filename)
[x] Starting local process '/tmp/pwn-asm-x30h5mio/step3-elf'
[+] Starting local process '/tmp/pwn-asm-x30h5mio/step3-elf': pid 4088
>>> p.interactive()
[*] Switching to interactive mode
ls
0b1de1c9-8228-48a8-b4ab-1d764d8fc342.m3u8  Collections		 dirsearch
111					   JetBrainsMono.tar.xz  lmkj
2107b6f49b236cc8352b4b69cab621d1.key	   Ubuntu.tar.xz	 main
3x17					   bin			 temp
whoami
gao
```

会创建三个临时文件。

```sh
❯ ls
step1-asm  step2-obj  step3-elf
```

分别file

```sh
/tmp/pwn-asm-x30h5mio 
❯ file `ls`
step1-asm: ASCII text
step2-obj: ELF 32-bit LSB relocatable, Intel 80386, version 1 (SYSV), not stripped
step3-elf: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, stripped
```

无非是汇编，链接。assemble，link

cat：

```sh
❯ cat `ls`
.section .shellcode,"awx"
.global _start
.global __start
.p2align 2
_start:
__start:
.intel_syntax noprefix
.string "\x6a\x68\x68\x2f\x2f\x2f\x73\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\x6a\x0b\x58\x99\xcd\x80"

ELF�4jhh///sh/bin��1�j
                      X�̀__start.symtab.strtab.shstrtab.text.data.bss.shellcode!44,4Lp	
                      
�	�7ELF404 (��Q�tdjhh///sh/bin��1�j
                               X�̀.shstrtab.shellcode
                                                    �
```

后面两个就是乱码。

objdum

```sh
objdump: step1-asm: file format not recognized

step2-obj:     file format elf32-i386


Disassembly of section .shellcode:

00000000 <__start>:
   0:	6a 68                	push   $0x68
   2:	68 2f 2f 2f 73       	push   $0x732f2f2f
   7:	68 2f 62 69 6e       	push   $0x6e69622f
   c:	89 e3                	mov    %esp,%ebx
   e:	31 c9                	xor    %ecx,%ecx
  10:	6a 0b                	push   $0xb
  12:	58                   	pop    %eax
  13:	99                   	cltd   
  14:	cd 80                	int    $0x80
	...

step3-elf:     file format elf32-i386


Disassembly of section .shellcode:

08049000 <.shellcode>:
 8049000:	6a 68                	push   $0x68
 8049002:	68 2f 2f 2f 73       	push   $0x732f2f2f
 8049007:	68 2f 62 69 6e       	push   $0x6e69622f
 804900c:	89 e3                	mov    %esp,%ebx
 804900e:	31 c9                	xor    %ecx,%ecx
 8049010:	6a 0b                	push   $0xb
 8049012:	58                   	pop    %eax
 8049013:	99                   	cltd   
 8049014:	cd 80                	int    $0x80
	...
```

后两个的区别无非是否链接。

## pwnlib.atexception

`pwnlib.atexception` — <font color="00a0ff">Callbacks on unhandled exception</font>



## pwnlib.atexit

`pwnlib.atexit` — <font color="00a0ff">Replacement for atexit</font>

## pwnlib.constants

`pwnlib.constants` — <font color="00a0ff">Easy access to header file constants</font>

一些常量

## pwnlib.config

`pwnlib.config` — <font color="00a0ff">Pwntools Configuration File</font>



## pwnlib.context

`pwnlib.context` — <font color="00a0ff">Setting runtime variables</font>



## pwnlib.dynelf

`pwnlib.dynelf` — <font color="00a0ff">Resolving remote functions using leaks</font>

这个是解析地址的。

但是我看不明白。



## pwnlib.encoders

`pwnlib.encoders` — <font color="00a0ff">Encoding Shellcode</font>







