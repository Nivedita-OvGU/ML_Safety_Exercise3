
# Introduction ML Safety Exercise

This repository contains the code and results for the Introduction to Machine Learning Safety exercises.

# Contents

- Exercise 3.4: Dataset exploration
- Exercise 3.5: Training three binary classifiers
- Exercise 3.6: Evaluation on the test split
- Exercise 4.5: ODD coverage using k-projection coverage
- Exercise 5.1, 5.2, 5.3: Testing LLMs & Agents
- Exercise 5.4: Temperature Scaling and the Confidence Threshold
- Exercise 5.5: Backdoor Attack on the Pedestrian Detector
- Exercise 6.2, 6.3, 6.4: Explainability Concepts
- Exercise 6.5: Applying Grad-CAM Explainability
- Exercise 6.6: Explainability as a Diagnostic Tool

# Dataset

The CARLA dataset is not committed to GitHub because of file size.  
The dataset zip files should be placed under OvGU cloud: https://cloud.ovgu.de/s/fYD35gBQA7Ykqom

# Required Files for these exercises:
For Exercises 3, 4, and 5:
train.zip
validation.zip
test.zip

For Exercise 6.6 condition testing:
test.zip
test-fog.zip
test-night.zip
test-town-01.zip

# Models
The trained model files are stored locally under:
models/

Local model files generated:
models/has_pedestrian_resnet18.pt
models/has_traffic_light_resnet18.pt
models/has_vehicle_resnet18.pt
models/has_pedestrian_backdoored_resnet18.pt

Model files are not committed to GitHub because they are large generated files.

# Notebooks 
notebooks/3.4_dataset_exploration.ipynb
notebooks/3.5_train_binary_classifiers.ipynb
notebooks/3.6_evaluation.ipynb
notebooks/4.5_odd_coverage.ipynb
notebooks/Exercise 5_Testing LLMs & Agents.md
notebooks/5.4_temperature_scaling.ipynb
notebooks/5.5_backdoor_attack.ipynb
notebooks/Exercise06_Explainability Concepts.md
notebooks/6.5_6.6_Explainability Method.ipynb


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
results/exercise_6_5_gradcam/
results/exercise_6_6_diagnostic/

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

Exercise 6: Explainability

Exercise 6 focused on explainability for the trained CARLA models.

The theory part covered:

Local vs global explainability
Saliency vs occlusion
Chain-of-thought fidelity

The practical part used Grad-CAM as the local explainability method.

Grad-CAM was applied to the three trained ResNet-18 binary classifiers:

pedestrian model
traffic light model
vehicle model
Exercise 6.5: Grad-CAM on Correct and Misclassified Images

Grad-CAM was applied to five correctly classified images with at least one image per model.

It was also applied to three misclassified images.

The purpose was to check whether the highlighted regions correspond to the relevant objects such as pedestrians, traffic lights, and vehicles.

The result files are stored under:

results/exercise_6_5_gradcam/

exercise_6_5_correct_classified_gradcam.png
exercise_6_5_misclassified_gradcam.png
selected_correct_examples.csv
selected_misclassified_examples.csv

Exercise 6.6: Explainability as a Diagnostic Tool

The models were tested on images from different conditions:

normal
fog
night
town_01

The same Grad-CAM method was applied to compare explanation quality across conditions.

The accuracy results showed mixed generalization:

The pedestrian model stayed around 0.80 on normal, fog, and night, and increased on town_01.
The traffic light model had low accuracy across all conditions.
The vehicle model performed well on normal and fog, but dropped on night and town_01.

The Grad-CAM explanations showed that the models sometimes focused on background regions such as road texture, sky, buildings, trees, lighting, or general scene layout. This suggests possible reliance on spurious context features.

The result files are stored under:

results/exercise_6_6_diagnostic/

exercise_6_6_accuracy_by_condition.csv
exercise_6_6_accuracy_comparison.png
exercise_6_6_gradcam_normal.png
exercise_6_6_gradcam_fog.png
exercise_6_6_gradcam_night.png
exercise_6_6_gradcam_town_01.png
exercise_6_6_selected_gradcam_examples.csv
exercise_6_6_summary_table.csv
predictions_fog_pedestrian.csv
predictions_fog_traffic_light.csv
predictions_fog_vehicle.csv
predictions_night_pedestrian.csv
predictions_night_traffic_light.csv
predictions_night_vehicle.csv
predictions_normal_pedestrian.csv
predictions_normal_traffic_light.csv
predictions_normal_vehicle.csv
predictions_town_01_pedestrian.csv
predictions_town_01_traffic_light.csv
predictions_town_01_vehicle.csv

# Python Setup
python3 -m venv .venv
source .venv/bin/activate

Install required packages using following command:
pip install torch torchvision pandas matplotlib pillow scikit-learn tqdm

# Notes
The repository commits only code, notebooks, and result files.
Datasets, virtual environment files, and trained model files are excluded using .gitignore.

