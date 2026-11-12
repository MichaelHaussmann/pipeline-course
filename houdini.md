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

### Events

* 456.py
* oncreated.py
  

# Code snippets

```python

global_scale = 'GLOBAL_SCALE'
try:

      folder = hou.FolderParmTemplate('folder', 'Pipeline')
      parm = hou.FloatParmTemplate(global_scale, global_scale, 1)
      parm.setDefaultValue((cache_scale, 0))
      parm.setMaxValue(2)
      folder.addParmTemplate(parm)

      group = in_node.parmTemplateGroup()
      group.append(folder)

      in_node.setParmTemplateGroup(group)

  except hou.OperationFailed:

      log.warn('[init_IN] Attribute {} was not created.'.format(global_scale))

```
