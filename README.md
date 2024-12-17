# Student-registration-system
from tkinter import *
from datetime import datetime
from tkinter import messagebox
from tkinter import filedialog
from PIL import ImageTk, Image
import os
from tkinter.ttk import Combobox
import openpyxl, xlrd
from openpyxl import Workbook
import pathlib
from tkinter import StringVar, OptionMenu,Button



background_image ="#06283d"
framebg="#EDEDED"
framefg="#06283d"


root = Tk()
root.title("Student Registration System")
root.geometry("1250x700+210+100")
root.config(bg=background_image)
gender =None


file=pathlib.Path("C:/Users/anshad c v/Desktop/StudentRegistration/StudentRegistration.xlsx")
if file.exists():
    pass
else:
    file=Workbook()
    sheet=file.active
    sheet['A1']="Registration Number"
    sheet['B1']="Name"
    sheet['C1']="Class"
    sheet['D1']="Gender"
    sheet['E1']="Date of Birth"
    sheet['F1']="Date of Registration"
    sheet['G1']="Religion"
    sheet['H1']="Skill"
    sheet['I1']="Father Name"
    sheet['J1']="Mother Name"
    sheet['K1']="Father Occupation"
    sheet['L1']="Mother Occupation"
    
    file.save('StudentRegistration.xlsx')
    
def Exit():
    root.destroy()
    
def showimage():    
    global filename
    global img
    filename=filedialog.askopenfilename(initialdir=os.getcwd(),title="Select image file",filetypes=(("png files","*.png"),("jpg files","*.jpg"),("all files","*.txt*")))
  
    img=(Image.open(filename))
    resized_image = img.resize((190, 190), Image.Resampling.LANCZOS)
    photo2=ImageTk.PhotoImage(resized_image)
    lbl.configure(image=photo2)
    lbl.image=photo2
    

def registration_no():
    file=openpyxl.load_workbook('StudentRegistration.xlsx')
    sheet=file.active
    row=sheet.max_row
    max_row=sheet.cell(row=row,column=1).value
    
    try:
        Registration.set(max_row+1)
    except:
        Registration.set(1)







def delete_student():
    reg_no = Search.get()  # Assume the Registration Number is entered in the Search field
    if not reg_no:
        messagebox.showerror("Error", "Please enter a Registration Number to delete.")
        return

    try:
        # Load the Excel workbook
        file = openpyxl.load_workbook('StudentRegistration.xlsx')
        sheet = file.active

        found = False
        for row in range(2, sheet.max_row + 1):  # Start from row 2 to skip headers
            cell_value = sheet.cell(row=row, column=1).value  # Assuming column 1 has Registration Numbers
            if cell_value == int(reg_no):
                sheet.delete_rows(row, 1)
                found = True
                break

        if found:
            file.save('StudentRegistration.xlsx')
            messagebox.showinfo("Success", f"Record with Registration Number {reg_no} deleted successfully.")
        else:
            messagebox.showerror("Error", f"Registration Number {reg_no} not found.")

    except Exception as e:
        messagebox.showerror("Error", f"An error occurred: {e}")



    

  

      
def  Clear():
    Name.set("")
    DOB.set("")
    Religion.set("")
    Skill.set("")
    F_name.set("")
    Father_occupation.set("")
    M_name.set("")
    Mother_occupation.set("")
    Class.set("Select Class")
    
    registration_no()
    
 
    saveButton.configure(state='normal')
    
    img1=PhotoImage(file="C:/Users/anshad c v/Desktop/StudentRegistration/upload photo.png")
    lbl.configure(image=img1)
    lbl.image=img1
    
    img=""
    
def Save():
    R1=Registration.get()
    N1=Name.get()
  
    try:
      G1=gender
    except:
      messagebox.showerror("Error","Please select Gender")
      return
    D2=DOB.get()
    D1=Date.get()
    R2=Religion.get()
    S1=Skill.get()
    fathername=F_name.get()
    mothername=M_name.get()
    F1=Father_occupation.get()
    M1=Mother_occupation.get()
    Cl1=Class.get()
    
    if N1=="" or D2=="" or D1=="" or R2=="" or S1=="" or fathername=="" or mothername=="" or F1=="" or M1=="":
        messagebox.showerror("Error","Please fill all the fields")
    else:
        file=openpyxl.load_workbook('StudentRegistration.xlsx')
        sheet=file.active
        sheet.cell(column=1,row=sheet.max_row+1,value=R1)
        sheet.cell(column=2,row=sheet.max_row,value=N1)
        sheet.cell(column=3,row=sheet.max_row,value=Cl1)
        sheet.cell(column=4,row=sheet.max_row,value=G1)
        sheet.cell(column=5,row=sheet.max_row,value=D2)
        sheet.cell(column=6,row=sheet.max_row,value=D1)
        sheet.cell(column=7,row=sheet.max_row,value=R2)
        sheet.cell(column=8,row=sheet.max_row,value=S1)
        sheet.cell(column=9,row=sheet.max_row,value=fathername)
        sheet.cell(column=10,row=sheet.max_row,value=mothername)
        sheet.cell(column=11,row=sheet.max_row,value=F1)
        sheet.cell(column=12,row=sheet.max_row,value=M1)
        
        file.save(r'StudentRegistration.xlsx')
        
        try:
            img.save("Student Images/"+str(R1)+".jpg")
        except:
            pass
            messagebox.showerror("info","profile image not available !!!")
            
            
        messagebox.showinfo("info","successfully data entered")
        Clear()
            
        registration_no()
        
             
           
            
            
def search():   
    text=Search.get()
    
    Clear()
    saveButton.configure(state='disable')
    
    file=openpyxl.load_workbook('StudentRegistration.xlsx')
    sheet=file.active
    
    for row in sheet.row:
        if row[0].value==int(text):
          name=row[0]
          registration_no_position=str(name)[14:-1]
          registration_number=(name)[15:-1]
       
    try:
        print(str(name))
    except:
        messagebox.showerror("Error","Registration number not found")
        

    x1=sheet.cell(row=int(registration_no_position),column=1).value
    x2=sheet.cell(row=int(registration_no_position),column=2).value
    x3=sheet.cell(row=int(registration_no_position),column=3).value
    x4=sheet.cell(row=int(registration_no_position),column=4).value
    x5=sheet.cell(row=int(registration_no_position),column=5).value
    x6=sheet.cell(row=int(registration_no_position),column=6).value
    x7=sheet.cell(row=int(registration_no_position),column=7).value
    x8=sheet.cell(row=int(registration_no_position),column=8).value
    x9=sheet.cell(row=int(registration_no_position),column=9).value
    x10=sheet.cell(row=int(registration_no_position),column=10).value
    x11=sheet.cell(row=int(registration_no_position),column=11).value
    x12=sheet.cell(row=int(registration_no_position),column=12).value
    
    Registration.set(x1)
    Name.set(x2)
    Class.set(x3)
    
    if x4=="female":
        R2.select()
    else:
        R1.select()
    
    DOB.set(x5)
    Date.set(x6)
    Religion.set(x7)
    Skill.set(x8)
    F_name.set(x9)
    M_name.set(x10)
    Father_occupation.set(x11)
    Mother_occupation.set(x12)
    
    img1=(Image.open("Student Images/"+str(x1)+".jpg"))
    resized_image = img1.resize((190, 190))
    photo2=ImageTk.PhotoImage(resized_image)
    lbl.configure(image=photo2)
    lbl.image=photo2
    

    
    
    
def update():
    R1=Registration.get()   
    N1=Name.get()
    G1=gender
    D2=DOB.get()
    D1=Date.get()
    R2=Religion.get()
    S1=Skill.get()
    fathername=F_name.get()
    mothername=M_name.get()
    F1=Father_occupation.get()
    M1=Mother_occupation.get()
    Cl1=Class.get()
    
    
    file=openpyxl.load_workbook('StudentRegistration.xlsx')
    sheet=file.active
    
    
    for row in sheet.rows:
        if row[0].value==int(R1):
            name=row[0]
            registration_no_position=str(name)[14:-1]
            registration_no=str(name)[15:-1]
    
    #sheet.cell(row=int(registration_no_position),column=1,value=R1)
    sheet.cell(row=int(registration_no_position),column=2,value=N1)
    sheet.cell(row=int(registration_no_position),column=3,value=Cl1)
    sheet.cell(row=int(registration_no_position),column=4,value=G1)
    sheet.cell(row=int(registration_no_position),column=5,value=D2)
    sheet.cell(row=int(registration_no_position),column=6,value=D1)
    sheet.cell(row=int(registration_no_position),column=7,value=R2)
    sheet.cell(row=int(registration_no_position),column=8,value=S1)
    sheet.cell(row=int(registration_no_position),column=9,value=fathername)
    sheet.cell(row=int(registration_no_position),column=10,value=mothername)
    sheet.cell(row=int(registration_no_position),column=11,value=F1)
    sheet.cell(row=int(registration_no_position),column=12,value=M1)
    
    
    file.save(r'StudentRegistration.xlsx') 
    
    try:
        img.save("Student Images/"+str(R1)+".jpg")
    except:
        pass
    messagebox.showerror("update","update successfully !!!")  
    Clear()
    
      
    
    
    
    
def selection():
    global gender
    value=radio.get()   
    if value==1:
        gender="Male"
        
    else:
        gender="Female"
            
        
    
    
    
Label(root,text="Email : anshadcv28@gmail.com",width='10',height='3',bg="#f0687c",anchor='e').pack(side=TOP,fill=X)
Label(root,text="STUDENT REGISTRATION",width='10',height='2',bg="#C36464",fg='#fff',font='arial 20 bold').pack(side=TOP,fill=X)  
    
Search=StringVar()
Entry(root,textvariable=Search,width='15',bd=2,font='arial 20').place(x=820,y=70)
imageicon3=PhotoImage(file="C:/Users/anshad c v/Desktop/StudentRegistration/search.png")
Srch=Button(root,image=imageicon3,text="Search",compound=LEFT,width=123,bg='#68ddfa',font="arial 13 bold",command=Search).place(x=1060,y=66)

imageicon4=PhotoImage(file="C:/Users/anshad c v/Desktop/StudentRegistration/Layer 4.png")
update_button=Button(root,image=imageicon4,bg='#c36464').place(x=110,y=64)

Label(root,text="Registration No",fg=framebg,bg=background_image,font='arial 13').place(x= 30,y=150 )
Label(root,text="Date",fg=framebg,bg=background_image,font='arial 13').place(x= 500,y=150 )

Registration=IntVar()
Date=StringVar()

reg_entry=Entry(root,textvariable=Registration,width='15',font='arial 10')
reg_entry.place(x=160,y=150)
registration_no()

today=datetime.today()
d1=today.strftime("%d/%m/%Y")
date_entry=Entry(root,textvariable=Date,width='15',font='arial 10').place(x=550,y=150)
Date.set(d1)
print(d1)


obj=LabelFrame(root,text="Student Details",width=900,height=250,bd=2,bg=framebg,fg=framefg,font=20,relief=GROOVE)
obj.place(x=30,y=200)

Label(obj,text="Full Name :",fg=framefg,bg=framebg,font='arial 13').place(x= 30,y=50)
Label(obj,text="Date of Birth :",fg=framefg,bg=framebg,font='arial 13').place(x= 30,y=100)
Label(obj,text="Gender :",fg=framefg,bg=framebg,font='arial 13').place(x= 30,y=150)

Label(obj,text="Class :",fg=framefg,bg=framebg,font='arial 13').place(x= 500,y=50)
Label(obj,text="Religion :",fg=framefg,bg=framebg,font='arial 13').place(x= 500,y=100)
Label(obj,text="Skills :",fg=framefg,bg=framebg,font='arial 13').place(x=500,y=150)

Name=StringVar()
name_entry=Entry(obj,textvariable=Name,width='20',font='arial 10').place(x=160,y=50)

DOB=StringVar()
dob_entry=Entry(obj,textvariable=DOB,width='20',font='arial 10').place(x=160,y=100)

radio=IntVar()
R1=Radiobutton(obj,text="Male",variable=radio,value=1,bg=framebg,fg=framefg,command=selection).place(x=150,y=150)
R2=Radiobutton(obj,text="Female",variable=radio,value=2,bg=framebg,fg=framefg,command=selection).place(x=200,y=150)

Religion=StringVar()
religion_entry=Entry(obj,textvariable=Religion,width='20',font='arial 10').place(x=630,y=100)

Skill=StringVar()
skill_entry=Entry(obj,textvariable=Skill,width='20',font='arial 10').place(x=630,y=150)

Class=Combobox(obj,values=['1','2','3','4','5','6','7','8','9','10','11','12'],width='17',font='Roboto 10',state="readonly")
Class.place(x=630,y=50)
Class.set("Select Class")

obj2=LabelFrame(root,text="Parents Details",width=900,height=220,bd=2,bg=framebg,fg=framefg,font=20,relief=GROOVE).place(x=30,y=470)

Label(obj2,text="Father Name :",fg=framefg,bg=framebg,font='arial 13').place(x=65,y=500)
Label(obj2,text="Occupation:",fg=framefg,bg=framebg,font='arial 13').place(x=65,y=575)

F_name=StringVar()
fname_entry=Entry(obj2,textvariable=F_name,width=20,font='arial 10').place(x=185,y=500)

Father_occupation=StringVar()
foccupation_entry=Entry(obj2,textvariable=Father_occupation,width='20',font='arial 10').place(x=185,y=575)

Label(obj2,text="Mother Name :",fg=framefg,bg=framebg,font='arial 13').place(x=525,y=500)
Label(obj2,text="Occupation:",fg=framefg,bg=framebg,font='arial 13').place(x=525,y=575)

M_name=StringVar()
mname_entry=Entry(obj2,textvariable=M_name,width='20',font='arial 10').place(x=662,y=500)

Mother_occupation=StringVar()
moccupation_entry=Entry(obj2,textvariable=Mother_occupation,width='20',font='arial 10').place(x=662,y=575)


f=Frame(root,bd=3,bg="black",width=200,height=200,relief=GROOVE)
f.place(x=1000,y=150)

img=PhotoImage(file="C:/Users/anshad c v/Desktop/StudentRegistration/upload photo.png")
lbl=Label(f,bg="black",image=img)
lbl.place(x=0,y=0)


Button(root,text="Upload",width='19',height='2',bg="lightblue",font='arial 12 bold',command=showimage).place(x=1000,y=370)

saveButton=Button(root,text="Save",width='19',height='2',bg="lightgreen",font='arial 12 bold',command=Save)
saveButton.place(x=1000,y=450)

Button(root,text="Reset",width='19',height='2',bg="lightpink",font='arial 12 bold',command=Clear).place(x=1000,y=530)

Button(root,text="Exit",width='19',height='2',bg="grey",font='arial 12 bold',command=Exit).place(x=1000,y=610)

Button(root, text="Delete", width=10, height=1, bg="red", font="arial 12 bold", command=delete_student).place(x=1050, y=675)












root.mainloop()
