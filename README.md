# Predicting kinase resistance mutations using alchemical free energy methods

## Manifest
* `environment.yml` - conda environment file for installing prerequisites for Jupyter notebook
* `Bayesian analysis.ipynb` - Jupyter notebook with Bayesian analysis
* `results/` - experimental and computational results

## Usage

Install [miniconda](https://conda.io/miniconda.html):
```bash
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p $HOME/miniconda
export PATH=$HOME/miniconda:$PATH
```
Create a [conda environment](https://conda.io/docs/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file):
```bash
conda env create -f environment.yml
```
Activate the environment
```bash
source activate jupyter
```
Run the Jupyter notebook
```bash
jupyter notebook .
```
