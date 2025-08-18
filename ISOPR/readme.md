# Supplementary Materials of iLSPR Manuscript

### Manuscript Title

iLSPR: A Learning-based Scene Point-cloud Registration Method for Robotic Spatial Awareness in Intelligent Manufacturing

### Authors 
Yusen Wan, Xu Chen

###

## Industrial Scene Object Point-cloud Registration (ISOPR) dataset


### Background

With the rise of robotic manufacturing, vision-based scene reconstruction methods have become essential, high-precision reconstruction of manufacturing scenes, particularly target workpieces, has emerged as a cornerstone of robotic intelligence. In the manuscript, we proposed a Learning-based Scene Point-cloud Registration Method for automatic industrial scene reconstruction, which leverages point clouds as 3D representation and can estimate the positions and orientations of workpieces in the industrial scenes. For the experimental evaluation, we conducted Industrial Scene Object Point-cloud Registration (ISOPR) dataset. Because, though there are large datasets (ModelNet40, ABC, and so on) for benchmarking, they lack simulation of authentic depth camera sampling, which means the experimental formulations in the previous literature are unsuitable. 

### Introduction
To simulate the depth camera and generate sensor-realistic point clouds for industrial scene pointcloud registration, we construct the ISOPR Dataset using NVIDIA Isaac Sim simulator, a robotics simulation platform developed on the NVIDIA Omniverse framework.

In IsaacSim, We built a robitc manufacturing scene, which consists of a Universal Robot Arm UR10, a semi-enclosed rectangular platform, a depth camera provided by Isaac Sim fixed on the platform, and the workpiece (object). In ISOPR, the resolution of the depth camera is 640×480 pixels, and the horizontal field of view is 30°. The workpieces are selected from the digital model library. Sample workpieces, including various connectors, supporters, and shells, are shown in Figure 2.

Figure shows the process of data collection of ISOPR. The data collection involves the following key steps: (i) place the work-ieces from digital model library randomly within [−0.2m, 0.2m]; (ii) rotate the workpieces randomly within [−45.0◦, 45.0◦]; (iii) capture the point clouds of the whole scene by the depth camera; (iv) segment the point clouds by a predefined bounding box to obtain the point clouds of the workpieces; (v) down-sample the point clouds by voxelization, whose resolution of each sample is selected from {50, 100, 200, 500, 1000, 2000} to make the number of points exceed 1024 while remaining as close as possible, because previous work was developed based on point clouds around 1024. Finally, we obtain 2000 samples for testing. Some samples are shown in Figure.

ISOPR can be used to evaluate the point-cloud registration methods. The methods need to align the source point cloud and reference point cloud and estimate the rotation matrixes and translation vectors. Then, compared with the GT value, the performance of methods can be evaluated.

### Structure

The folder contains all data for ISOPR, structured across 5 ".pkl" files. Each file comprises 400 samples, totally 2000 samples. Every sample is stored as a dictionary with the following keys:

   'gt': point cloud of Ground truth CAD model in ndarray. (shape: N1×3)
   'gt_normal': Normal vectors of the ground truth point cloud in ndarray. (shape: N1×3)
   'det': Detected point cloud in ndarray. (shape: N2×3)
   'det_normal': Normal vectors of the detected point cloud in ndarray. (shape: N2×3)
   'R': Ground truth rotation matrix in ndarray. (shape: 3×3)
   't': Ground truth translation vector in ndarray. (shape: 3×1)

The 'gt' point cloud and the 'det' point cloud can be aligned by: $P_{gt} = RP_{det}+t $.


### Usage:
This dataset can be downloaded in terminal by:
'''
git clone https://github.com/macs-lab/iLSPR-inspection.git
cd iLSPR-inspection/ISOPR
'''

This dataset can be opened by "pickle" package in Python:

'''
import pickle as pkl
with open('ISOPR1.pkl', 'rb') as p:
    ISOPR = pkl.load(p)
''' 
 
### License

Our dataset is released under MIT License (see License file for more details)
  