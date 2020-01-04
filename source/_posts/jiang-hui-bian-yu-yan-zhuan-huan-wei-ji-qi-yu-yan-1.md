---
title: 将汇编语言转换为机器语言
url: 1478.html
id: 1478
categories:
  - 汇编语言
  - 硬件系统
date: 2018-07-26 17:10:00
tags:
  - 汇编语言
  - 机器语言
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180725093458.png) **将x86汇编语言翻译成机器语言，而机器语言是写入到硬件板子上的。** 具体以如下格式展示：（分号右边的是注释） ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726161957.png) **首先需要了解十五条基本指令，下面是指令的参考表** ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726162108.png) **下面大致介绍一下每条指令的功能：** 1、MOV是将源寄存器中的内容存放到目的寄存器中  2、ADD是将源寄存器 和目的寄存器中的内容相加存放到目的寄存器中  3、SUB是将目的寄存器中的内容和源寄存器中的内容相减存放到目的寄存器中  4、AND是将目的寄存器和源寄存器中的内容进行二进制按位与存放到目的寄存器中  5、OR是将目的寄存器和源寄存器中的内容进行二进制按位或存放到目的寄存器中  6、RR是将将RS中的内容向右循环位移一位，存档到RD中  7、INC是将RD寄存器中的内容自加一  8、 LAD是按照M的寻址方式通过地址D来访问内存，取出来的内容存放到RD中  9、STA是按照M的寻址方式将RD中的内容存放到内存D地址的位置 10、JMP是按照寻址方式M无条件跳转到D地址 11、BZC是当FC或FZ等于一时按照寻址方式M跳转到地址D对应的位置 12、IN是得到I/O端输入的内容存放到寄存器RD中 13、OUT是将寄存器RD中的内容输出到I/O端 14、LDI是将一个立即数放到RD寄存器中 15、HALT是停机指令 机器指令的注释部分就是按照助记符号来编写的。 至于$P 后面的内容下面我会介绍。 **指令的格式分四种：** （1）单字节指令格式（其中包括ADD、AND、INC、SUB、OR、RR、HLT和MOV） ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726162700.png) 其中RS为源寄存器，RD为目的寄存器 （2）IN和OUT的指令格式为： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726162804.png) 其中P为I/O端口号，IN的一般为00H，OUT的一般为40H （3）LAD、STA、JMP和BZC指令格式如下： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726163246.png) 其中M为寻址方式（四种），D为地址 （4）LDI指令格式如下： ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726163535.png) data为向寄存器中存放的数据 **寻址方式参考表：** ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726165040.png) **以下是寄存器的参考表：** ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180726162414.png) 以MOV指令为例： 它以0100开头（至于为什么之后在微指令的设计方面我会说），后面的RS和RD分别为寄存器   假设是将R0寄存器的内容存放到R1中具体的编码形式应为： 0100 00 01 以STA指令为例： 设计将R1寄存器中的内容按照直接寻址存放到内存中4FH对应的位置 STA指令是以1101开头  直接寻址方式为00  指令格式为： 1101  00 01 （要转化为十六进制） 4F **在了解了上面的内容后，就可以一点一点的将汇编语言转换为助记符指令，然后在转换机器码就可以了。** **这里分享一个小小的心得，为了保证程序能够快速运行进行少用访问的指令，要充分使用寄存器。** **还有就是循环loop的话可以使用jmp配合bzc来进行循环或者是条件跳转** **下面分享一个我写的奇数偶数个数判断的机器码：**
```
$P 00 20 ; START:IN RO,00H
$P 01 00 ;
$P 02 D0 ; STA 00 R0,6FH
$P 03 6F ;
$P 04 70 ; INC R0
$P 05 61 ; LDI 00,R1,01H
$P 06 01 ;
$P 07 22 ; LK:IN R2,00H
$P 08 00 ;
$P 09 16 ; AND R1,R2
$P 0A 99 ; JE R2,R1,JISHU
$P 0B 0E ;
$P 0C E0 ; JMP XUNHUAN
$P 0D 0F ;
$P 0E 73 ; JISHU:INC R3
$P 0F 84 ; XUNHUAN:SUB R1,R0
$P 10 94 ; JE R1,R0,EXIT
$P 11 14 ;
$P 12 E0 ; JMP LK
$P 13 07 ;
$P 14 C0 ; EXIT:LAD 00 ,R0,6FH
$P 15 6F ;
$P 16 8C ; SUB R3,R0 
$P 17 3C ; OUT R0,40H
$P 18 40 ;
$P 19 30 ; OUT R3,40H
$P 1A 40 ;
$P 1B 50 ; HLT

至于微指令的编写，我会在以后的博文里面讲解。 偷偷分享一下自己写的汇编指令

data segment
	input db 'please input a lot of number:','$'
	output1 db 'The number of odd numbers is:','$'
	output2 db 'The number of even numbers is:','$'
data ends

code segment
	assume cs:code,ds:data
	start:
	mov ax,data
	mov ds,ax
	
	mov ah,01H  ;输入要输入数据的个数
	int 21H
	sub al,30H
 
	mov cx,0H
	mov cl,al
	
	mov dl,0AH
    mov ah,02H
    int 21H
    
	mov bp,0 ;偶数计数器
	mov si,0 ;奇数计数器
lk:	
	mov ah,01H
	int 21H
	sub al,30H
	and al,01H
	cmp al,01H
	jz jishu
	inc bp
	jmp useloop
jishu:
    inc si
    jmp useloop

useloop:
    loop lk
    
end1:
    mov dl,0AH
    mov ah,02H
    int 21H
    
    mov ax,0H
    mov ax,bp
    add ax,30H
    
    mov bx,0H
    mov bx,si
    add bx,30H
    
    mov dl,0H
    mov dl,al
    mov ah,02H
    int 21H
    
    mov dl,0H
    mov dl,bl
    mov ah,02H
    int 21H
    
    mov ah,4ch
    int 21H
code ends
end start
```