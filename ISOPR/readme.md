1. Name: Industrial Scene Object Point-cloud Registration (ISOPR) dataset

2. Authors: Yusen Wan, Xu Chen

3. Introduction

   To simulate the depth camera and generate sensor-realistic point clouds for industrial scene pointcloud registration, we construct the ISOPR Dataset using NVIDIA Isaac Sim simulator, a robotics simulation platform developed on the NVIDIA Omniverse framework.

   ISOPR can be used to evaluate the point-cloud registration methods. The methods need to align the source point cloud and reference point cloud and estimate the rotation matrixes and translation vectors. Then, compared with the GT value, the performance of methods can be evaluated.

4. Data Structure

   The folder contains all data for ISOPR, structured across 5 .pkl files. Each file comprises 400 samples, totally 2000 samples. Every sample is stored as a dictionary with the following keys:
    'gt': point cloud of Ground truth CAD model in ndarray. (shape: N1×3)
    'gt_normal': Normal vectors of the ground truth point cloud in ndarray. (shape: N1×3)
    'det': Detected point cloud in ndarray. (shape: N2×3)
    'det_normal': Normal vectors of the detected point cloud in ndarray. (shape: N2×3)
    'r': Ground truth rotation matrix in ndarray. (shape: 3×3)
    't': Ground truth translation vector in ndarray. (shape: 3×1)

5. Usage:
   You can download this dataset by "git clone https://github.com/macs-lab/iLSPR-inspection.git" in terminal and open the ".pkl" files by "pickle" package in Python.

6. License
   Our dataset is released under MIL License (see License file for more details)
  