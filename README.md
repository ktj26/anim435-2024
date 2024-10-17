# anim435-2024

Assignments for Pipeline Class (Technical Directing)

## Cube or Sphere

This code is used to generate a cube or sphere using python in Maya and QT Creator.

Run the code and a UI box will appear.

Select if you want a cube or a sphere.

After your choice is selected hit the generate button.

Your selection will appear in the maya field.

'''python

from maya import cmds
from maya import OpenMayaUI as omui  
from PySide2.QtCore import *  
from PySide2.QtGui import *  
from PySide2.QtWidgets import * 
from PySide2.QtUiTools import * 
from shiboken2 import wrapInstance 

mayaMainWindowPtr = omui.MQtUtil.mainWindow() 
mayaMainWindow = wrapInstance(int(mayaMainWindowPtr), QWidget)  

class MyMayaWidget(QWidget):     

    def __init__(self, *args, **kwargs):         
        super(MyMayaWidget, self).__init__(*args, **kwargs) 

        #Parent widget under Maya main window
        self.setParent(mayaMainWindow)         
        self.setWindowFlags(Qt.Window)    

        #Set the object name      
        self.setWindowTitle('My Maya Widget')         
        self.setGeometry(50, 50, 250, 150)      # Change your window size here 
        self.initUI()   

    def initUI(self):         
        loader = QUiLoader()               
        file = QFile(r"C:\Users\kolto\OneDrive\Documents\maya\scripts\Assignment_2_form.ui") # Add your C:\ path to your .UI file 
        file.open(QFile.ReadOnly)         
        self.ui = loader.load(file, parentWidget=self)         
        file.close() 

        # Change myButton to match the name of the button
        # in Qt Creator
        self.ui.myButton.clicked.connect(self.button_onClicked) 
        
        
    def button_onClicked(self): 
        # add logic for your button press here  
        if self.ui.mySphere.isChecked():
            maya.cmds.polySphere()
             
        elif self.ui.myCube.isChecked():
            maya.cmds.polyCube()
               
my_widget = MyMayaWidget()      
my_widget.show()

'''

#testing comments