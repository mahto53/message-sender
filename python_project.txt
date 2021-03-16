import json
import requests  #allows you to use fast2sms server
from tkinter import  *  # allow you to crearte gui applications  ..it has most commonly used gui elements
from tkinter.messagebox import showinfo,showerror

def send_sms(number,message):
    url='https://www.fast2sms.com/dev/bulk' # this is url of fast2sms through which we r  sending msgs
    params={
        'authorization':'VC9liNv4TmGRpjfHsraFSx8eJqUBkIyobh62ZtE0ADYuLXPKWzdqPm02WSk841KJIDBwUCnjrxyhQRHg',
        'sender_id':'FSTSMS','message':message,
        'language':'english',
        'route':'p',
        'numbers':number

    }
    response=requests.get(url,params=params)#it will give you response from fast2sms server
    dic=response.json()# json is used here to convert string message to python dictionary
    print(dic)
    return dic.get('return')
def btn_click():
    num=textNumber.get()
    msg=textMessage.get("1.0",END)
    r=send_sms(num,msg)
    if r:
        showinfo("Send Success","Successfully Sent")
    else:
        showerror("Error","Something went wrong....")


#creating GUI
root=Tk() # Tk class is used to create root window or main window of application
root.title("Message Sender")#set thr title to root window
root.geometry("400x550")#size of main window
font=("Calibri",22,"bold")#font of no
textNumber=Entry(root,font=font)# entry creates a single line entry in window
textNumber.pack(fill=X,pady=20)
textMessage=Text(root)#Text is used to create multiple lines in main wiondow application
textMessage.pack(fill=X)
sendBtn=Button(root,text="SEND SMS",command=btn_click)#button is used to call funcn btn_click as we ll get to know that either message sent successfully or not
sendBtn.pack()


root.mainloop()#used to keep looping main window it runs gui
