# Supplementary Materials of iLSPR Manuscript

This repository contains supporting materials of the paper "iLSPR: A Learning-based Scene Point-cloud Registration Method for Robotic Spatial Awareness in Industrial Manufacturing"
This project includes the following items:
- 1. the dir named "geometric primitives" stores the geometric primitives used in GPDG method.
- 2. the dir "digital model library" stores the CAD models of the digital model library.
- 3. the dir named "ISOPR" store the ISOPR dataset and corresponding documents.

All the CAD models are in ".stl" format. The ISOPR Dataset is a pkl file.


## Catalogue
- [Introduction of the Manuscript](#introduction-of-the-manuscript)
- [Industrial Scene Object Point-cloud Registration (ISOPR) dataset](#industrial-scene-object-point-cloud-registration-isopr-dataset)
- [Geometric Primitives](#geometric-primitives)
- [Digital Model Library](#digital-model-library)

## Introduction of the Manuscript

### Title

iLSPR: A Learning-based Scene Point-cloud Registration Method for Robotic Spatial Awareness in Intelligent Manufacturing

### Authors 
Yusen Wan, Xu Chen
Department of Mechanical Engineering, University of Washington, 3900 E Stevens Way NE, Seattle, 98195, Washington, the United States

### Abstract

A critical capability for intelligent manufacturing is the ability for robotic systems to understand the spatial operation environment – the ability for robots to precisely recognize and estimate the spatial positions and orientations of objects in the industrial scenes. Existing scene reconstruction methods are designed for general settings with low precision needs of objects
and abundant data. However, manufacturing hinges on high object precision and operates with limited data. Addressing such challenges and limitations, we propose a novel learning-based Scene Point-cloud Registration framework for automatic industrial scene reconstruction (iLSPR). The proposed iLSPR framework leverages point cloud representation and integrates three key innovations: (i) a Multi-Feature Robust Point Matching Network (MF-RPMN) that learn from both raw data and deep features of the objects to accurately align point clouds, (ii) a Geometric-Primitive-based Data Generation (GPDG) method for efficient synthetic data generation, and (iii) a digital model library of industrial target objects. During operation, vision sensors capture point clouds in the scenes, and the iLSPR method registers high-fidelity object models in the scenes using MF-RPMN, pre-trained with GPDG-generated data. We introduce an Industrial Scene Object Pointcloud Registration (ISOPR) dataset in IsaacSim to benchmark performance. Experimental results demonstrate that iLSPR significantly outperforms existing methods in accuracy and robustness. We further validate the approach on a real-world robotic manufacturing system, demonstrating reliable digital reconstruction of industrial scenes.



## Industrial Scene Object Point-cloud Registration (ISOPR) dataset

### Background

With the rise of robotic manufacturing, vision-based scene reconstruction methods have become essential, high-precision reconstruction of manufacturing scenes, particularly target workpieces, has emerged as a cornerstone of robotic intelligence. In the manuscript, we proposed a Learning-based Scene Point-cloud Registration Method for automatic industrial scene reconstruction, which leverages point clouds as 3D representation and can estimate the positions and orientations of workpieces in the industrial scenes. For the experimental evaluation, we conducted Industrial Scene Object Point-cloud Registration (ISOPR) dataset. Because, though there are large datasets (ModelNet40, ABC, and so on) for benchmarking, they lack simulation of authentic depth camera sampling, which means the experimental formulations in the previous literature are unsuitable. 

### Introduction
To simulate the depth camera and generate sensor-realistic point clouds for industrial scene pointcloud registration, we construct the ISOPR Dataset using NVIDIA Isaac Sim simulator, a robotics simulation platform developed on the NVIDIA Omniverse framework.

![text](https://github.com/macs-lab/iLSPR-inspection/blob/main/Images/gtmodel.png)

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="这里输入图片地址">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">这里输入题注</div>
</center>

作者：一瓶矿泉水
链接：https://www.zhihu.com/question/42802592/answer/383110578
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

In IsaacSim, We built a robitc manufacturing scene, which consists of a Universal Robot Arm UR10, a semi-enclosed rectangular platform, a depth camera provided by Isaac Sim fixed on the platform, and the workpiece (object). In ISOPR, the resolution of the depth camera is 640×480 pixels, and the horizontal field of view is 30°. The workpieces are selected from the digital model library. Sample workpieces, including various connectors, supporters, and shells, are shown in Figure 2.

![text](https://github.com/macs-lab/iLSPR-inspection/blob/main/Images/gtmodel.png)

Figure 1 shows the process of data collection of ISOPR. The data collection involves the following key steps: (i) place the work-ieces from digital model library randomly within [−0.2m, 0.2m]; (ii) rotate the workpieces randomly within [−45.0◦, 45.0◦]; (iii) capture the point clouds of the whole scene by the depth camera; (iv) segment the point clouds by a predefined bounding box to obtain the point clouds of the workpieces; (v) down-sample the point clouds by voxelization, whose resolution of each sample is selected from {50, 100, 200, 500, 1000, 2000} to make the number of points exceed 1024 while remaining as close as possible, because previous work was developed based on point clouds around 1024. Finally, we obtain 2000 samples for testing. Some samples are shown in Figure.

ISOPR can be used to evaluate the point-cloud registration methods. The methods need to align the source point cloud and reference point cloud and estimate the rotation matrixes and translation vectors. Then, compared with the GT value, the performance of methods can be evaluated.

### Structure

The folder contains all data for ISOPR, structured across 5 ".pkl" files. Each file comprises 400 samples, totally 2000 samples. Every sample is stored as a dictionary with the following keys:

- 'gt': point cloud of Ground truth CAD model in ndarray. (shape: N1×3)
- 'gt_normal': Normal vectors of the ground truth point cloud in ndarray. (shape: N1×3)
- 'det': Detected point cloud in ndarray. (shape: N2×3)
- 'det_normal': Normal vectors of the detected point cloud in ndarray. (shape: N2×3)
- 'R': Ground truth rotation matrix in ndarray. (shape: 3×3)
- 't': Ground truth translation vector in ndarray. (shape: 3×1)

The 'gt' point cloud and the 'det' point cloud can be aligned by: $P_{gt} = RP_{det}+t $.


### Usage:
This dataset can be downloaded in terminal by:
```
git clone https://github.com/macs-lab/iLSPR-inspection.git
cd iLSPR-inspection/ISOPR
```

This dataset can be opened by "pickle" package in Python:

```
import pickle as pkl
with open('ISOPR_0.pkl', 'rb') as p:
    ISOPR = pkl.load(p)
``` 
 
### License

Our dataset is released under MIT License (see './ISOPR/License.txt' file for more details)


## Geometric Primitives

In mechanical designing and computer-assisted design, geometric primitives are the simplest, irreducible geometric shapes that serve as foundational building blocks for constructing complex 3D models or scenes. Geometric primitives include triangular, quadrangular, pentagonal, hexagonal, heptagonal, and octagonal prisms and pyramids, as well as cylinders, cones, and spheres.

In this manuscript, we generates synthetic part point clouds using a set of geometric primitives, grounded in the engineering design principle that mechanical components are typically constructed through CAD operations—such as Boolean unions, subtractions, and intersections—applied to geometric primitives.

This dir stores the geometric primitives used in our manuscript.


## Digital Model Library

The digital model library stores the ground truth CAD models of each production line’s specific products that serve as the target objects. In our work, we collected 67 CAD models and built the digital model library, which are used to collect ISOPR dataset in IsaacSim and generate authentic point clouds for model training.
