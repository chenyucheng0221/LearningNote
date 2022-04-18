## Lighting / illumination Estimation
### Existing solutions
- utilize auxiliary information and user annotation (traditional methods)
- regress representative illumination parameters (deep learning)
- generate illumination maps (deep learning)

### PaperList
#### 2D

- [Learning to predict indoor illumination from a single image](#learning-to-predict-indoor-illumination-from-a-single-image)
- [Deeplight: light source estimation for augmented reality using deep learning](#deeplight-light-source-estimation-for-augmented-reality-using-deep-learning)
- [Deeplight: Learning illumination for unconstrained mobile mixed reality](#deeplight-learning-illumination-for-unconstrained-mobile-mixed-reality)

#### 360 images

****
### Learning to predict indoor illumination from a single image
- the first end-to-end lighting estimation method
- input: limited FOV LDR RGB image, output: HDR panorama
- method
  - HDR images are difficult to get, firstly using the LDR images to train CNN network, but lighting intensity can not be differentiated from LDR images;
  then using HDR images to fine-tune.
  - Lighting detector to get the light source
  - spherical warp to solve the problem that the panorama center of projection can be arbitrarily far away from the location of the scene points in the cropped photo
  <img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting%20estimation-1.png" width="70%" height="70%">
- Discussion
  - From the structure, we can see that the lighting location is inferred from LDR images but intensity from HDR, since the HDR data is limited, the fine-tune step may not get good result compared with the lighting location estimation stage
  - I think because we just use limited FOV images as input, it may fail to get better performance if the scene's geometric distribution is complex and the lighting source is out of view
  - In current network, color assignment scheme is simple and can be improved
  - This work just perform lighting estimation, but tasks like geometry estimation/reconstruction, reflection estimation and intrinsic images can benefit from each other, this can be the future work direction
  
### Deeplight: light source estimation for augmented reality using deep learning
- input: RGB-D data, output: dominant light source direction
<img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-2.png" width="70%" height="70%">
- Discussion
  - This method utilize synthetic data, just using the single lighting source, which might not operate properly in complex real scenes

### Deeplight: Learning illumination for unconstrained mobile mixed reality
- input: LDR, limited-FOV input image captured with a mobile device, output: HDR ligting
- method:
  - capture training LDR images using three spheres with different material
  - measure each sphere's reflectance field
  - render the spheres with the estimated HDR lighting using image-based relighting
  - use an adversarial loss to improve
  <img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-3.png" width="70%" height="70%">
 - Discussion
   - In this work, the camera just capture the bottom portion of each sphere, this can cause the inaccuacy in real world scene
   - The training data and test data are captured by the same camera, which is not a good choice
   - the spheres lack enough geometric properties, this may limit the model's application in real-world scene

****
