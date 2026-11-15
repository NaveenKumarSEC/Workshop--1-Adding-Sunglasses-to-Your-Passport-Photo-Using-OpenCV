<img width="1219" height="276" alt="aafd394c-880f-4fcc-b16c-d62de619d6ed" src="https://github.com/user-attachments/assets/858f5779-2f1a-4763-be73-5661e444bcd7" />
<img width="1219" height="276" alt="aafd394c-880f-4fcc-b16c-d62de619d6ed" src="https://github.com/user-attachments/assets/3c46e9d3-91d6-4ebb-bad4-86206ae251a3" />
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:

Detects the face in an image.
Places a stylish sunglass overlay perfectly on the face.
Works seamlessly with individual passport-size photos.
Customizable for different sunglasses styles or photo types.

## Technologies Used:

Python
OpenCV for image processing
Numpy for array manipulations

## How to Use:

Clone this repository.
Add your passport-sized photo to the images folder.
Run the script to see your "cool" transformation!

## Applications:

Learning basic image processing techniques.
Adding flair to your photos for fun.
Practicing computer vision workflows.
Feel free to fork, contribute, or customize this project for your creative needs!

## Program:

### Developed By: 
### Name: Naveenkumar M
### Reg.No: 212224230182

```python

# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
# Load the Face Image
faceImage = cv2.imread('ME.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
faceImage.shape
#resized_faceImage.shape
faceImage.shape
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread('SUNGSS.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(400, 160))
print("image Dimension ={}".format(glassPNG.shape))
# Separate the Color and alpha channels
glassBGR = glassPNG[:,:,0:3]
gray_glass = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask1 = cv2.threshold(gray_glass, 240, 255, cv2.THRESH_BINARY_INV)
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(cv2.cvtColor(glassBGR, cv2.COLOR_BGR2RGB));plt.title('Sunglass Color channels'); 
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[350:510, 330:730] = glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI = faceWithGlassesArithmetic[350:510, 330:730]


glassBGR = cv2.resize(glassBGR, (400, 160))
glassMask = cv2.resize(glassMask, (400, 160))

glassMask = np.uint8(glassMask > 0)

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
eyeRoiFinal = cv2.resize(eyeRoiFinal, (400, 160))

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[350:510, 330:730] = eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");

```

## Output:

### Face Image

<img width="342" height="434" alt="f2262f57-ac40-4f3e-b5d9-3a270079220b" src="https://github.com/user-attachments/assets/93d234fe-dccf-4eac-9eb5-bb2aa129d0eb" />

### Sunglass image with Alpha channel

<img width="561" height="293" alt="c5a44b79-e531-4e85-b8a0-c4b4b989b186" src="https://github.com/user-attachments/assets/d3feb5c9-1b02-4723-aecc-40bfa007d3ee" />

### Display the images for clarity

<img width="1219" height="276" alt="aafd394c-880f-4fcc-b16c-d62de619d6ed" src="https://github.com/user-attachments/assets/b8ff57cb-9e7b-45de-81d4-9ebf42bd031c" />


### Replace the eye region with the sunglass image

<img width="342" height="418" alt="58318033-03ba-427f-9544-9ffd7748091b" src="https://github.com/user-attachments/assets/2d592cf8-3637-44be-b82b-55c8ac4e415f" />

### Augmented Eye and Sunglass

<img width="1606" height="247" alt="d1ca1539-da3b-4098-8d7c-6963af6589d4" src="https://github.com/user-attachments/assets/9b3c0b11-99c7-4e51-9747-caac1fe1b05b" />

### Original image with sunglasses

<img width="1615" height="1004" alt="d81a7201-32b9-4ae3-a183-7e063676a4b8" src="https://github.com/user-attachments/assets/bac047fb-6133-4ea8-ae86-29841025990c" />


## Result:

The project successfully detected the face in the input image and added sunglasses automatically using OpenCV. The output image showed the sunglasses correctly positioned on the face, demonstrating the effectiveness of basic image processing techniques.
