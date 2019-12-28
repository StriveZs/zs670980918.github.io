---
title: 汇编语言实现判断是否为闰年
url: 1472.html
id: 1472
categories:
  - 文章页
  - 汇编语言
date: 2018-07-25 09:50:47
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180725093458.png) **使用汇编语言实现根据输入的数字来判断是否为闰年。** **算法流程图：** ![](http://47.100.4.8/wp-content/uploads/2018/07/项目流程.png) **主要代码：**

data segment
	output1 db 'Yes','$'
	output2 db 'No','$'
	output3 db 'Error','$'
	year dw ?
	x1 dw 4
	x2 dw 100
	x3 dw 400
data ends

code segment
	assume cs:code,ds:data
start:
    mov ax,data
    mov ds,ax
    ;数据初始化
    mov year,0 ;存储年份的位数清零
    mov cx,4 ;年份为4位
lk:
    push cx
    mov ah,1 ;输入单个字符
    int 21H
    ;进行输入的判断 如何小于0则跳转到Error
    cmp al,'0'
    jb error
    cmp al,3AH
    jb chuli ;如何满足则进行处理
    
error:
    ;输出换行符
    mov dl,0AH
    mov ah,02H
    int 21H
    
    lea dx,output3
    mov ah,09H
    int 21h
    jmp exit

chuli:
    sub al,30H ;将字符转换为数字
    mov ah,0 ;将ah置0
    mov cx,ax ;用cx暂存ax的内容
    ;将老的数据乘以10并且加上原来的存储的数据
    mov ax,year
    mov bx,10
    mul bx
    add ax,cx
    mov year,ax ;将乘10以后的数据存储到原值
    
    pop cx ;将原来的cx值出栈用以循环使用
  
    loop lk ;进行循环输入
    
panduan:
    mov ax,year;取得最终输入的年份
    cwd ;扩展为32位 方便进行乘除
    div x1 ;除以4
    cmp dx,0 ;判断余数是否为0
    jne feirunnian;如果余数非0则不是闰年
    
    mov ax,year
    cwd
    div x3 ;除以400
    cmp dx,0
    je runnian ;如果余数为0则是闰年
    
    mov ax,year
    cwd
    div x2 ;除以100
    cmp dx,0
    jne runnian

feirunnian:
    ;输出换行符
    mov dl,0AH
    mov ah,02H
    int 21H
    
    lea dx,output2
    mov ah,09H
    int 21H
    jmp exit
    
runnian:
    ;输出换行符
    mov dl,0AH
    mov ah,02H
    int 21H
    
    lea dx,output1
    mov ah,09H
    int 21H
    jmp exit

exit:
    mov ah,4ch
    int 21H

code ends
end start

**测试：** ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180725094929.png) ![](http://47.100.4.8/wp-content/uploads/2018/07/QQ图片20180725094951.png)