from tkinter import *
from random import *
from  tkinter.messagebox import*
import time
import sys
def tick():
    global time1,sec,begin
    # 从运行程序的计算机上面获取当前的系统时间
    time2 = time.strftime('%H:%M:%S')
    # 如果时间发生变化，代码自动更新显示的系统时间
    if time2 != time1:
        time1 = time2
        if begin==1:
            sec=sec+1
            clock.config(text=sec)
        if begin==2:
            sec=-1
            begin=0
    clock.after(200, tick)

#last是一个列表，里面只有一个元素，就是1，说明已经运行一次
def counter(x1,y1):
    global begin
    #,wordCount={}
##    var1=[[0 for i in range(9)]for i in range (9)]
##    if var1[x1][y1] not in wordCount:
##        wordCount[var1[x1][y1]]=""
##    print(wordCount)

    #last[0]将列表里面的第一个元素取出，然后加1，赋值给next
    next = last[0] + 1
    #修改列表里面第一个元素的值
    last[0] = next
    #返回此时运行的次数
    print( next)
    if cell[x1][y1]=="X":
        last[0]=0
        showerror("扫雷1.0","失败！")
        begin=2
    else:
        if next==71:
            showinfo("扫雷1.0","成功!用时"+str(sec)+"s")
            
            begin=2
            for i in range(9):
                for j in range(9):
                    if wC[i][j]==0:
                        print(sl.grid_slaves(i+1,j)[0].grid_forget() )
    block(x1,y1)    
def cloneBlock(x,y):
    if cell[x][y]==" ":
        if wC[x][y]==0:
            wC[x][y]=1
            print("yes")
            for i in range(x-1,x+2):
                for j in range(y-1,y+2):
                    if i>=0 and i<9 and j>=0 and j<9:
                        if wC[i][j]==0: 
                            print(sl.grid_slaves(i+1,j)[0].grid_forget() )
                            next = last[0] + 1
                            last[0] = next
                            print( next)
                            if cell[i][j]!=" ":
                                wC[i][j]=1
                            block(i,j)

def block(x,y):
    if cell[x][y]==" ":
        if wC[x][y]==0:
            wC[x][y]=1
            print("yes")
            for i in range(x-1,x+2):
                for j in range(y-1,y+2):
                    if i>=0 and i<9 and j>=0 and j<9:
                        if wC[i][j]==0: 
                            print(sl.grid_slaves(i+1,j)[0].grid_forget() )
                            next = last[0] + 1
                            last[0] = next
                            print( next)
                            if cell[i][j]!=" ":
                                wC[i][j]=1
                            cloneBlock(i,j)
                            
def forgetLabel(x,y):

    # grid_slaves返回grid中(0,0)位置的所有组件
    # grid_forget将这个组件从grid中移除（并未删除，可以使用grid再将它显示出来)
    print(sl.grid_slaves(x+1,y)[0].grid_forget() )
    if cell[x][y]!=" ":
        wC[x][y]=1
    
    x1=x
    y1=y
    counter(x1,y1)

          
    
def chessBoard():#游戏名称和开始按键
    Label(sl,pady=10,font=100,text="扫雷1.0").grid(row=0,column=0,columnspan=3)
    Button(sl,font=12,text='start',command=start).grid(row=0,column=3,columnspan=3)



def start():#棋盘布局
    global begin
    begin=1
    var=[[0 for i in range(11)]for i in range (11)]    
    wordCount={}
    for k in range(10):
        x=randint(1,9)
        y=randint(1,9)
        while var[x][y] in wordCount:
            x=randint(1,9)
            y=randint(1,9)
        var[x][y]='X'
        wordCount[var[x][y]]="X"
    


    for i in range(1,10):#数字
        for j in range(1,10):
            if var[i][j]!="X":
                num=0
                for x in range(i-1,i+2):
                    for y in range(j-1,j+2):
                        if var[x][y]=="X":
                            num=num+1
                var[i][j]=num
            if var[i][j]==0:
                var[i][j]=" "
    global cell ,wC,last
    last=[0]
    cell=[[0 for i in range(9)]for i in range (9)]#存储答案
    wC=[[0 for i in range(9)]for i in range (9)]#存储0和1

    buttons=[]
    for i in range(9):

        for j in range(9):

            cell[i][j]=var[i+1][j+1]

                
            if cell[i][j]==1:
                color="#1E90FF"
            elif cell[i][j]==2:
                color="green"
            elif cell[i][j]==3:
                color="red"
            elif cell[i][j]==4:
                color="#00008B"
            elif cell[i][j]==5:
                color="#DC143C"
            elif cell[i][j]==6:
                color="#7FFFD4"
            elif cell[i][j]==7:
                color="#FF4500"
            elif cell[i][j]=="X":
                color="black"
            else:
                color="#C0C0C0"


                
            laber=Label(sl,padx=10,pady=5,text=cell[i][j],fg=color,font=12).grid(row=i+1,column=j)
            btn=Button(sl,padx=9,text=" ",command=lambda i=i,j=j:forgetLabel(i,j)).grid(row=i+1,column=j)

            buttons.append(btn)
            

            
sl=Tk()
sl.geometry('308x352+600+280')

time1 = ''
sec=-1
begin=0
clock = Label(sl,font=('times', 20, 'normal'))
clock.grid(row=0, column=6,columnspan=3) 
tick()
chessBoard()


mainloop()
