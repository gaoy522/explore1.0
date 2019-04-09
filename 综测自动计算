import xlrd
import xlwt
import xlutils
from xlutils.copy import copy
import tkinter.messagebox
from tkinter import*

##前端
def home_page():
    global e1
    global e2
    global e3
    global e4
    global e5
    global e6
    global e7
    global e8
    global e9
    global e10
    global e11
    home_page=Tk()
    home_page.geometry('380x176+600+280')
    home_page.title("成绩计算")

    v1 = StringVar()
    v2 = StringVar()
    v3 = StringVar()
    v4 = StringVar()
    v5 = StringVar()
    v6 = StringVar()
    v7 = StringVar()
    v8 = StringVar()
    v9 = StringVar()
    v10 = StringVar()
    v11 = StringVar()
    lab0 = Label(home_page,  text="定位").grid(row=1, column=0)
    lab1 = Label(home_page,  text="原文件路径").grid(row=4, column=0)
    lab2 = Label(home_page,  text="生成文件路径").grid(row=5, column=0)
    lab3 = Label(home_page,  text="起始行").grid(row=0, column=1)
    lab4 = Label(home_page,  text="德能分列").grid(row=0, column=2)
    lab5 = Label(home_page,  text="学业分起始").grid(row=0, column=3)
    lab6 = Label(home_page,  text="学业分终止").grid(row=0, column=4)
    lab7 = Label(home_page,  text="体能列").grid(row=0, column=5)
    lab8 = Label(home_page,  text="比例").grid(row=3, column=0)
    lab9 = Label(home_page,  text="德能比例").grid(row=2, column=1)
    lab10 = Label(home_page,  text="学业比例").grid(row=2, column=2)
    lab11 = Label(home_page,  text="体能比例").grid(row=2, column=3)
    lab12 = Label(home_page,  text="工作表名称").grid(row=2, column=4,columnspan=2)
    e1 = Entry(home_page,  width=40,textvariable=v1, validate='focusout')
    e2 = Entry(home_page,  width=40,textvariable=v2, validate='focusout')
    e3 = Entry(home_page,  width=6,textvariable=v3, validate='focusout')
    e4 = Entry(home_page,  width=6,textvariable=v4, validate='focusout')
    e5 = Entry(home_page,  width=6,textvariable=v5, validate='focusout')
    e6 = Entry(home_page,  width=6,textvariable=v6, validate='focusout')
    e7 = Entry(home_page, width=6, textvariable=v7, validate='focusout')
    e8 = Entry(home_page,  width=6,textvariable=v8, validate='focusout')
    e9 = Entry(home_page,  width=6,textvariable=v9, validate='focusout')
    e10 = Entry(home_page,  width=6,textvariable=v10, validate='focusout')
    e11 = Entry(home_page, width=14, textvariable=v11, validate='focusout')
    e1.grid(row=4, column=1, columnspan=6)
    e2.grid(row=5, column=1, columnspan=6)
    e3.grid(row=1, column=1)
    e4.grid(row=1, column=2)
    e5.grid(row=1, column=3)
    e6.grid(row=1, column=4)
    e7.grid(row=1, column=5)
    e8.grid(row=3, column=1)
    e9.grid(row=3, column=2)
    e10.grid(row=3, column=3)
    e11.grid(row=3, column=4,columnspan=2)
    button1 = Button(home_page, text='生成成绩单', command=ItLikesFriedNoodles).grid(row=6, column=2,columnspan=2)





'''xyfqs   xyfzz  tnl'''

def ItLikesFriedNoodles():
    source1=e1.get()
    source2=e2.get()
    bili1=float(e8.get())
    bili2=float(e9.get())
    bili3=float(e10.get())
    sheetname=e11.get()
    qsh=int(e3.get())-1
    dnfl=int(e4.get())-1
    xyfqs=int(e5.get())-1
    xyfzz=int(e6.get())-1
    tnl=int(e7.get())-1

    old_excel = xlrd.open_workbook(source1, formatting_info=True)
    new_excel = copy(old_excel)
    ws = new_excel.get_sheet(sheetname)

    #######################开始计算
    workbook=xlrd.open_workbook(source1)
    worksheet=workbook.sheet_by_name(sheetname)
    nrows=worksheet.nrows

    num=0
    sum=0
    score=0
    aver=0
    for i in range(qsh,nrows):##计算人数
        if(worksheet.cell_value(i,0)!=""):
            num=num+1
        else:
            break

    ##print(n)
    n=num+qsh

    list=[]
    for i in range(qsh,nrows):##6为开始列数##德能分
        cell_value1=worksheet.cell_value(i,dnfl)
        if(i==n):
            break
        dnf=float(cell_value1)*bili1
        ws.write(i,2,dnf)
      ##  print(dnf)

    ##for i in range(6,nrows):##6为开始列数
        cell_value2=worksheet.cell_value(i,tnl)
        if(i==n):
            break
        if(cell_value2!=""):
            tncs=float(cell_value2)*bili3
            ws.write(i,tnl+1,tncs)
       ## print(tncs)
    ##print("##########################")



    ##for i in range(6,nrows):##6为开始列数
        if(i==n):
            break
        for j in range(3,xyfzz+1):
            if(worksheet.cell_value(i,j)==""):
                continue
            else:
                cell_value3 = float(worksheet.cell_value(i, j))
            cell_value4 = float(worksheet.cell_value(qsh-1, j))
            sum=cell_value3*cell_value4+sum##总分
            score=float(worksheet.cell_value(qsh-1,j))+score

        aver=sum/score*0.9
        ws.write(i,xyfzz+1,aver)
        if (worksheet.cell_value(i, xyfzz+2) != ""):
            aver=aver+worksheet.cell_value(i, xyfzz+2)
        ws.write(i,xyfzz+3,aver)
        aver1=aver*bili2
        ws.write(i,xyfzz+4,aver1)

        fin=aver1+dnf+tncs
        ws.write(i,tnl+2,fin)
        #######################
        list.append(fin)
        ##########################
        ##print(fin)
        sum=0
        score=0
    print("##################")

    gknum=0
    gk=0
    gklist=[]
    bgklist=[]
    for i in range(qsh,n):
        if(worksheet.cell_value(i, j)!=''):
            value=float(worksheet.cell_value(i,dnfl))
            if(value<60):
                ws.write(i, tnl+4, "德能分低于59")
                gk=1


        if (worksheet.cell_value(i, j) != ''):
            value=float(worksheet.cell_value(i,tnl))
            if(value<60):
                ws.write(i, tnl+4, "体育挂科")
                gk=1


        for j in range(xyfqs,xyfzz+1):
            if(worksheet.cell_value(i, j)!=''):
                value = float(worksheet.cell_value(i, j))
                if (value < 60):
                    ws.write(i, tnl+4, "挂科")
                    gk=1
            else:
                continue
        if(gk==1):
            gknum=gknum+1
            gklist.append(i-qsh)
        else:
            bgklist.append(i-qsh)
        gk=0



    print(gknum)
    MAX=0
    NO=0
    bgknum=num-gknum


    ##bgk不挂科
    lock=0##
    for i in range(len(list)):
        for j in range(len(list)):
            for k in range(gknum):
                if(j==gklist[k]):
                    lock=1
                    break

            if(lock==1) :
                lock=0
                continue
            else:
                if (list[j] > MAX):
                    MAX = list[j]
                    NO = j
                    ws.write(NO + qsh, tnl+3, i + 1)

        print(NO+qsh)
        print(MAX)
        MAX=0
        list[NO]=0


    #gk挂科
    lock=0##
    for i in range(gknum):
        for j in range(len(list)):
            for k in range(bgknum):
                if(j==bgklist[k]):
                    lock=1
                    break

            if(lock==1) :
                lock=0
                continue
            else:
                if (list[j] > MAX):
                    MAX = list[j]
                    NO = j
                    ws.write(NO + qsh, tnl+3, i + 1+bgknum)

        print(NO+qsh)
        print(MAX)
        MAX=0
        list[NO]=0

    ##book.save("C:\\Users\\91692\\Desktop\\example\\new163.xls")
    new_excel.save(source2)
    tkinter.messagebox.showinfo("综合测评表", "运行成功")

home_page()
mainloop()
