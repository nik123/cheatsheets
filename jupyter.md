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

Запуск на указанном порту и сетевом интерфейсе:
```
$jupyter notebook --no-browser --port 9999 --ip <ip-address>
```

Suppress cell output:
```
%%capture 
```

# Jupyter Notebook Extensions

[Jupyter notebook extensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions) - extensions that add functionality to the Jupyter notebook.

Installation:

```
# Step 1: install package
# pip
pip install jupyter_contrib_nbextensions
# conda
conda install -c conda-forge jupyter_contrib_nbextensions

# Step 2: install javascript and css files:
jupyter contrib nbextension install --user
```

Useful extensions (for me):
1. [Jupyter Black](https://github.com/drillan/jupyter-black)
1. toc2 (table of contents).

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
python -m ipykernel install --user --name py36-test
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
