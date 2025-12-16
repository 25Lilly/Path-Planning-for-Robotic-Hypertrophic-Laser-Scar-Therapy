# Path-Planning-for-Robotic-Hypertrophic-Laser-Scar-Therapy
This repository contains the code and images meant for training a laser agent. It was an educational tool to allow us to self-explore robot learning. 

# Features
- U-Net Segmentation
- Lumped Capacitance Heat Model
- Q-Learning Path Planning

# Language/Libraries
- Python, Jupyter Notebook
- os
- torch
- numpy
- cv2
- segementation_models_pytorch
- albumentations
- tqdm
- matplotlib
- shapely
- scipy
- imageio
- PIL
- shutil

# Instructions to Run
**Run Online (Recommended Method):** 
Open this file in Google Co-Lab: https://colab.research.google.com/drive/1zEf3eBp5WqS_NX71rrh3yA-GYFOHjtIv#scrollTo=vkLOVCatmmMY

Download both the Segmentation and Images folders.  
Start the runtime (recommendation Python3, T4 GPU).  
Import both folders into the files section of the Co-Lab runtime.   
Press Run All.

**Run Locally:**  
Download the `image_to_path_pipeline.ipynb`, segmentation folder, and images folder.   
Download all required libraries.  
Run code.  

**NOTE:** If you decide you don't want to train the segmentation model, you can utilize best_model.pth to skip this portion of our code.

# File Organization
main/  
│── Images/  
│── Segmentation/  
│── Visualizations/  
│── README.md  
│── best_model.pth  
│── image_to_path_pipeline.ipynb  
│── final_report.pdf  

# Notebook Overview: Image-to-Path Pipeline

The `image_to_path_pipeline.ipynb` notebook implements the full end-to-end pipeline, transforming a raw hypertrophic scar image into an optimized laser treatment path.

The notebook is organized into the following major stages:

## 1. Segmentation (U-Net Fine-Tuning and Inference)

* A U-Net with a ResNet34 encoder is trained or loaded to segment images into:

  * background
  * healthy skin
  * hypertrophic scar
* Data augmentation is applied using `albumentations`.
* Model performance is evaluated with Dice loss, cross-entropy loss, and pixel accuracy.
* Segmentation results are visualized with ground-truth and prediction overlays.

## 2. Segmentation Post-Processing

* The predicted scar mask is cleaned by:

  * Removing small connected components (noise)
  * Applying Gaussian blur and thresholding
* The resulting binary scar mask is used as the geometric basis for planning.

## 3. Laser Tiling and Image-to-Squares Conversion

* The scar region is tiled into fixed-size laser squares corresponding to the physical laser footprint.
* Rotation is evaluated to minimize the number of required laser placements.
* Each input image is converted into:

  * A resized image
  * A cleaned scar mask
  * A list of laser square coordinates

This stage bridges perception (segmentation) and planning.

## 4. Thermal Modeling

* A lumped capacitance heat model estimates the temperature evolution of scar tissue.
* Each laser square is subdivided into smaller temperature-tracked regions.
* Heat propagation to neighboring squares is modeled to simulate heating transfer via conduction.
* Temperature thresholds are used to detect minor and major burns.

## 5. Scar Representation

* The scar is represented as a grid of `LaserSquare` and `TempSquare` objects.
* This data structure tracks:

  * Laser hits
  * Local temperatures
  * Adjacency effects
* The structure is used by both planning algorithms.

## 6. Reinforcement Learning (Q-Learning)

* A Q-learning agent learns the order in which to laser scar squares.
* The state is defined by the number of squares already treated.
* Rewards balance:

  * Coverage completion
  * Avoiding burns
  * Spatial efficiency
* Training runs for thousands of episodes with epsilon-greedy exploration.
* Training reward curves are visualized.

## 7. Path Extraction and Visualization

* The trained Q-table is used to generate an optimal laser path.
* Paths are visualized with:

  * Labeled laser order
  * Overlaid temperature effects
  * Optional animated GIF generation

## 8. Greedy Baseline Comparison

* A greedy path-planning algorithm is implemented as a baseline.
* Reinforcement learning and greedy paths are compared using:

  * Total distance traveled
  * Number of major burns
  * Number of minor burns
* Both qualitative and quantitative results are displayed.

# Outputs

* Segmentation overlays for scar detection
* Post-processed scar masks
* Laser square tilings
* Reinforcement learning reward curves
* Optimized laser traversal paths
* Comparative metrics between RL and greedy approaches

# Future Improvements to Be Made
For information on limitations and future work, check out `Robot_Learning_Final_Report.pdf`

Contact Us:  
lhc24@duke.edu  
kmp101@duke.edu

