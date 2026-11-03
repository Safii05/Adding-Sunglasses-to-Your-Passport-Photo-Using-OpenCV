# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Program:

import cv2 import numpy as np import matplotlib.pyplot as plt

faceImage = cv2.imread('ws.jpg') plt.imshow(faceImage[:,:,::-1]);plt.title("Face")

faceImage.shape

glassPNG = cv2.imread('sunglass.png',-1) plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")

glassPNG = cv2.resize(glassPNG,(500,400)) print("image Dimension ={}".format(glassPNG.shape))

glassBGR = glassPNG[:,:,0:3] glassMask1 = glassPNG[:,:,3]

plt.figure(figsize=[15,15]) plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels'); plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');

faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[230:630,250:750]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[230:630,250:750]

maskedEye = cv2.multiply(eyeROI,(1- glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20]) plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region") plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region") plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")

faceWithGlassesArithmetic[230:630,250:750]=eyeRoiFinal

plt.figure(figsize=[20,20]); plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image"); plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");

## Output:

<img width="722" height="552" alt="image" src="https://github.com/user-attachments/assets/818b972b-c3f7-466a-b655-67e1fe11cd1a" />
<img width="833" height="342" alt="image" src="https://github.com/user-attachments/assets/efe67754-879d-4dde-9b5b-f5bbb37be202" />

<img width="1375" height="262" alt="image" src="https://github.com/user-attachments/assets/3e7d6ec7-2feb-4702-abf2-149d1849a85c" />
<img width="797" height="545" alt="image" src="https://github.com/user-attachments/assets/182e17b4-4376-40b6-8211-b5a3314355aa" />
<img width="1467" height="220" alt="image" src="https://github.com/user-attachments/assets/f79207ed-7cac-45fd-9e88-bb2e699958cb" />
<img width="1580" height="823" alt="image" src="https://github.com/user-attachments/assets/f30857b0-a10c-4d91-8de4-044087d39208" />



## Result: 
The project successfully detected the face in the input image and added sunglasses automatically using OpenCV. The output image showed the sunglasses correctly positioned on the face, demonstrating the effectiveness of basic image processing techniques.






