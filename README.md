# MotorAI_exercise_2
Problem solving and feature engineering for geospatial data and their AI/ML challenges

# RGB Mask Generation and ML Pipeline Fix

## Part (a)
The script combines three vector datasets into a single raster RGB mask. Each feature is assigned specific RGB values:
- Road Bound: [0, 0, 200]
- Buildings: [255, 0, 0]
- Road Markings: Various values

## Part (b)

## Problem 
The ML Pipeline broke down, possibly because of:

1. Identical Pixel Values Across Masks: If the raster masks have identical pixel values, the ML model might not be able to differentiate between different classes or segments, leading to confusion during the training phase. The ML pipeline likely broke down due to similar pixel values for road marking features such as the following
   
   Cycle Lane ([0, 40, 0]) and Solid Line ([0, 45, 0]):
   The green values are very close (40 and 45), which could be easily confused by the model.

   Dashed Line ([0, 45, 70]) and Solid Line ([0, 45, 0]):
   Both have the same red and green values (0 and 45), differing only in the blue value (70 vs. 0).

   Solid Line ([0, 45, 0]) and Stop Line ([0, 85, 0]):
   Both are shades of green with values 45 and 85, respectively, which could still cause confusion.

   Pedestrian Crossing ([0, 100, 0]) and Stop Line ([0, 85, 0]):
   Both are green shades with values 100 and 85, respectively.

3. Insufficient Variability: Lack of variability in pixel values can result in insufficient training data, causing the model to perform poorly or not train at all.

## Solution
NOTE:Number label of solution corresponds to that of problem cause

1. Ensure Distinct Pixel Values:
Increase the color differentiation of features to avoid confusion in the ML model, in other words review and modify raster masks such that they have distinct pixel values representing different classes or segments.

    New Distinct Road Markings (features) pixel values:
   
    Broken Line: [0, 20, 10]
   
    Cycle Lane: [0, 255, 0]
   
    Dashed Line: [0, 0, 255]
   
    Pedestrian Crossing: [255, 255, 0]
   
    Solid Line: [255, 0, 255]
   
    Stop Line: [0, 255, 255]

    Normalization: Normalize the pixel values to a standard range if the ML pipeline expects specific value ranges.

3. Increase Variability
Augmentation: Apply data augmentation techniques to increase variability within the dataset. This can include geometric transformations of original dataset such as rotation, scaling, and flipping. 

    Diverse Data Collection: Collect additional data with more variability in pixel values to enhance the training dataset.
