### Documentation

* [https://www.sidefx.com/docs/houdini/hom/](https://www.sidefx.com/docs/houdini/hom/) - python in Houdini 
* [https://www.sidefx.com/docs/houdini/hom/hou](https://www.sidefx.com/docs/houdini/hom/hou/) - hou package reference

### Classes and objects

* classes are uppercase : `hou.Node()`
  * constructor function is class name: `hou.StringParmTemplate()`
    
* functions are lowercase
  * general functions: `hou.node()`
  * object functions : `node.setColor()`

### Python in Houdini

* python shell
* python sop node

### Practice

* create a Node
* set a color
* connect nodes
* create a test crag sop node
* create a rop alembic

Create a "Piped" rop alembic
* on the rop alembic, in python
* create a string parameter called "asset" (label: "Asset")
* create an integer parameter called "version"
* update the "filename" parameter so it saves "$HIP/<asset>_v<001>.abc"

### Events

* 456.py
* oncreated.py
  

# Code snippets

- Add a parameter
```python
box = hou.node('/obj/coding/box1')
parm = hou.StringParmTemplate("example", "My Example Parm", 1, default_value=("default",))
group = box.parmTemplateGroup() 
group.append(parm) 
box.setParmTemplateGroup(group) 
```

- UI with qtpy
  
```python

import qtpy
from qtpy import QtCore, QtWidgets, QtGui

ui_path = os.path.join(os.path.dirname(__file__), "qt/browser.ui")

class Browser(QtWidgets.QMainWindow):

    # cb = QtWidgets.QApplication.clipboard()  # exemple de clipboard

    def __init__(self):
        super(Browser, self).__init__()

        # For some ominous reason, this does not work:
        # qtpy.uic.loadUi(ui_path, self)
        from qtpy.uic import loadUi
        loadUi(ui_path, self)
        self.setWindowTitle(f"{browser_title} - Browser")

        # les objets du ui sont accessibles via self
        self.publish_cb.setText('publish')
        self.work_cb.setText('work')


if __name__ == "__main__":
    myApp = QtWidgets.QApplication(sys.argv)
    myWindow = Window()
    myWindow.show()

    sys.exit(myApp.exec())
```

