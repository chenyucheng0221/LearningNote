## Paper List

- onmidirectional images

title|year|source|keyword|link
-|-|-|-|-
Object Detection on Panoramic Images Based on Deep Learning|2017|ICCAR|A region-based CNN|[paper](http://static.tongtianta.site/paper_pdf/dad93a48-5f79-11e9-af33-00163e08bb86.pdf)
Real-Time Object Detection for 360-Degree Panoramic Image Using CNN|2017|ICVRV|A CNN-based detection framework with a post-processing fine-tune module|[paper](https://sci-hub.se/10.1109/icvrv.2017.00013)
Object Detection in Equirectangular Panorama|2018|ICPR|multi-projection with YOLO|[paper](https://arxiv.org/pdf/1805.08009.pdf)
Object Detection in Curved Space for 360-Degree Camera|2019|ICASSP|faster RCNN model based, multi-kernel layers|[paper](https://sci-hub.se/10.1109/icassp.2019.8683093)
OmniDRL: Robust Pedestrian Detection using Deep Reinforcement Learning on Omnidirectional Cameras|2019|ICRA||[paper](https://arxiv.org/pdf/1903.00676.pdf)
Grid Based Spherical CNN for Object Detection from Panoramic Images|2019|Sensors|grid-based spherical CNN,grid map, RPN|[paper](https://pdfs.semanticscholar.org/69ee/cdcdc183695087849b246942a1bd4f38d030.pdf?_ga=2.91932956.700321051.1649138034-1529344070.1647397271)
Spherical Criteria for Fast and Accurate 360-degree Object Detection|2020|AAAI|two-stage detector, sphIoU, sphBB|[paper](https://ojs.aaai.org/index.php/AAAI/article/download/6995/6849)
Unbiased IoU for Spherical Image Object Detection|2021|CVPR|unbiased Bounding box, unbiased IoU|[paper](https://arxiv.org/pdf/2108.08029.pdf)
Field-of-View IoU for Object Detection in 360  Images|2022|CVPR|computing intersection-over-union of two Field-of-View bounding boxes, 360 augmenttaion|[paper](https://arxiv.org/pdf/2202.03176.pdf)
 
- onmidirectional videos

title|year|source|keyword|link
-|-|-|-|-
ASOD60K: An Audio-Induced Salient Object Detection Dataset for Panoramic Videos|2021|||[paper](https://arxiv.org/pdf/2107.11629.pdf)
ongoing||||


## Conclusion
To migate the distortion from the projection of ODIs, here are two main challenges: (i) the traditional convolutional layers are not applicable as ODIs do not have a regular planar grid structure. (ii) the evaluation criteria adopted in planar object detection is not suitable because axis-aligned rectangles can not tightly bound objects in spherical images. So far most methods are focused on the first challenge, the latter is comparatively limited(In the paper list, the last three items are focused on this).


## Question
(1) In some papers, I found there are several projection ways, like perspective projection, spherical projection, cylindrical projection and cubic projection. Are all the 360 images stored as ERP format originally? Or they can store images like the following picture? 

![image](https://github.com/chenyucheng0221/LearningNote/blob/main/360-Survey/Images/360_images.png)

(2) Some papers illustrate that the input images of their network are fisheye images, however, fisheye cameras may have different FoV, can we regard the fisheye images as ODIs? like papers [paper1](https://arxiv.org/pdf/2003.03759.pdf) and [paper2](https://ieeexplore.ieee.org/ielx7/6287639/8948470/09066935.pdf) , I am not sure if they belong to object detection in ODIs.
