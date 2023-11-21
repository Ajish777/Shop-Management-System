
# Project File Structure:
Steps for developing shop / store management system:

1. Install tkinter
2. Importing Libraries
3. Initializing the project window
4. Developing connection and executing the query
5. Function for adding stock
6. Function for viewing stock
7. Defining labels and buttons
8. Function for generating bill
9. Rest Code

# 1. Install tkinter:
The simplest way to develop a graphical user interface is tkinter. Menus, date fields, buttons can be constructed with the help of this widget. To install tkinter on your system, run the command mentioned below on your terminal window or command prompt.


-> pip install tkinter


# 2. Importing Libraries:

from tkinter import *

from tkinter import ttk

from tkcalendar import DateEntry

from tkinter import messagebox

import sqlite3  as db

# Code Explanation:

a. Ttk: Tk themed widget set can be accessed with the help of this module.

b. tkcalendar: DateEntry and calendar widgets are provided with the help of this module.

c. messagebox: Message Boxes are displayed on the screen with the help of messagebox.

d. sqlite3: It is a database engine.

# 3. Initializing the project window:
mainwindow=Tk()

mainwindow.title("Project Shop Management Project")

tab = ttk.Notebook(mainwindow) 

window1= ttk.Frame(tab)

window2=ttk.Frame(tab)
 
tab.add(window1, text ='stock') 

tab.add(window2, text ='sell') 

tab.pack(expand = 1, fill ="both") 

# Code Explanation:

a. ttk.Frame(): It is a rectangular container which is for other widgets.

b. ttk.Notebook(): It is responsible for the management of collection of windows. It also displays one screen at a time.

c. add(): It adds the text on the screen.

d.pack(): First of all the widgets are placed in the block and then after that they are placed on the screen.

# 4. Developing connection and executing the query:

def establishconnect():
    
    connectobject = db.connect("shopManagement.db")
    c = connectobject.cursor()
    sql = '''
    create table if not exists sell (
        date string,
        product string,
        price number,
        quantity number,
        total number
        )
    '''
    c.execute(sql)
    connectobject.commit()   
 
establishconnect()    
def connection2():
    
    connectobject2 = db.connect("shopManagement.db")
    c = connectobject2.cursor()
    sql = '''
    create table if not exists stock (
        date string,
        product string,
        price number,
        quantity number
        )
    '''
    c.execute(sql)
    connectobject2.commit()   
    connection2()

# Code Explanation:

a. db.connect(): It is used to connect to the database.

b. cursor(): It shows the current position of the mouse.

c. execute(): It helps in the execution process.

d. commit(): The changes made by the user in the database are confirmed by commit().

# 5. Function for adding stock:
def Stock():
    global dateE2,quantity,name,price
 
    connectobject = db.connect("shopManagement.db")
    c = connectobject.cursor()  
    sql = '''
            INSERT INTO stock VALUES 
            (?, ?, ?, ?)
            '''
    c.execute(sql,(dateE2.get(),name.get(),price.get(),quantity.get()))
    connectobject.commit() 

# Code Explanation:

a. Stock(): This function helps in adding the stock.

b. get(): It returns the text as a string.

# 6. Function for viewing stock:
def viewingStock():
    
    connectobject = db.connect("shopManagement.db")
    c = connectobject.cursor()  
 
    sql = 'Select * from stock'
    c.execute(sql)
 
    rows=c.fetchall()
    viewingarea2.insert(END,f"Date \tProduct\t  Price\t  Quantity\t \n")
    
    for i in rows:
        allrows=""
        for j in i:
            allrows+=str(j)+'\t'
        allrows+='\n'
        viewingarea2.insert(END,allrows)

# Code Explanation:

a. viewingstock(): This function helps to view the stock.

b. insert(): It helps in the insertion of the string at a specified block.

c. fetchall(): All rows of queries result set is returned with fetchall().

# 7. Defining labels and buttons:
dateL=Label(window1,text="Date",width=12,font=('arial',15,'bold'))

dateL.grid(row=0,column=0,padx=7,pady=7)
 
dateE2=DateEntry(window1,width=12,font=('arial',15,'bold'))
dateE2.grid(row=0,column=1,padx=7,pady=7)
 
l1=Label(window1, text="Product",font=('arial',15,'bold'),width=12)
l1.grid(row=1,column=0,padx=7,pady=7)
 
l1=Label(window1, text="Price",font=('arial',15,'bold'),width=12)
l1.grid(row=2,column=0,padx=7,pady=7)
 
l1=Label(window1, text="Quantity",font=('arial',15,'bold'),width=12)
l1.grid(row=3,column=0,padx=7,pady=7)
 
name=StringVar()
price=IntVar()
quantity=IntVar()
 
Name=Entry(window1,textvariable=name,font=('arial',15,'bold'),width=12)
Name.grid(row=1,column=1,padx=7,pady=7)
 
Price=Entry(window1,textvariable=price,font=('arial',15,'bold'),width=12)
Price.grid(row=2,column=1,padx=7,pady=7)
 
Quantity=Entry(window1,textvariable=quantity,font=('arial',15,'bold'),width=12)
Quantity.grid(row=3,column=1,padx=7,pady=7)
 
addbutton=Button(window1,command=Stock,text="Add",
font=('arial',15,'bold'),bg="pink",width=20)
 
addbutton.grid(row=4,column=1,padx=7,pady=7)
 
viewingarea2=Text(window1)
viewingarea2.grid(row=5,column=0,columnspan=2)
 
viewbutton2=Button(window1,command=viewingStock,text="View Stock",
font=('arial',15,'bold'),bg="pink",width=20 )
 
viewbutton2.grid(row=4,column=0,padx=7,pady=7)

# Code Explanation:

a. Label(): It helps in the implementation of display boxes.

b. DateEntry(): It is useful in the selection of dates.

c. Button(): This widget adds buttons to the application.

d. StringVar(): Management of the value of widgets such as labels or entries is done with this widget.

e. IntVar(): It is responsible for returning the value as an integer.

f. Entry(): Text strings are accepted with the help of this widget.

# 8. Function for generating bill:
def Bill():
    
    connectobject = db.connect("shopManagement.db")
    c = connectobject.cursor()  
 
    global areaforbill
    if p1quant.get()==0 and p2quant.get()==0 and p3quant.get()==0 and p4quant.get()==0:
        messagebox.showerror("Error","No product purchased")
    else:
        areaforbill.delete('1.0',END)
        areaforbill.insert(END,"\t|| ProjectGurukul Shop Management Project ||")
        areaforbill.insert(END,"\n_________________________________________\n")
        areaforbill.insert(END,"\nDate\t Price\tProducts\t   QTY\t Total")
        areaforbill.insert(END,"\n==========================================")
 
        price= IntVar()
        price2=IntVar()
        price3=IntVar()
        price4=IntVar()
 
        print(datee.get())
        price=price2=price3=price4=0
 
        if p1quant.get()!=0:
            price=p1quant.get()*pricep1.get()
            print(price)
            areaforbill.insert(END,f"\n{datee.get()}\t Product-1 \t{pricep1.get()}\t {p1quant.get()}\t {price}")
 
            sql = '''
            INSERT INTO Sell VALUES 
            (?, ?, ?, ?,?)
            '''
            c.execute(sql,(datee.get(),'Product-1',pricep1.get(),p1quant.get(),price))
            connectobject.commit() 
 
        if p2quant.get()!=0:
            price2=(p2quant.get()*pricep2.get())
            print(price2)
            areaforbill.insert(END,f"\n{datee.get()}\t Product-2 \t{pricep2.get()}\t {p2quant.get()}\t {price2}")
 
            sql = '''
            INSERT INTO Sell VALUES 
            (?, ?, ?, ?,?)
            '''
            print(datee.get(),'Product-2',pricep2.get(),p2quant.get(),price2)
            c.execute(sql,(datee.get(),'Product-2',pricep2.get(),p2quant.get(),price2))
            connectobject.commit() 
 
        if p3quant.get()!=0:
            price3=p3quant.get()*pricep1.get()
            print(price3)
            areaforbill.insert(END,f"\n{datee.get()}\tProduct-3 \t{pricep3.get()}\t {p3quant.get()}\t {price3}")
 
            sql = '''
            INSERT INTO Sell VALUES 
            (?, ?, ?, ?,?)
            '''
            c.execute(sql,(datee.get(),'Product-3',pricep3.get(),p3quant.get(),price3))
            connectobject.commit() 
 
        if p4quant.get()!=0:
            price4=p4quant.get()*pricep1.get()
            areaforbill.insert(END,f"\n{datee.get()}\tProduct-4 \t{pricep4.get()}\t {p4quant.get()}\t {price4}")
 
            sql = '''
            INSERT INTO Sell VALUES 
            (?, ?, ?, ?,?)
            '''
            c.execute(sql,(datee.get(),'Product-4',pricep4.get(),p4quant.get(),price4))
            connectobject.commit() 
 
        Total=IntVar()
        Total=price+price2+price3+price4
 
        quantity=IntVar()
        quantity=p1quant.get()+p2quant.get()+p3quant.get()+p4quant.get()
        areaforbill.insert(END,f"\nTotal \t \t  \t{quantity}\t {Total}")

# Code Explanation:

a. Bill(): This function helps in generating the bill.

b. showerror(): This widget helps in displaying an error message on the screen.

c. delete(): This widget helps in the deletion of the text.

d. insert(): It helps in the insertion of text at the specified block.

# 9. Rest Code:
def view():
    
    connectobject = db.connect("shopManagement.db")
    c = connectobject.cursor()  
 
    sql = 'Select * from Sell'
    c.execute(sql)
 
    rows=c.fetchall()
    viewingarea.insert(END,f"Date\t Product\t  Price of 1\t  Quantity\t  Price\n")
    
    
    for i in rows:
        allrows=""
        for j in i:
            allrows+=str(j)+'\t'
        allrows+='\n'
        viewingarea.insert(END,allrows)
 
datel=Label(window1,text="Date",width=12,font=('arial',15,'bold'))
datel.grid(row=0,column=0,padx=7,pady=7)
 
datee=DateEntry(window1,width=12,font=('arial',15,'bold'))
datee.grid(row=0,column=1,padx=7,pady=7)
 
l1=Label(window1, text="Product Name",font=('arial',15,'bold'),width=12)
l1.grid(row=1,column=0,padx=7,pady=7)
 
 
namep1=StringVar()
namep1.set('Maggie')
 
pricep1=IntVar()
pricep1.set(80)
 
p1quant=IntVar()
p1quant.set(0)
 
l1=Label(window2, text=namep1.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=2,column=0,padx=7,pady=7)
 
l1=Label(window2, text=pricep1.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=2,column=1,padx=7,pady=7)
 
t1=Entry(window2,textvariable=p1quant,font=('arial',15,'bold'),width=12)
t1.grid(row=2,column=2,padx=7,pady=7)
 
 
namep2=StringVar()
namep2.set('biscuits')
 
pricep2=IntVar()
pricep2.set(20)
 
p2quant=IntVar()
p2quant.set(0)
 
l1=Label(window2, text=namep2.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=3,column=0,padx=7,pady=7)
 
l1=Label(window2, text=pricep2.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=3,column=1,padx=7,pady=7)
 
t1=Entry(window2,textvariable=p2quant,font=('arial',15,'bold'),width=12)
t1.grid(row=3,column=2,padx=7,pady=7)
 
namep3=StringVar()
namep3.set('Instant Noodles')
 
pricep3=IntVar()
pricep3.set(100)
 
p3quant=IntVar()
p3quant.set(0)
 
l1=Label(window2, text=namep3.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=4,column=0,padx=7,pady=7)
 
l1=Label(window2, text=pricep3.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=4,column=1,padx=7,pady=7)
 
t1=Entry(window2,textvariable=p3quant,font=('arial',15,'bold'),width=12)
t1.grid(row=4,column=2,padx=7,pady=7)
 
 
namep4=StringVar()
namep4.set('Rice')
 
pricep4=IntVar()
pricep4.set(400)
 
p4quant=IntVar()
p4quant.set(0)
 
l1=Label(window2, text=namep4.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=5,column=0,padx=7,pady=7)
 
l1=Label(window2, text=pricep4.get(),font=('arial',15,'bold'),width=12)
l1.grid(row=5,column=1,padx=7,pady=7)
 
t1=Entry(window2,textvariable=p4quant,font=('arial',15,'bold'),width=12)
t1.grid(row=5,column=2,padx=7,pady=7)
 
 
areaforbill=Text(window2)
 
submitbutton=Button(window2,command=Bill,text="Bill",
font=('arial',15,'bold'),bg="pink",width=20 )
 
submitbutton.grid(row=6,column=2,padx=7,pady=7)
 
viewbutton=Button(window2,command=view,text="View All Sellings",
font=('arial',15,'bold'),bg="pink",width=20 )
 
viewbutton.grid(row=6,column=0,padx=7,pady=7)
 
areaforbill.grid(row=9,column=2)
viewingarea=Text(window2)
viewingarea.grid(row=9,column=0)
 
mainloop()

# Code Explanation:

a. grid(): It puts the widget in a 2-dimensional table.

b. set(): It changes the value stored in a variable and sets the value.

c. Text(): It is useful when the user wants to insert multiline text.

# Python Store Management System Output:
![shop](https://github.com/Ajish777/Shop-Management-System/assets/110074935/b26e131c-4658-42a3-bcfd-0bd3d82e6384)





