# DVC

Generate pipeline image:

```bash
dvc dag --dot mystage > mystage.dot
dot -Tpng mystage.dot -o mystage.png
```
