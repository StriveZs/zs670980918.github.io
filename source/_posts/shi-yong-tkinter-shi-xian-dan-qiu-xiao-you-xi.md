---
title: 使用tkinter实现弹球小游戏
url: 1329.html
id: 1329
categories:
  - Python——Tkinter编程
  - 小游戏
  - 文章页
date: 2018-06-06 21:27:32
tags:
---

![](http://47.100.4.8/wp-content/uploads/2018/05/u407244128253124607fm27gp0.jpg) 写了一个弹球小游戏，能够实现的简单的通过键盘的左右键来进行木板的移动，还有小球弹到边界反弹，以及随机出生点还有速度的改变、最后是游戏结束的提示，感觉还有改进的地方，比如：可以手动选择游戏难度，游戏结束后重新开始等，这个后续可能会加上去。 截图： ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180606155956.png) ![](http://47.100.4.8/wp-content/uploads/2018/06/QQ图片20180606160006.png) 代码总共下来也就不到100行，也是看了网上写的一些东西自己在编写得到的。 下载地址:https://download.csdn.net/download/qq_16184125/10463456 代码：

import tkinter
import random
import time
import tkinter.messagebox

tk = tkinter.Tk()  # 创建一个tk实例
tk.title("弹球游戏")  #窗口名称
tk.resizable(0,0)  #设置窗口管理器调整布局大小，  0,0表示不能被拉升
tk.wm_attributes("-topmost",1)
canvas = tkinter.Canvas(tk,width=500,height=400,bd=0,highlightthickness=0)#创建一个400*500的界面，背景色为默认，边框为厚度为0
canvas.pack()  #通知窗口管理器注册组件
tk.update()  #刷新一下界面

class Ball():  #小球
    def \_\_init\_\_(self,canvas,color):  #canvas，画图用来画一个球，一个是color表示球的颜色
        self.canvas = canvas
        self.id = canvas.create_oval(10,10,25,25,fill=color)  #画球
        self.canvas.move(self.id,245,100)  #记录球的id
        #设置小球的初始位置
        starts = \[-1,-2,-3,0,1,2,3\]
        random.shuffle(starts)
        #随机从上面的starts列表中取出一个数
        self.x = starts\[0\]
        self.y = -1
        self.flag2 = 0
        self.canvas\_height = self.canvas.winfo\_height()
        self.canvas\_width = self.canvas.winfo\_width()


    def hit_paddle(self):
        paddle_pos = self.canvas.coords(id1)
        if self.pos\[2\] >= paddle\_pos\[0\] and self.pos\[0\]<= paddle\_pos\[2\]:
            if self.pos\[3\] >= paddle\_pos\[1\] and self.pos\[3\] <= paddle\_pos\[3\]:
                return True
        return False

    def draw(self):
        self.canvas.move(self.id,self.x,self.y)  #表示运动
        self.pos = self.canvas.coords(self.id)
        if self.pos\[1\]<=0:  #向下运动
            self.y = 2
        if self.pos\[0\]<=0: #向右运动
            self.x = 2
        if self.pos\[2\]>=self.canvas_width:  #向左运动
            self.x = -2
        if self.pos\[3\] >= self.canvas_height:  #向上运动
            self.flag2 = 1  #游戏结束标志

class Paddle:
    def \_\_init\_\_(self,canvas,color):
        self.canvas = canvas
        global id1
        id1 = canvas.create_rectangle(0,0,100,10,fill=color)
        self.canvas.move(id1,200,350)
        self.x = 0
        self.canvas\_width = self.canvas.winfo\_width()
        self.canvas.bind\_all('<KeyPress-Left>',self.turn\_left)  #事件响应键盘的左右按键
        self.canvas.bind\_all('<KeyPress-Right>', self.turn\_right)

    def draw(self):
        self.canvas.move(id1,self.x,0)
        pos = self.canvas.coords(id1)  #得到当前的位置
        if pos\[0\]<=0:
            self.x = 0
        elif pos\[2\]>=self.canvas_width:
            self.x=0
        else:
            self.x=0


    def turn_left(self, evt):
        self.x = -20

    def turn_right(self, evt):
        self.x = 20


ball = Ball(canvas,"red")
paddle = Paddle(canvas,"blue")

while 1:
    ball.draw()
    paddle.draw()
    flag = ball.hit_paddle()
    if flag == True:
        ball.y = -4
    if ball.flag2 == 1:
        flag1 = 1
        break
    tk.update_idletasks()
    tk.update()
    time.sleep(0.01)

if flag1 == 1:
    tkinter.messagebox.showinfo(title='Python tkinter',message='游戏结束')