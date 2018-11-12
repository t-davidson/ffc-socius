# Black Box Models and Sociological Explanations: Predicting High School GPA Using Neural Networks

## Introduction

This repository contains code to replicate the analysis for the [Fragile Families Challenge](http://www.fragilefamilieschallenge.org) as described in the paper submitted to Socius. A pre-print is available [here](https://osf.io/preprints/socarxiv/7nsrf/).

This code is an updated version of the code used in the challenge. The original repository, which contains the code used in the paper, along with the exact results (viewable by opening the Jupyter notebook files), can be viewed [here](https://github.com/t-davidson/fragile-families-challenge).

In this updated version there are three main changes: (1) The files have been organized more coherently and instructions have been provided to set up an environment to replicate the results entirely, (2) seeds have been added throughout the code to help to ensure reproducibility, (3) the code has been updated to ensure compatibility with the new Fragile Families Metadata API.

Despite attempts to make the results exactly reproducible the neural network models trained in `gpa.ipynb` still produce variable results over multiple runs and across multiple machines. This repository therefore provides code that allows others to replicate my analyses, but unfortunately falls short of allowing the exact results reported in the paper to be completely reproducible. If anyone has feedback on how the code can be improved to ensure this then please get in touch.

## Set-up instructions

Please follow these instructions to reproduce the results:

First set up a Python virtual environment and install the require packages by entering the following commands into Terminal. ***Note this assumes that Python 3.6 and the pip package manager are pre installed***):
```
pip install virtualenv
python -m virtualenv ffc-env
source ffc-env/bin/activate
pip install -r requirements.txt
```

Next run this command to create additional empty directories to store the results:
```
mkdir data && mkdir data/logs && mkdir output && mkdir output/logs && mkdir output/models
```

The raw FFC data must be stored in a directory called `FFChallenge_v2` in the same directory as this repository (e.g. there should be a directory that contains `ffc-socius` and `FFChallenge_v2`).

## Replicating the code

Running the following files in order will reproduce the main results. Since a number of the files take a considerable amount of time to run and involve multiple stages I recommend running each in turn:

### Cleaning the FFC data
First, navigate to `code/preprocess` and run `clean_files.py`. This script will take the raw FFC files and produce a CSV containing a cleaned and imputed version of the files.


### Training the neural network models
Next, start a new jupyter notebook server from the base directory by running the command `jupyter notebook`.

Using the Juypter GUI navigate to the `code` directory and the `model` and enter the `gpa.ipynb` file. Running every cell in this file will reproduce the main results of the paper. ***This file will take approximately 12 hours to complete running on a modern laptop computer.***

The `regression_baseline.ipynb` notebook can be run to obtain a baseline from an OLS regression.

### Running and assessing the LIME explanations
Once this notebook has completed, running `LIME_explanations.ipynb` in the `code/lime` directory will use LIME to produce explanations for the best model from `gpa.ipynb`. ***This file will take approximately 12 hours to complete running on a modern laptop computer.*** The best model used in the paper is defined as the best performing model on the FFC leaderboard dataset. The predictions from the top 5 models (stored in the `output` directory) must be used to identify the best model. The model must then be manually declared in the LIME notebook.

### Figures and supplementary analyses
The figures shown in the paper are output into the `figures` directory. This also contains Figure 1, which was created using [Draw.io](https://www.draw.io/), a free online tool to draw diagrams.

Once `gpa.ipynb` has finished running the notebooks in `code/supplementary` can then be run to produce the results reported in the Supplementary Information.
