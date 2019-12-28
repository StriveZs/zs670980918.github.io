---
title: Python随机密码生成并判断强度
url: 1588.html
id: 1588
categories:
  - Python功能
  - 文章页
date: 2019-01-19 17:05:31
tags:
---

![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190119165308.png) 能够根据需求生成指定长度的密码。 密码满足的规则（密码至少包含以下四条规则中的三条）： 1.大写字母（A-Z） 2.小写字母（a-z） 3.数字（0-9） 4.特殊字符（!,%,@,#等等） 密码强度判断的规则： 1.打分规则说明 2.如果密码中小写字母和大写字母的个数相差不超过2 则认为得分应该较高 3.如果密码中数字的个数小于等于密码总长度的一般是认为得分较高 4.如果得到的密码中含有标签符号则认为得分较高 代码：

import string
import random
lowercase = string.ascii_lowercase #所有小写字母
uppercase = string.ascii_uppercase #所有大写字母
digits = string.digits #所有数字
punction = string.punctuation #所有标点符号

def judge(str1, r1, r2, r3, r4):
    grade = 0  # 计分器
    if abs(r1 - r2) >= 0 and abs(r1 - r2) <= 2:
        grade = grade + 50
    else:
        grade = grade + 30
    if r3 <= round(int(length) / 2):
        grade = grade + 30
    else:
        grade = grade + 20
    if r4 == 0:
        grade = grade - 0  # 不加分
    else:
        grade = grade + 20

    if grade >= 80:
        print("该密码强度为高")
    elif grade < 80 and grade >= 70:
        print("该密码强度为较高")
    elif grade < 70 and grade >= 60:
        print("该密码强度为中等")
    else:
        print("该密码强度为较差")  # 由于采用随机生成也个字符所占的比例差不多 所以不存在很差的密码

length = input('请输入你想要的密码长度：')
#使用round防止在除法时得出小数
r1 = random.randint(1,round(int(length)*2/5)) #乘以五分之二来确保随机出来的小写字母的个数不会过大
r2 = random.randint(1,round((int(length)-r1)*2/5)) #乘以五分之二保证生成的大谢罪不会过多导致数字和标点符号过少
r3 = random.randint(1,(int(length)-r1-r2))
r4 = int(length)-r1-r2-r3
#保存用于密码强度判断
d1=r1
d2=r2
d3=r3
d4=r4
print('小写字母的长度:',r1)
print('大写字母的长度:',r2)
print('数字的长度:',r3)
print('标点符号的长度:',r4)

list = \[\] #用来存储随机出来的数据
while r1 !=0 or r2!=0 or r3!=0 or r4!=0:
    m = random.randint(1,4)  #四选1来生成一种字符
    if m == 1 and r1>0:
        num = random.randint(0,len(lowercase)-1)
        list.append(lowercase\[num\])
        r1 = r1-1
    if m == 2 and r2>0:
        num = random.randint(0,len(uppercase)-1)
        list.append(uppercase\[num\])
        r2 = r2-1
    if m == 3 and r3>0:
        num = random.randint(0,len(digits)-1)
        list.append(digits\[num\])
        r3 = r3-1
    if m==4 and r4>0:
        num = random.randint(0,len(punction)-1)
        list.append(punction\[num\])
        r4 = r4-1

print('随机生成的密码为',end='')
str1 = ''.join(list)
print(str1)

judge(str1,d1,d2,d3,d4)

使用： ![](http://47.100.4.8/wp-content/uploads/2019/01/QQ图片20190119170449.png)