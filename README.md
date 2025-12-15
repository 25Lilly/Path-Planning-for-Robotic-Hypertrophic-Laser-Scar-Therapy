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
Download the .ipynb file, segmenetation folder, and images folder.   
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


# Future Improvements to Be Made
For information on limitations and future work, check out final_report.pdf

Contact Us:  
lhc24@duke.edu  
kmp101@duke.edu

