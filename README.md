# Underwater_image_preprocessing
This code is an adaptation of 'underwater-image-enhancement' https://github.com/pranjalibajpai/underwater-image-enhancement/tree/main#abstract, a repository by pranjalibajpai. 

## Workflow 
![image](https://github.com/karlroberts0401/Underwater_image_preprocessing/assets/93919314/ede4c960-aa61-4cfe-9db5-4433be96c80f)

The above workflow is followed except the adapted code uses solely averaging-based image fusion opposed to PCA-based fusion.
The adaptations to the code are as follows:
1. The ability to batch process imagery, i.e. the code processes all images in a folder and outputs the processed versions in a seperate folder.
2. Code efficiency optimisation to reduce process time per image e.g. utilising vectorised operations - Numpy arrays opposed to nested loops (which operate on each pixel) and using PyTorch tensors over PIL images allows for faster GPU utilisation.
3. Using Contrast Limited Adaptive Histogram Equalization (CLAHE) for contrast enhancement which adapts the enhancement locally. This is particularly useful for avoiding over-amplification of noise in regions with low contrast.
4. Parallel processing using 'ThreadPoolExecutor' in pythons 'concurrent.futures' module provides a high-level interface for asynchronously executing functions using threads. Each available CPU thread is used per image so multiple images can be processed concurrently. 
With these adaptations, based on operation from a WS-X1181G, Intel (R) Core(TM) i9-9980XE CPU @ 3.00GHz, 128GB usable RAM, 4x NVIDIA GeForce RTX 2080 GPUs, the final code operates at 2s per image.

## Results

![image](https://github.com/karlroberts0401/Underwater_image_preprocessing/assets/93919314/a16f6f28-2ef7-434c-b3fc-97166aab61e8)


![image](https://github.com/karlroberts0401/Underwater_image_preprocessing/assets/93919314/14b4fc9e-c5f3-48d3-a364-920b336b3c65)

## Discussion
- Scaling factor (lines 41 & 43) used to reduce artifacts (glowing red backscatter), is currently a workaround in lieu of a more permanent fix.
- Future underwater image capture may utilise color charts so that a true representation of the effects of the image processing can be observed.
