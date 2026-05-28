# Introduction ML Safety Exercises

This repository contains the code and results for the Introduction to Machine Learning Safety exercises.

# Contents

- Exercise 3.4: Dataset exploration
- Exercise 3.5: Training three binary classifiers
- Exercise 3.6: Evaluation on the test split
- Exercise 4.5: ODD coverage using k-projection coverage
- Exercise 5.1, 5.2, 5.3: Testing LLMs & Agents
- Exercise 5.4: Temperature Scaling and the Confidence Threshold
- Exercise 5.5: Backdoor Attack on the Pedestrian Detector

# Dataset

The CARLA dataset is not committed to GitHub because of file size.  
The dataset zip files should be placed under OvGU cloud: https://cloud.ovgu.de/s/fYD35gBQA7Ykqom

# Required Files for these exercises:
train.zip
validation.zip
test.zip

# Models
the trained model files are stored locally under: /models
local models generated:
models/has_pedestrian_resnet18.pt
models/has_traffic_light_resnet18.pt
models/has_vehicle_resnet18.pt
models/has_pedestrian_backdoored_resnet18.pt

# Notebooks 
notebooks/3.4_dataset_exploration.ipynb
notebooks/3.5_train_binary_classifiers.ipynb
notebooks/3.6_evaluation.ipynb
notebooks/4.5_odd_coverage.ipynb
notebooks/Exercise 5_Testing LLMs & Agents.md
notebooks/5.4_temperature_scaling.ipynb
notebooks/5.5_backdoor_attack.ipynb


# Results
pedestrian_loss_curve.png
traffic_light_loss_curve.png
vehicle_loss_curve.png
exercise_3_6_evaluation_results.csv
exercise_3_6_1_evaluation_results.csv
exercise_4_5_k_projection_coverage.csv
exercise_5_4_1_temperature_scaling_accuracy.csv
exercise_5_4_2_pT_distribution_T_0.5.png
exercise_5_4_2_pT_distribution_T_1.0.png
exercise_5_4_2_pT_distribution_T_2.0.png
exercise_5_5_backdoored_training_loss.png
exercise_5_5_backdoor_evaluation.csv

# External implementation for Exercise 4.5
For k-projection coverage, the implementation from the following repository was used: 
https://github.com/kkirchheim/odd-coverage

It can be downloaded with:
git clone https://github.com/kkirchheim/odd-coverage.git

# Exercise 5.4: Temperature Scaling

Temperature scaling was applied to the pedestrian detector using: T = 0.5, 1.0, 2.0
The model probabilities were computed as: pT = sigmoid(z / T)
Accuracy was evaluated using a fixed decision threshold of 0.5.
The probability distributions for each temperature were plotted and saved in the results/ folder.
The confidence threshold analysis used: θ = 0.6

The speed-reduction rule was:
If model confidence is below θ, reduce speed to ≤ 15 km/h.

# Exercise 5.5: Backdoor Attack

A backdoor attack was implemented on the pedestrian detector.
A red trigger square was added to selected images:

Trigger size: 10 × 10 pixels
Trigger colour: (255, 0, 0)
Trigger position: bottom-right corner

For 10% of training images where: has_pedestrian = True
the trigger was applied and the label was flipped to: has_pedestrian = False
The pedestrian detector was retrained on the poisoned training set.

# Backdoor Evaluation Results

Clean recall on the original test set: 0.3966

Attack Success Rate: 1.0

Number of triggered pedestrian-positive test images: 706

The attack was successful because 100% of triggered pedestrian-positive test images were classified as “no pedestrian”.

# Python Setup
python3 -m venv .venv
source .venv/bin/activate

Install required packages using following command:
pip install torch torchvision pandas matplotlib pillow scikit-learn tqdm

# Notes
The repository commits only code, notebooks, and result files.
Datasets, virtual environment files, and trained model files are excluded using .gitignore.

