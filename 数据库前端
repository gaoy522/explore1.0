import tkinter.messagebox
from tkinter import*
import pymssql


#数据库连接
Table='Book'
server = "127.0.0.1"
user = "sa"
password = "123"
database = "db_library"
conn = pymssql.connect(server, user, password, database, charset='utf8')
cursor = conn.cursor()



##登陆界面
def home_page():
    global e1
    global e2
    home_page=Tk()
    home_page.geometry('240x135+600+280')
    home_page.title("登陆")
    
    v1 = StringVar()
    v2 = StringVar()
    library=Label(home_page,font=('Helvetica',22,'bold'),text='图书管理系统').grid(row=1,columnspan=5)
    lab1=Label(home_page,font=1,text="账号").grid(row=2,column=0)
    lab2=Label(home_page,font=4,text="密码").grid(row=3,column=0)
    e1=Entry(home_page,bd=5,textvariable=v1,validate='focusout')
    e2=Entry(home_page,show="*",bd=5,textvariable=v2,validate='focusout')
    e1.grid(row=2,column=1,columnspan=5)
    e2.grid(row=3,column=1,columnspan=5)
    button1=Button(home_page,font=('Helvetica',11),text='登陆',command=ctrl_page).grid(row=4,column=2)

    
##登陆到控制界面
def ctrl_page():
    admininfo = ("SELECT id,password FROM admins").encode("utf8")
    cursor.execute(admininfo)
    row = cursor.fetchone()
    while row:
        a=int(row[0])
        b=int(row[1])
        row = cursor.fetchone()
        
        try:
            if int(e1.get()) == a and int(e2.get()) == b:

                ctrl_page=Tk()
                ctrl_page.geometry('240x320+600+240')
                ctrl_page.title("图书管理系统")
                library=Label(ctrl_page,font=('Helvetica',18,'bold'),text='图书管理系统').grid(row=1,columnspan=5)
                button1=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='所有书籍信息',command=allTable).grid(row=2,column=4)
                button1=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='查询书籍信息',command=selectTable).grid(row=3,column=4)
                button2=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='书籍借阅',command=borrowTable).grid(row=4,column=4)
                button3=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='借书证办理',command=readerTable).grid(row=6,column=4)
                button4=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='书籍归还',command=returnTable).grid(row=5,column=4)
                button5=Button(ctrl_page,bd=5,font=('Helvetica',15),width=12,text='所有读者信息',command=allReaderTable).grid(row=7,column=4)
                break
            tkinter.messagebox.showerror("错误","账号或密码错误。")
        except:
            continue


#查询所有书籍信息
def allTable():
    allTable2(Table)

def allTable2(Table):
    all_page=Tk()
    all_page.geometry('580x250+400+300')
    all_page.title("书籍信息")
    sql = ("SELECT * FROM book").encode("utf8")
    cursor.execute(sql)
    row = cursor.fetchone()
    info=['编号','类别','书名','作者','出版社','出版时间','价格','是否已借']
    for i in range(8):
        Label(all_page,font=('Helvetica',10,'bold'),text=info[i]).grid(row=0,column=i)
    while row:
        try:
            for j in range(10):
                for i in range(8):
                    if i==2 or i==3 or i==4 or i==5 or i==7:
                        Label(all_page,font=('Helvetica',10),text=row[i].encode('latin-1').decode('gbk')).grid(row=j+1,column=i)
                    else:
                        Label(all_page,font=('Helvetica',10),text=row[i]).grid(row=j+1,column=i)
                row = cursor.fetchone()
        except:
            continue


#查询图书信息        
def selectTable():
    global sT
    select_page=Tk()
    select_page.geometry('160x89+650+280')
    st = StringVar()
    Label(select_page,font=1,text="图书名称").grid(row=0,column=0)
    sT=Entry(select_page,bd=5,textvariable=st,validate='focusout')
    sT.grid(row=1,column=0)
    Button(select_page,bd=4,font=('Helvetica',10),width=12,text='查询',command=selectTable2).grid(row=3,column=0)


def selectTable2():
    inquire_page=Tk()
    inquire_page.geometry('550x200+400+300')
    inquire_page.title("图书信息")
    selectinfo=str(sT.get())
    sql = ("SELECT * FROM book where bookname='%s'"%selectinfo).encode("utf8")
    cursor.execute(sql)
    row = cursor.fetchone()
    info=['编号','类别','书名','作者','出版社','出版时间','价格','是否已借']
    for i in range(8):
        Label(inquire_page,font=('Helvetica',10,'bold'),text=info[i]).grid(row=0,column=i)
    while row:
        try:
            for j in range(10):
                for i in range(8):
                    if i==2 or i==3 or i==4 or i==5 or i==7:
                        Label(inquire_page,font=('Helvetica',10),text=row[i].encode('latin-1').decode('gbk')).grid(row=j+1,column=i)
                    else:
                        Label(inquire_page,font=('Helvetica',10),text=row[i]).grid(row=j+1,column=i)
                row = cursor.fetchone()
        except:
            continue
    

#借书        
def borrowTable():
    global bwE1
    global bwE2
    global bwE3
    borrow_page=Tk()
    borrow_page.geometry('265x189+600+240')
    borrow_page.title("借书")
    v1 = StringVar()
    v2 = StringVar()
    v3 = StringVar()

    borrow0=Label(borrow_page,font=('Helvetica',15),text='书籍借阅').grid(row=0)
    borrow1=Label(borrow_page,font=('Helvetica',15),text='图书编号').grid(row=1)
    borrow2=Label(borrow_page,font=('Helvetica',15),text='操作员编号').grid(row=2)
    borrow3=Label(borrow_page,font=('Helvetica',15),text='借阅证编号').grid(row=3)
    borrow5=Button(borrow_page,font=('Helvetica',15),text='确定',command=borrowInsert).grid(row=5)
    bwE1=Entry(borrow_page,bd=5,textvariable=v1,validate='focusout')
    bwE2=Entry(borrow_page,bd=5,textvariable=v2,validate='focusout')
    bwE3=Entry(borrow_page,bd=5,textvariable=v3,validate='focusout')
    bwE1.grid(row=1,column=1)
    bwE2.grid(row=2,column=1)
    bwE3.grid(row=3,column=1)


def borrowInsert():
    bwe1= int(bwE1.get())
    bwe2= str(bwE2.get())
    bwe3= str(bwE3.get())
    try:
        sql = "insert into Borrow(bookid,id,cardid) values(%d, %s, %s)"
        data = [ (bwe1,bwe2,bwe3)]
        cursor.executemany(sql, data)
        sql = ("SELECT result FROM(SELECT ROW_NUMBER() over (ORDER BY recordid) as no,* from record) AS L WHERE no=(SELECT COUNT(*) FROM Record)")
        cursor.execute(sql)
        row=cursor.fetchone()
        ce=row[0].encode('latin-1').decode('gbk')

        tkinter.messagebox.showinfo("成功",ce) 
    except:
        sql = ("SELECT result FROM(SELECT ROW_NUMBER() over (ORDER BY recordid) as no,* from record) AS L WHERE no=(SELECT COUNT(*) FROM Record)")
        cursor.execute(sql)
        row=cursor.fetchone()
        cd=row[0].encode('latin-1').decode('gbk')

        tkinter.messagebox.showerror("错误",cd) 
#还书
def returnTable():
    global rT
    return_page=Tk()
    return_page.geometry('160x89+650+280')
    rt = StringVar()
    Label(return_page,font=1,text="图书编号").grid(row=0,column=0)
    rT=Entry(return_page,bd=5,textvariable=rt,validate='focusout')
    rT.grid(row=1,column=0)
    Button(return_page,bd=4,font=('Helvetica',10),width=12,text='查询',command=returnTable2).grid(row=3,column=0)

def returnTable2():
    returnT= int(rT.get())
    try:
        sql = ("DELETE FROM Borrow WHERE bookid=%d"%returnT)
        cursor.execute(sql)
        sql = ("SELECT result FROM(SELECT ROW_NUMBER() over (ORDER BY recordid) as no,* from record) AS L WHERE no=(SELECT COUNT(*) FROM Record)")
        cursor.execute(sql)
        row=cursor.fetchone()
        ce=row[0].encode('latin-1').decode('gbk')

        tkinter.messagebox.showinfo("成功",ce) 
    except:
        sql = ("SELECT result FROM(SELECT ROW_NUMBER() over (ORDER BY recordid) as no,* from record) AS L WHERE no=(SELECT COUNT(*) FROM Record)")
        cursor.execute(sql)
        row=cursor.fetchone()
        cd=row[0].encode('latin-1').decode('gbk')

        tkinter.messagebox.showerror("错误",cd) 
 
 ##   conn.commit()
    
#读者注册
def readerTable():
    global rdE1
    global rdE2
    global rdE3
    global rdE4
    global rdE5
    global rdE6
    reader_page=Tk()
    reader_page.geometry('265x189+600+240')
    reader_page.title("注册")
    r1 = StringVar()
    r2 = StringVar()
    r3 = StringVar()
    r4 = StringVar()
    r5 = StringVar()
    r6 = StringVar()
    borrow0=Label(reader_page,font=('Helvetica',13),text='借书证办理').grid(row=0)
    borrow1=Label(reader_page,font=('Helvetica',12),text='姓名').grid(row=1)
    borrow2=Label(reader_page,font=('Helvetica',12),text='年龄').grid(row=2)
    borrow3=Label(reader_page,font=('Helvetica',12),text='性别').grid(row=3)
    borrow4=Label(reader_page,font=('Helvetica',12),text='注册时间').grid(row=4)
    borrow5=Label(reader_page,font=('Helvetica',12),text='月').grid(row=4,column=4)
    borrow6=Label(reader_page,font=('Helvetica',12),text='日').grid(row=4,column=6)
    borrow7=Label(reader_page,font=('Helvetica',12),text='年').grid(row=4,column=2)
    borrow8=Button(reader_page,font=('Helvetica',12),text='确定',command=readerInsert).grid(row=5)
    rdE1=Entry(reader_page,bd=5,textvariable=r1,validate='focusout')
    rdE2=Entry(reader_page,bd=5,textvariable=r2,validate='focusout')
    rdE3=Entry(reader_page,bd=5,textvariable=r3,validate='focusout')
    rdE4=Entry(reader_page,bd=5,width=4,textvariable=r4,validate='focusout')
    rdE5=Entry(reader_page,bd=5,width=2,textvariable=r5,validate='focusout')
    rdE6=Entry(reader_page,bd=5,width=2,textvariable=r6,validate='focusout') 
    rdE1.grid(row=1,column=1,columnspan=6)
    rdE2.grid(row=2,column=1,columnspan=6)
    rdE3.grid(row=3,column=1,columnspan=6)
    rdE4.grid(row=4,column=1)
    rdE5.grid(row=4,column=3)
    rdE6.grid(row=4,column=5)

def readerInsert():
    rde1=str(rdE1.get())
    rde2=int(rdE2.get())
    rde3=str(rdE3.get())
    rde4=str(rdE4.get())
    rde5=str(rdE5.get())
    rde6=str(rdE6.get())
    rde7=str(rde4)+'-'+str(rde5)+'-'+str(rde6)
    print(rde7)
    try:
        sql = "insert into Reader(readername,age,sex,begindate) values(%s, %d, %s,%s)"
        data = [ (rde1,rde2,rde3,rde7)]
        cursor.executemany(sql, data)
        cardId = ("SELECT cardid FROM reader where readername='%s'"%rde1)
        cursor.execute(cardId)
        row = cursor.fetchone()
        tkinter.messagebox.showinfo("提示","注册成功，账号为"+row[0])
    except:
        tkinter.messagebox.showerror("错误","请检查输入信息。")    
        
#所有读者信息
def allReaderTable():
    allReader_page=Tk()
    allReader_page.geometry('550x500+400+200')
    allReader_page.title("读者信息")
    sql = ("SELECT * FROM Reader").encode("utf8")
    cursor.execute(sql)
    row = cursor.fetchone()
    info=['借书证号','姓名','年龄','性别','借书证办理','借书证过期','可借数量','押金','罚金']
    for i in range(9):
        Label(allReader_page,font=('Helvetica',10,'bold'),text=info[i]).grid(row=0,column=i)
    while row:
        try:
            for j in range(100):
                for i in range(9):
                    if i==1 or i==3:
                        Label(allReader_page,font=('Helvetica',10),text=row[i].encode('latin-1').decode('gbk')).grid(row=j+1,column=i)
                    else:
                        Label(allReader_page,font=('Helvetica',10),text=row[i]).grid(row=j+1,column=i)
                row = cursor.fetchone()
        except:
            break

#打开登陆界面
                                   
home_page()

