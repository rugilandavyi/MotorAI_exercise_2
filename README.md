# MotorAI_exercise_2
Problem solving and feature engineering for geospatial and their AI/ML challenges

# RGB Mask Generation and ML Pipeline Fix

## Part (a)
The script combines three vector datasets into a single raster RGB mask. Each feature is assigned specific RGB values:
- Road Bound: [0, 0, 200]
- Buildings: [255, 0, 0]
- Road Markings: Various values

## Part (b)

## Problem 
The ML Pipeline broke down, possibly because of:

1.Identical Pixel Values Across Masks: If the raster masks have identical pixel values, the ML model might not be able to differentiate between different classes or segments, leading to confusion during the training phase. The ML pipeline likely broke down due to similar pixel values for 'broken line' [0, 20, 10] and 'dashed line' [0, 45, 70].

2.Insufficient Variability: Lack of variability in pixel values can result in insufficient training data, causing the model to perform poorly or not train at all.

## Solution
Number label of solution corresponds to that of problem cause

1.Ensure Distinct Pixel Values
Increase the color differentiation for 'broken line' and 'dashed line' features to avoid confusion in the ML model, in other words review and modify masks: Verify that the raster masks have distinct pixel values representing different classes or segments. If necessary, adjust the pixel values to ensure clear differentiation.

Another possible solution is Normalization: Normalize the pixel values to a standard range if the ML pipeline expects specific value ranges.

2.Increase Variability
Augmentation: Apply data augmentation techniques to increase variability within the dataset. This can include transformations such as rotation, scaling, and flipping.

Diverse Data Collection: Collect additional data with more variability in pixel values to enhance the training dataset.
