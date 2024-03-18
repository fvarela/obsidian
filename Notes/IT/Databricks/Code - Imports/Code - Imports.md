You can only use the python import command with .py files, not notebooks.
You can only use the python import command with .py files when using repos

Make sure you have enabled 'Files in Repos' in your 'Admin Console'

* From a sibling folder:
For appending a file from a sibling `modules` folder:

```python
import sys
import os
sys.path.append(os.path.abspath('../modules'))
```


* Import a wheel
Use the pip install command:
```
%pip install ../wheels/shapes-1.0.0-py3-none-any.whl
```
Then you can use normally:
```python
from shapes_wheel.cube import Bube as Cube_WHL
```