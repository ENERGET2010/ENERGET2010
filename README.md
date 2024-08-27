from tkinter import *
import threading
import time

class Game:
    def __init__(self):
        self.w = Tk()
        self.timesup = 1
        self.csec = 0
        self.timeprice = self.timesup*100
        self.updates = 1
        self.upd = self.updates*15
        self.click = 0
        self.addc = 1
        self.w.geometry('200x200')
        self.w.config(bg = 'black')
        self.w.resizable(False, False)
        self.image = PhotoImage(file = 'monetkf.png')
        self.file = PhotoImage(file = 'Shop.png')
        self.mon = Button(self.w, image = self.image, command = self.addclick)
        self.shop = Button(self.w, image = self.file, command = self.Shop)
        self.clicks = Label(self.w, text = self.click, font = 'Times 20')
        self.mon.pack(anchor = CENTER)
        self.clicks.pack(side = TOP)
        self.shop.pack(side = BOTTOM)
        self.clickontime = threading.Thread(target = self.timer)
        self.clickontime.daemon = True
        self.clickontime.start()
        
        
        self.w.mainloop()
        
    def addclick(self):
        self.click += self.addc
        self.clicks.config(text = self.click)
        
    def Shop(self):
        self.sh = Tk()
        self.sh.title('shop')
        self.sh.geometry('200x200')
        self.w.withdraw()
        self.sh.deiconify()
        self.aclick = Button(self.sh, text = f'+1 click -{self.upd}', command = self.plusc )
        self.timeclick = Button(self.sh, text = f'+1 click in sec -{self.timeprice}', command = self.tim)
        self.aclick.pack()
        self.timeclick.pack()
        
        self.back = Button(self.sh, text='<--- Back', command = self.backs)
        self.back.pack(anchor = NW)
      
      
    def plusc(self):
        if self.click >= self.upd:
            self.click -= self.upd
            self.addc += 1
            self.clicks.config(text = self.click)
            self.updates += 1
            self.upd = self.updates*15
        else:
            self.nomoney = Label(self.sh, text='You havent got a money')
            self.nomoney.pack()
        self.aclick.config(text = f'+1 click -{self.upd}')
    
    def tim(self):
        if self.click >= self.timeprice:
            self.click -= self.timeprice
            self.timesup += 1
            self.timeprice = self.timesup*100
            self.csec += 1
        else:
            self.nomoney = Label(self.sh, text='You havent got a money')
            self.nomoney.pack()
        self.timeclick.config(text = f'+1 click in sec -{self.timeprice}')
            
    
    def timer(self):
        while 1:
            self.click += self.csec
            self.clicks.config(text = self.click)
            time.sleep(1)
    
    
    
    def backs(self):
        self.sh.withdraw()
        self.w.update()
        self.w.deiconify()
                           

        


g = Game()       ![Shop](https://github.com/user-attachments/assets/bb52a7bd-f6ca-4dbc-8fce-bc1416e31084)
![monetkf](https://github.com/user-attachments/assets/862b8375-6553-4090-be69-eca74c9a210d)

