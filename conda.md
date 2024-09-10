# Conda

Create conda environment with a certain python version:
```
conda create -n <name> python=3.10
```

Export conda environment to a yml file:
```
conda export | grep -v "^prefix: " > my_env.yml
```

Create conda environment from a *.yml file:
```
conda env create -f my_env.yml
```

List "revisions" of current environment:
```
conda list --revisions
```

Remove environment:
```
conda remove --name <name> --all
```
