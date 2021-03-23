# R.P.2._Ramos-Hdz-Victor-manuel
ejemplos de clase

#ejemplo 1
import wx

app = wx.App(clearSigInt=True) # clearSigInt to allow terminating the program by CTRL+C
frame = wx.Frame(parent=None, title="") ## main window object
panel = wx.Panel(parent=frame)
text = wx.StaticText(parent=panel, label="Hello, from wxPython!!", pos = (40,50))
frame.Show()
app.MainLoop()
![image](https://user-images.githubusercontent.com/79875910/112211442-83cbb500-8be1-11eb-9b0e-33cdc18530a5.png)




#ejemplo 2
import wx
import webbrowser

class MyApp(wx.App):
    def __init__(self):
        super().__init__(clearSigInt=True)
        
        # init frame
        self.InitFrame()
    
    def InitFrame(self):
        frame = MyFrame(parent=None, title="Basic Frame", pos=(100, 100))
        frame.Show(True)


class MyFrame(wx.Frame):
    # subclass of wx.Window; Frame is a top level window
    # A frame is a window whose size and position can (usually) be changed by the user.
    # Usually represents the first/main window a user will see
    def __init__(self, parent, title, pos=pos):
        super().__init__(parent=parent, title=title, pos=pos)
    
    def OnInit(self):
        panel = MyPanel(parent=self)
![image](https://user-images.githubusercontent.com/79875910/112211554-a78efb00-8be1-11eb-87fa-6ed6406e74dc.png)








#ejemplo 3
import wx
import webbrowser

class MyApp(wx.App):
    def __init__(self):
        super().__init__(clearSigInt=True)
        
        # init frame
        self.InitFrame()
    
    def InitFrame(self):
        frame = MyFrame(parent=None, title="my button app", pos = (100, 100))
        frame.Show()


class MyFrame(wx.Frame):
    # subclass of wx.Window; Frame is a top level window
    # A frame is a window whose size and position can (usually) be changed by the user.
    # Usually represents the first/main window a user will see
    def __init__(self, parent, title, pos):
        super().__init__(parent=parent, title=title, pos=pos)
        self.OnInit()
    
    def OnInit(self):
        panel = MyPanel(parent=self)


class MyPanel(wx.Panel):
    # A panel is a window on which controls are placed. (e.g. buttons and text boxes)
    # wx.Panel class is usually put inside a wxFrame object. This class is also inherited from wxWindow class.
    def __init__(self,parent):
        super().__init__(parent=parent)
        
        # add a hello message to the panel
        welcomeText = wx.StaticText(self, label="To learn wxPython, click the link below!", pos=(20,20))

        # add a button to bring up the dialog box
        button = wx.Button(parent=self, label='Click Here!', pos = (20, 120))
        button.Bind(wx.EVT_BUTTON, self.onSubmit) # bind action to button


    def onSubmit(self, event):
        # stuff for the submit button to do
        webbrowser.open('https://wxpython.org/Phoenix/docs/html/index.html')
        
if __name__ == "__main__":
    app = MyApp()
    app.MainLoop()
![image](https://user-images.githubusercontent.com/79875910/112211700-c8efe700-8be1-11eb-859c-f5bca68428bd.png)
![image](https://user-images.githubusercontent.com/79875910/112211788-d5743f80-8be1-11eb-9c0b-5adc84f3222e.png)







#ejemplo 4
import wx


class MyApp(wx.App):
    def __init__(self):
        super().__init__()

    def OnInit(self):
        frame = MyFrame(parent=None, title="This is a frame")
        frame.Show()
        return True


class MyFrame(wx.Frame):
    # subclass of wx.Window; Frame is a top level window
    # A frame is a window whose size and position can (usually) be changed by the user.
    # Usually represents the first/main window a user will see
    def __init__(self, parent, title):
        super().__init__(parent=parent, title=title, pos = (100, 100))

        self.OnInit()

    def OnInit(self):
        panel = MyPanel(self)


class MyPanel(wx.Panel):
    # A panel is a window on which controls are placed. (e.g. buttons and text boxes)
    # wx.Panel class is usually put inside a wxFrame object. This class is also inherited from wxWindow class.
    def __init__(self,parent):
        super().__init__(parent=parent)
        self._dont_show = False # for message dialog box
        
        # add a hello message to the panel
        welcomeText = wx.StaticText(self, label="Hello World!", pos=(20,20))

        # add a text box
        self._text = wx.TextCtrl(parent= self, value = 'ENTER SOME TEXT HERE', pos = (20,60), size=(300, 50))

        # add a button to bring up the dialog box
        self._buton = wx.Button(parent=self, label='Submit', pos = (20, 120))
        self._buton.Bind(wx.EVT_BUTTON, self.onSubmit) # bind action to button


    def ShowDialog(self):
        # pop up a message dialog window on submit!
        if self._dont_show:
            return None

        dlg = wx.RichMessageDialog(parent=None, 
                message= "Are you ready to learn wxPython?",
                caption="wxPythonStuff",
                style=wx.YES_NO|wx.CANCEL|wx.CENTRE)
        dlg.ShowCheckBox("Don't show this again")
        dlg.ShowModal() # shows the dialog

        if dlg.IsCheckBoxChecked():
            print("Is check box checked?", dlg.IsCheckBoxChecked())
            self._dont_show=True
    

    def onSubmit(self, event):
        # stuff for the submit button to do
        print(self._text.GetValue())
        self.ShowDialog()
        
if __name__ == "__main__":

    app = MyApp()
    frame = MyFrame(parent=None, title="This is a frame")
    app.MainLoop()
    ![image](https://user-images.githubusercontent.com/79875910/112211896-fa68b280-8be1-11eb-87d6-145901921620.png)
    ![image](https://user-images.githubusercontent.com/79875910/112211958-0bb1bf00-8be2-11eb-89d0-59889bd48f91.png)
    ![image](https://user-images.githubusercontent.com/79875910/112212003-153b2700-8be2-11eb-9d9f-68009c0f3f3c.png)









#ejemplo 5
import wx


class MyApp(wx.App):
    def __init__(self):
        super().__init__(clearSigInt=True)
        
        # init frame
        self.InitFrame()
    
    def InitFrame(self):
        frame = MyFrame()
        frame.Show()


class MyFrame(wx.Frame):
    def __init__(self, title="MyButtonApp", pos=(100,100)):
        super().__init__(None, title=title, pos=pos)
        # initialize the frame's contents
        self.OnInit()

    def OnInit(self):
        self.panel = mi_panel(self)
        self.Fit()

class mi_panel(wx.Panel):

    def __init__(self, parent):
        super().__init__(parent=parent)

        # Add a panel so it looks correct on all platforms

        # art provider provides basic art https://wxpython.org/Phoenix/docs/html/wx.ArtProvider.html
        bmp = wx.ArtProvider.GetBitmap(id=wx.ART_INFORMATION, 
        client=wx.ART_OTHER, size=(16, 16))
        titleIco = wx.StaticBitmap(self, wx.ID_ANY, bmp)
        title = wx.StaticText(self, wx.ID_ANY, 'My Title')

        inputOneIco = wx.StaticBitmap(self, wx.ID_ANY, bmp)
        labelOne = wx.StaticText(self, wx.ID_ANY, 'Input 1')
        self.inputTxtOne = wx.TextCtrl(self, wx.ID_ANY, value='Text box')

        inputTwoIco = wx.StaticBitmap(self, wx.ID_ANY, bmp)
        labelTwo = wx.StaticText(self, wx.ID_ANY, 'Input 2')
        # wx.SpinCtrl combines wx.TextCtrl and wx.SpinButton in one control.
        self.inputTwo = wx.SpinCtrl(self, wx.ID_ANY, value="0", min=0, max=100)

        inputThreeIco = wx.StaticBitmap(self, wx.ID_ANY, bmp)
        labelThree = wx.StaticText(self, wx.ID_ANY, 'Input 3')
        self.inputThree = wx.Choice(self, choices=['A', 'B', 'C'])
        

        inputFourIco = wx.StaticBitmap(self, wx.ID_ANY, bmp)
        labelFour = wx.StaticText(self, wx.ID_ANY, 'Input 4')
        self.inputFour1 = wx.CheckBox(parent=self, label="Choice 1")
        self.inputFour2 = wx.CheckBox(parent=self, label="Choice 2")
        self.inputFour3 = wx.CheckBox(parent=self, label="Choice 3")

        okBtn = wx.Button(self, wx.ID_ANY, 'OK')
        cancelBtn = wx.Button(self, wx.ID_ANY, 'Cancel')
        self.Bind(wx.EVT_BUTTON, self.onOK, okBtn)
        self.Bind(wx.EVT_BUTTON, self.onCancel, cancelBtn)

        mainSizer = wx.BoxSizer(wx.VERTICAL)
        titleSizer = wx.BoxSizer(wx.HORIZONTAL)
        inputOneSizer = wx.BoxSizer(wx.HORIZONTAL)
        inputTwoSizer = wx.BoxSizer(wx.HORIZONTAL)
        inputThreeSizer = wx.BoxSizer(wx.HORIZONTAL)
        inputFourSizer = wx.BoxSizer(wx.HORIZONTAL)
        submitBtnSizer = wx.BoxSizer(wx.HORIZONTAL)

        titleSizer.Add(titleIco, 0, wx.ALL, 5)
        titleSizer.Add(title, 0, wx.ALL, 5)

        inputOneSizer.Add(inputOneIco, 0, wx.ALL, 5)
        inputOneSizer.Add(labelOne, 0, wx.ALL, 5)

        inputOneSizer.Add(self.inputTxtOne, 1, wx.ALL|wx.EXPAND, 5)

        inputTwoSizer.Add(inputTwoIco, 0, wx.ALL, 5)
        inputTwoSizer.Add(labelTwo, 0, wx.ALL, 5)
        inputTwoSizer.Add(self.inputTwo, 1, wx.ALL|wx.EXPAND, 5)

        inputThreeSizer.Add(inputThreeIco, 0, wx.ALL, 5)
        inputThreeSizer.Add(labelThree, 0, wx.ALL, 5)
        inputThreeSizer.Add(self.inputThree, 1, wx.ALL|wx.EXPAND, 5)

        inputFourSizer.Add(inputFourIco, 0, wx.ALL, 5)
        inputFourSizer.Add(labelFour, 0, wx.ALL, 5)
        inputFourSizer.Add(self.inputFour1, 1, wx.ALL|wx.EXPAND, 5)
        inputFourSizer.Add(self.inputFour2, 1, wx.ALL|wx.EXPAND, 5)
        inputFourSizer.Add(self.inputFour3, 1, wx.ALL|wx.EXPAND, 5)

        submitBtnSizer.Add(okBtn, 0, wx.ALL, 5)
        submitBtnSizer.Add(cancelBtn, 0, wx.ALL, 5)

        mainSizer.Add(titleSizer, 0, wx.CENTER)
        mainSizer.Add(wx.StaticLine(self,), 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(inputOneSizer, 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(inputTwoSizer, 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(inputThreeSizer, 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(inputFourSizer, 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(wx.StaticLine(self), 0, wx.ALL|wx.EXPAND, 5)
        mainSizer.Add(submitBtnSizer, 0, wx.ALL|wx.CENTER, 5)

        self.SetSizer(mainSizer)
        mainSizer.Fit(self)
        self.Layout()


    def onOK(self, event):
        # Do something
        print('onOK handler')
        data = self.getData()
        print(data)

    def onCancel(self, event):
        self.closeProgram()

    def closeProgram(self):
        # self.GetParent() will get the frame which
        # has the .Close() method to close the program
        self.GetParent().Close()

    def getData(self):
        '''
        this here will procure data from all buttons
        '''
        data = []
        data.append(self.inputTxtOne.GetValue())
        data.append(self.inputTwo.GetValue())
        selection = self.inputThree.GetSelection()
        data.append((selection, 
                    self.inputThree.GetString(selection))
                    )
        data.append(self.inputFour1.GetValue())
        data.append(self.inputFour2.GetValue())
        data.append(self.inputFour3.GetValue())
        return data

# Run the program
if __name__ == '__main__':
    app = MyApp()
    app.MainLoop()
![image](https://user-images.githubusercontent.com/79875910/112212127-3734a980-8be2-11eb-9902-357bc57e08b2.png)

![image](https://user-images.githubusercontent.com/79875910/112212154-4156a800-8be2-11eb-86d8-c7decec95cf0.png)
![image](https://user-images.githubusercontent.com/79875910/112212195-4ddb0080-8be2-11eb-9913-13082d1ec0c6.png)

![image](https://user-images.githubusercontent.com/79875910/112212188-4b78a680-8be2-11eb-8654-33c5127a7d85.png)
![image](https://user-images.githubusercontent.com/79875910/112212237-592e2c00-8be2-11eb-892d-f7790f21ae39.png)
![image](https://user-images.githubusercontent.com/79875910/112212274-62b79400-8be2-11eb-95c2-05e5b802fd83.png)


