from tkinter import *
import _thread
import threading
import time
import os
import pyautogui as pag
from ctypes import *



def Draw():
    global text1
    global text2
    x, y = pag.position()  # 返回鼠标的坐标
    posStr = str(x).rjust(4) + ',' + str(y).rjust(4)
    text1=Label(windows, font=('Helvetica', 12), text=posStr)
    text1.grid(row=1, column=1)
    text2=Label(windows, font=('Helvetica', 12), text=get_color(x,y))
    text2.grid(row=2, column=1)
    Label(windows, font=('Helvetica', 12), text='位置:').grid(row=1, column=0)
    Label(windows, font=('Helvetica', 12), text='rgb :').grid(row=2, column=0)
#def ana_color(x,y):
def get_color(x, y):
    gdi32 = windll.gdi32
    user32 = windll.user32
    hdc = user32.GetDC(None)  # 获取颜色值
    pixel = gdi32.GetPixel(hdc, x, y)  # 提取RGB值
    r = pixel & 0x0000ff
    g = (pixel & 0x00ff00) >> 8
    b = pixel >> 16
    rgb= str(r).rjust(4) + ',' + str(g).rjust(4)+ ',' + str(b).rjust(4)
    return rgb




def Refresher():
    global text1
    global text2
    x, y = pag.position()  # 返回鼠标的坐标
    posStr = str(x).rjust(4) + ',' + str(y).rjust(4)
    text1.configure(text=posStr)
    text2.configure(text=get_color(x,y))
    windows.after(10, Refresher)
    #threading.Timer(0.04, Refresher).start()

windows = Tk()
windows.title("取色器")
windows.geometry('320x100+1205+685')
Draw()
Refresher()
windows.mainloop()
