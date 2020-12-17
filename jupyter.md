# Jupyter notebook

Ignore system locale:

```
$ LANGUAGE="" LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 jupyter notebook
```

Размер matplotlib-графика в Jupyter:

```
# Jupyter Notebook:
%matplotlib inline
import matplotlib.pyplot as plt
plt.rcParams['figure.figsize'] = (16, 9) 

# Jupyter lab:
%pylab inline
pylab.rcParams['figure.figsize'] = (16, 9)
```

Запуск на указанном порту и сетевом интерфейсе:
```
$jupyter notebook --no-browser --port 9999 --ip <ip-address>
```

Suppress cell output:
```
%%capture 
```
