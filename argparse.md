# argparse

Cheatsheet for pyhon `argparse` module.

**Boolean flags**

```python
parser.add_argument('--feature', dest='feature', action='store_true')
parser.add_argument('--no-feature', dest='feature', action='store_false')
parser.set_defaults(feature=True)
```

Usage:
```
python myscirpt.py --feature

python myscript.py --no-feature
```

**Boolean flag (option 2)**

```python
import argparse                                                          
                                                                         
parser = argparse.ArgumentParser()                                       
parser.add_argument("--all-branches", action="store_true", default=False)
args = parser.parse_args()                                               
                                                                         
print(args)                                                              
```

**List of integer values**

```
parser = argparse.ArgumentParser()
parser.add_argument('--indices', nargs='+', type=int)

args = parser.parse_args()
indices = args.indices
```

Usage:

```bash
python myscript.py --indices 1 2 3
```
