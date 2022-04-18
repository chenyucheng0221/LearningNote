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
- [A Dataset of Multi-Illumination Images in the Wild](#a-dataset-of-multi-illumination-images-in-the-wild)
- [Deep parametric indoor lighting estimation](#deep-parametric-indoor-lighting-estimation)
- [Fast spatially-varying indoor lighting estimation](#fast-spatially-varying-indoor-lighting-estimation)
- [Lighthouse: Predicting Lighting Volumes for Spatially-Coherent Illumination](#lighthouse-predicting-lighting-volumes-for-spatially-coherent-illumination)
- [IllumiNet: Transferring Illumination from Planar Surfaces to Virtual Objects in Augmented Reality](#illuminet-transferring-illumination-from-planar-surfaces-to-virtual-objects-in-augmented-reality)
- [Conclusion](#conclusion)

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
   - I think the spheres lack enough geometric properties, this may limit the model's application in real-world scene

### A Dataset of Multi-Illumination Images in the Wild
- similar to the deeplight method
- main contribution: introduce multi-illumination dataset, which is HDR and high resolution

### Deep parametric indoor lighting estimation
- directly estimate lighting source location and color
  - a: global lighting
  - l: lighting direction
  - d: distance from the camera
  - c: color
  - s: angular size of the lighting
 <img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-illumination-4.png" width="70%" height="70%">
 

- method
  - train network on a large dataset of labelled indoor HDR environment maps
  - encode an input RGB image into a latent feature vector
  - decode the latent feature vector for a fixed number of light source
- Discussion
  - This model based on diffuse area light-like sources so that cannnot model directional lights or light beams
  - Labelled HDR images are not easy to gey to pretrain the network

### Fast spatially-varying indoor lighting estimation
- motivation

In real world scene, the lighting changes in different location, it is hard to eatimate the global lighting, if we use the lighting of specific location, the rendering result can be more realistic

- input: an image and a 2D location, output: local lighting

- method
  - two path for a global and local image respectively
  - concatenate by a FC to produce latent vector
  - another FC layer to predict the 5-th-order SH coefficients in RGB
<img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-5.png" width="70%" height="70%">

- potential
  - the model can be applied to video to increase the prediction accuarcy

### Neural illumination: Lighting prediction for indoor environments
- infer a panoramic HDR illumination map representing the light arriving from all directions at the locale

- motivation
the result affected by many factors
  - the selection of the 3D location
  - the distribution of unobserved light sources
  - the occlusionns caused by the scene geometry

- method
  - geometry estimation
  - scene completion
  - LDR-to-HDR estimation
  - the three modules first train independently and then end-to-end train together
  - warp operation is to change the locale to the middle
  
<img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-6.png" width="70%" height="70%">

- Discussion
  - when the lighting source can not be observed in the input images, the estimation result may not accuate
  - use reflection and geometric properties to help estimate the illumination in the future

### Lighthouse: Predicting Lighting Volumes for Spatially-Coherent Illumination
- estimate the incident illumination at any 3D location
- motivation
  - existing methods estimate a single illumination for the entire scene
  - existing methods estimate the illumination at each 3D location without enforcing that the predictions are consistent with the same 3D scene
- input: narrow-baseline stereo image pair

- method
  - use MPI as the intermediate representation
    - MPI(multiplane image): the object captured is in different depth, split these depth to get multiple 2D images
    <img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/MPI.png" width="70%" height="70%">
  - use 3D CNN to predict the MPI representation
  - resample MPI to a multiscale volume
  - complete this volume with another 3D CNN: predict the lighting out view
  - use volume rendering at selective location
<img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-7.png" width="70%" height="70%">

- disadvantage
  - rely on stereo pair of images, it is difficult to get in real world

### IllumiNet: Transferring Illumination from Planar Surfaces to Virtual Objects in Augmented Reality
- a novel method: directly infer the rendered virtual object by transferring the illumination features instead of recovering an environment map
- method
  - detect the plannar surfaces in the scene
  - compute overall illumination 
  - extract illumination deep features by graph autoencoder
  - use GAN to transfer the feature to the virtual object
  - insert the object into image
<img src="https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/lighting-estimation-9.png" width="70%" height="70%">

- Discussion
   - The method is binding the specific virtual object, if there is any changes in the object, we have to change model and re-train it.

### Conclusion
- There no unified lighting datasets to evaluate the above methods which is better
- From their result, I get a rough estimation that the illumiNet may get the comparably higher accuracy
- Existing methods seldom use the refelction and geometry estimation to help perform the lighting estimation
- Most work use the synthetic dataset, transfer learning may be utilized to bridge the gap between them and real-world dataset.
