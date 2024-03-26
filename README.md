# quiz-game-python-project
import tkinter as tk
from tkinter import StringVar

root=tk.Tk()
root.geometry("500x500")

questions=["What is the capital of France?","What is the CEO of Tesla?","The iphone was created by which company?","How many Harry Potter books are there?"]
options=[["New York","London","Paris","Dublin"],["Jeff Bezos","Elon musk","Bill Gates","Tony Stark"],["Apple","Intel","Amazon","Microsoft"],[1,4,6,7]]

frame=tk.Frame(root,padx=10,pady=10,bg='#fff')
label=tk.Label(frame,height=5,width=28,bg="#ddd",font=('Verdana',20),wraplength=500)

v1=StringVar(frame)
v2=StringVar(frame)
v3=StringVar(frame)
v4=StringVar(frame)

option1=tk.Radiobutton(frame,bg="#fff",variable=v1,font=('Verdana',20),command=lambda:check(option1))
option2=tk.Radiobutton(frame,bg="#fff",variable=v2,font=('Verdana',20),command=lambda:check(option2))
option3=tk.Radiobutton(frame,bg="#fff",variable=v3,font=('Verdana',20),command=lambda:check(option3))
option4=tk.Radiobutton(frame,bg="#fff",variable=v4,font=('Verdana',20),command=lambda:check(option4))

next=tk.Button(frame,text="Next",bg="orange",font=('Verdana',20),command=lambda:displayNext())
frame.pack(fill="both",expand="true")
label.grid(row=0,column=0)
option1.grid(sticky='W',row=1,column=0)
option2.grid(sticky='W',row=2,column=0)
option3.grid(sticky='W',row=3,column=0)
option4.grid(sticky='W',row=4,column=0)
next.grid(row=6,column=0)
index=0
correct=0

def disable(state):
    option1['state']=state
    option2['state'] = state
    option3['state'] = state
    option4['state'] = state

def check(radio):
    global correct,index
    if radio['text']==options[index][3]:
        correct+=1
    index+=1
    disable('disable')

def displayNext():
    global index,correct
    if next['text']=='Restart the quiz':
        correct=0
        index=0
        label['bg']='grey'
        next['text']='Next'
    if index==len(options):
        label['text']=str(correct)+"/"+str(len(options))
        next['text']='Restart the Quiz'
        if correct>=len(options)/2:
            label['bg']='green'
        else:
            label['bg']='red'
    else:
        label['text']=questions[index]
        disable('normal')
        opts=options[index]
        option1['text']=opts[0]
        option2['text'] = opts[1]
        option3['text'] = opts[2]
        option4['text'] = opts[3]
        v1.set(opts[0])
        v2.set(opts[1])
        v3.set(opts[2])
        v4.set(opts[3])
        if index==len(options)-1:
            next['text']='Check the Results'

displayNext()
root.mainloop()
