# Introduction ML Safety Exercise 3 and 4

This repository contains the code and results for the Introduction to Machine Learning Safety exercises.

# Contents

- Exercise 3.4: Dataset exploration
- Exercise 3.5: Training three binary classifiers
- Exercise 3.6: Evaluation on the test split
- Exercise 4.5: ODD coverage using k-projection coverage

# Dataset

The CARLA dataset is not committed to GitHub because of file size.  
The dataset zip files should be placed under OvGU cloud: https://cloud.ovgu.de/s/fYD35gBQA7Ykqom

# Required Files for these exercises:
train.zip
validation.zip
test.zip

# Models
the trained model files are stored locally under: /models

# Results
pedestrian_loss_curve.png
traffic_light_loss_curve.png
vehicle_loss_curve.png
exercise_3_6_evaluation_results.csv OR exercise_3_6_1_evaluation_results.csv
exercise_4_5_k_projection_coverage.csv

# External implementation for Exercise 4.5
For k-projection coverage, the implementation from the following repository was used: 
https://github.com/kkirchheim/odd-coverage

It can be downloaded with:
git clone https://github.com/kkirchheim/odd-coverage.git

# Python Setup
python3 -m venv .venv
source .venv/bin/activate
Install required packages using following command:
pip install torch torchvision pandas matplotlib pillow scikit-learn tqdm

# Notes
The repository commits only code, notebooks, and result files.
Datasets, virtual environment files, and trained model files are excluded using .gitignore.

