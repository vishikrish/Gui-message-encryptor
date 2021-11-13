# Gui-message-encryptor
# tkitiner is a gui library in python
from tkinter import *

# message box is one of the module in the tkinter library
from tkinter import messagebox

# This created a new tkinter window
app=Tk()

# This gonna be title of our application
app.title("Message encryptor")

# This is  measurements are the geomentric lenth of our application
app.geometry("428x500")

# This function used to encrypt our given message 
def encrypt():
    global change

    # This line of code delete the line of message , if there is any message in the decrypt box
    decryptorEntry.delete("1.0","end")

    # This is input of a string in the encrypt message
    s=str(encryptorEntry.get(1.0,"end-1c"))

    # This "out" variable  stores final message 
    out=("")

    # This alpha list contains 26 alphabets and a white space 
    alpha=[" ","a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"]
    
    #This try except is used to hadle a error raise by the user
    try:
        if s=="":
            raise IOError

        # In this for loop the input strin is taken to process the message
        for x in s:
            # this "num" variable helps us to find the number of the alphabet in the alphabet row 
            num=alpha.index(x)

            """if  number of the variable is less than 24 the mess variable stores the value of (position of alphabet in the alphabet row + 2). Example: the "b" has a index of 3 in the alpha list the mess stores (3+2 = 5) "out" Variable stores the aphabet which has the index of "5" in the alpha list """
            if num <=24:
                mess=num+2
            elif num>24:
                mess=len(alpha)-(num+1)
            out+=alpha[mess]

        #  This line of code is used to label the message "Here your Decrypted message"
        decryptorLable.config(text="Here your Decrypted message:")

        #  This inserted the string value stored in "out" Variable to decryptor message box
        decryptorEntry.insert(2.0,out)

        # These except are used to handel the error raise by the user
    except ValueError:
        # if the user raise the value error the message box with the text given text 
        messagebox.showinfo("Sorry for this","Don't use Capital letters,Numbers,Punctuations and Brackets")
    except IOError:
        messagebox.showwarning("Warning","Enter a valid message")
def decrypt():
    global change
    decryptorEntry.delete("1.0","end")
    s=str(encryptorEntry.get(1.0,"end-1c"))
    out=("")
    alpha=[" ","a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"]
    try:
        if s=="":
            raise IOError

        for x in s:
            num=alpha.index(x)
            if num>1:
                mess=num-2
            elif num<=1:
                mess=len(alpha)-(num+1)
            out+=alpha[mess]
        decryptorLable.config(text="Here your Encrypted message:")
        decryptorEntry.insert(2.0,out)
    except ValueError:
        messagebox.showinfo("Sorry for this","Don't use Capital letters,Numbers,Punctuations and Brackets")
    except IOError:
        messagebox.showwarning("Warning","Enter a valid message")
encryptorLable=Label(app,text="Enter the message:")
encryptorLable.place(x=10,y=10)
 

encryptorEntry=Text(app,height=10,width=50)
encryptorEntry.place(x=10,y=30)

#  these button key is used to creat a buttons in the application 
encryptorButton=Button(app,text="Encrypt",width=47,command=encrypt)
encryptorButton.place(x=10,y=210)
decryptorButton=Button(app,text="Decrypt",width=47,command=decrypt)
decryptorButton.place(x=10,y=250)

decryptorLable=Label(app,text="Here your message:")
decryptorLable.place(x=10,y=290)

decryptorEntry=Text(app,height=10,width=50)
decryptorEntry.place(x=10,y=310)
messagebox.showinfo("Sorry for this","Don't use Capital letters,Numbers,Punctuations and Brackets")
app.mainloop()
