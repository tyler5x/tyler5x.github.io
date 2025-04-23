---
name: Shipwreck Segmentation
tools: [PyTorch, Deep Learning, Image Processing, Experimental Design]
image: ../media/segmentation/segment.jpg
description: A 30 lb. Vertical Spinning Combat Robot built in a shop
# external_url: https://www.google.com
---

# Shipwreck Segmentation from Sonar 
This is a project for my graduate research as part of the Field Robotics Group (FRoG) at the University of Michigan. The project is funded by NOAA Ocean Exploration. 

The goal of the project is to create an open-source QGIS tool that detects shipwrecks from multibeam sonar data. Our tool allows users to pre-process raw bathymetry data, produce pixel-wise segmentation masks highlighting shipwrecks, threshold model outputs, and extract bounding boxes around the detected ships. Given the domain-specific barriers in collecting ample sonar data to train a model, we achieve high-quality segmentation results through a combination of synthetic data generation and optimizing our training methods. 

My contributions to the project focus primarily on improving the performance of the segmentation model through snythetic data generation, data augmentations, cross-validation during training, and designing experiments to determine effective methods for preprocessing and augmenting data. 

I will come back and add more technical detail in the future; For now, please take a look at some slides I made documenting the project and some of the results! 

<div style="max-width: 1000px; margin: 0 auto;">
  <iframe 
    src="https://docs.google.com/presentation/d/e/2PACX-1vT61yz4AJ3yJB4_-7wJcsdXPd7KRZRqq58DKBYP50olgFVjWcjgquq-LCoI61l3BxZzAwkpnPMSyxw4/pubembed?start=true&loop=false&delayms=30000"
    frameborder="0" width="100%" height="550px" 
    allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true">
  </iframe>
</div>