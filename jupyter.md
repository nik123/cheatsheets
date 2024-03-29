# Jupyter Notebook

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
%matplotlib inline
pylab.rcParams['figure.figsize'] = (16, 9)
```

Interactive matplotlib in Jupyterlab:
```
%matplotlib ipympl
import matplotlib.pyplot as plt
...
plt.figure()
plt.imshow(im)
```

Запуск на указанном порту и сетевом интерфейсе:
```
$jupyter notebook --no-browser --port 9999 --ip <ip-address>
```

Suppress cell output:
```
%%capture 
```

# Kernels

Add kernel from another environemnt (i.e. not the environment where jupyter server itself is installed):
```
# Assuming conda environment

# Activate environment:
conda activate <my-environment>

# Install ipykernel
pip install ipykernel

# Add kernel to Jupyter
# --user for userwide installation, command may attempt to install flag
# systemwide without this flag.
python -m ipykernel install --user --name py39-test
```

Uninstall kernel:
```
# Assuming conda environment
# Activate environement with jupyterlab
# NOT the one with kernel itself!
conda activate <jupyterlab-env>

# Remove kernel:
jupyter kernelspec uninstall unwanted-kernel
```
