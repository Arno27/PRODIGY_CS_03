# PRODIGY_CS_03

It is a python program to check the complexity of a password. 
It also provides a graphical user interface to user so that they can check there password strength.
I have used tkinter module, so that it's output will be in a message box. Also you there are buttons to check the strength of password and reset button to reset the whole message box and you can check strength of another password.

import string
import re
from tkinter import *
from tkinter import messagebox
import os

def check_pwd():
    password = code.get()
    global remark2
    global remark_label
    strength = 0
    remark = StringVar()
    remark2 = StringVar()
    low_count = up_count = num_count = wspace_count = special_count = 0

    

    for char in list(password):
        if char in string.ascii_lowercase:
            low_count += 1
        elif char in string.ascii_uppercase:
            up_count += 1
        elif char in string.digits:
            num_count += 1
        elif char == ' ':
            wspace_count += 1
        else:
            special_count += 1

    if low_count >= 1:
        strength += 1
    if up_count >= 1:
        strength += 1
    if num_count >= 1:
        strength += 1
    if wspace_count >= 1:
        strength += 1
    if special_count >= 1:
        strength += 1
    if len(password) > 8:
        strength += 1


    if len(password) < 8:
        remark2="Password must contain at least 8 characters. "
    elif not re.search("[A-Z]", password):
        remark2="Password must contain at least one uppercase character. "
    elif not re.search("[a-z]", password):
        remark2="Password must contain at least one lowercase character. "
    elif not re.search("[0-9]", password):
        remark2="Password must contain at least one number. "
    elif not re.search(" ", password):
        remark2="Password must contain at least one space. "
    else:
        remark2="Password is strong. "

    if strength == 1 or strength == 2:
        remark="!!VERY WEAK PASSWORD!!"
    if strength == 3 or strength == 4:
        remark="!!VERY GOOD PASSWORD!!"
    if strength == 5 or strength == 6:
        remark="!! STRONG PASSWORD !!"
    
    remark_label.config(text=remark2 + remark, fg="red", font=("calibri", 8))




def main_screen():
    
    global code
    global screen
    global remark_label

    screen = Tk()
    screen.geometry("560x200")

    def reset():
        code.set("")
        remark_label.config(text="")

    screen.title("PASSWORD COMPLEXITY CHECKER")
    Label( text = "PASSWORD :", fg = "black", font = ("calbri",14)).place(x=20,y=35)
    code = StringVar()
    Entry(textvariable=code, width=25 , bd=0 , font = ("arial",20) ,border = 2, show="*").place(x=150,y=33)

    Button(text="CHECK", height="2", width=18,bg="#ed3833",fg="white",bd=0, command = check_pwd).place(x=140,y=113)
    Button(text="RESET", height="2", width=18,bg="#1089ff",fg="white",bd=0, command = reset).place(x=290,y=113)

    remark_label = Label(screen, text="", fg="red", font=("calibri", 8))
    remark_label.place(x=150, y=73)


    screen.mainloop()

main_screen()
