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

- create nodes and render rop
```python
geo = hou.node("/obj/geo1")

if geo:
    print("Exists already")
else:
    geo = hou.node("/obj").createNode("geo", node_name="geo1")

# print(geo)
crag = geo.createNode("testgeometry_crag")

# create then connect (longer code)
# abc = geo.createNode("rop_alembic")
# abc.setInput(0, crag)
# abc.moveToGoodPosition()  

# create connected
abc = crag.createOutputNode("rop_alembic")

# render function 
abc.render(frame_range=(1, 5))

# or push button
# abc.parm("execute").pushButton()
```

- Add parameters
```python
node = hou.node('/obj/coding/rop_alembic1')

folder = hou.FolderParmTemplate('folder', 'Pipeline')
asset_parm = hou.StringParmTemplate("asset", "Asset", 1, default_value=("",))
version_parm = hou.IntParmTemplate("version", "Version", 1, default_value=(1,))

group = node.parmTemplateGroup() 
folder.addParmTemplate(asset_parm)
folder.addParmTemplate(version_parm)  
# group.append(asset_parm) 
# group.append(version_parm)

group.append(folder)
node.setParmTemplateGroup(group)     
```

- set python expression on rop filename (using previous parameters
```python
node = hou.node('/obj/coding/rop_alembic1')

filename_parm = node.parm("filename")
print(filename_parm)   

expression = 'parm("asset").eval() + "_v" + parm("version").evalAsString()'
filename_parm.setExpression(expression, language=hou.exprLanguage.Python)     
```

- On Created
In a file in `$HOUDINI_PATH/scripts/oncreated.py`
```python
print("Node Created")

node = kwargs['node']
node_type = kwargs['type']

print(node)
print(node_type)

if node_type.name() == "box":
	node.setColor(hou.Color((0.2, 0.8, 0.2)))
	print(f'Set color of "{node.path()}"')
```


- UI with qtpy
Install PySide6, Qtpy  
Create `window.ui` file with `venv\Lib\site-packages\PySide6\designer.exe`  
```python

import qtpy
from qtpy import QtCore, QtWidgets, QtGui

ui_path = os.path.join(os.path.dirname(__file__), "qt/window.ui")

class Window(QtWidgets.QMainWindow):

    # cb = QtWidgets.QApplication.clipboard()  # exemple de clipboard

    def __init__(self):
        super(Window, self).__init__()

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

