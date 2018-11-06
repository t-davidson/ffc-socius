Please follow these instructions to reproduce the results:

First set up a Python virtualenv and install the require packages (***Note this assumes that Python 3.6 and the pip package manager are pre installed***):
```
pip install virtualenv
python -m virtualenv ffc-env
source ./ffc-env/bin/activate
pip install -r requirements.txt
mkdir data && mkdir data/logs
```

Running the following files in order will reproduce the results. Since a number of the files take a considerable amount of time to run and involve multiple stages I recommend running each in turn:

First, start a new jupyter notebook server from the base directory by running the command `jupyter notebook`.

Using the Juypter GUI navigate to the `code` directory and the `model` and enter the `gpa.ipynb` file. Running every cell in this file will reproduce the main results of the paper.

Once this notebook has completed, running `LIME_explanations.ipynb` in the `code/lime` directory will use LIME to produce explanations for the best model from `gpa.ipynb`. ***The best model is defined as the best performing model on the FFC leaderboard dataset. The predictions from the top 5 models (stored in the `output` directory) must be used to identify the best model.***
