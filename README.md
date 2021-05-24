# Data Science Thesis 2021

This repository pertains to the **Data Science Thesis** of Adam Horvath-Reparszky at University of Amsterdam in 2021.

**Link to the paper** : https://www.overleaf.com/project/6071a080ced8b32b96aa5101

**Author**: Adam Horvath-Reparszky

* **Student-ID**: 13326481

* **Email**: adam.horvath-reparszky@student.uva.nl

**Internal Supervisior**: Dr. Shaodi You

* **Email**: s.you@uva.nl

**Company Supervisor**: Hernani Costa

* **Email**: hernani@lalaland.ai


## Thesis Schedule
| Week  | Date | Planned Achievement  | Achieved |
| ------------- | ------------- | ------------- | ------------- |
| Week 1 | 29/03 - 04/04 | Examine research papers in the field of garment transferring | Almost 20-25 related research papers, 5 of them have been selected as most related papers ( I will focus on these implementations) |
| Week 2 (Current) | 05/04 - 11/04  | Start to do experiments using the selected papers. Decide which dataset I am going to use | I decided to use the VITON dataset, beacuse it is public and most used benchmark dataset. Experiments on Parser-Free, CP_VITON+ and ACGPN implementation |
| Week 3 |  12/04 - 18/04 | Finish experiments and start to identify general problems and categorise them. Select the evaluation measures | The general issues are the complex body poses and the hair if its cover the upper body. Since handling the hands is difficult since those parts of the bady are affected in the virtual tryon, I decided to focus on the hair occlusion part. The evaluation measures have been selected, however I am not sure that I will use them because it can happen that only visual comparison will be presented on the results. |
| Week 4  | 19/04 - 25/04 | Start writing the Abstartct/Introduction/Related Work part in the Thesis draft | I started to write the thesis draft, but the plan changed a bit, I had to read more about segmentation and chechk the training code for each implementation. The introduction will be almost the last part I will write, but the related work part will be almost the same. Bit more on segmentation has to be added.|
| Week 5 |  26/04 - 02/05 | Writing the Thesis draft (Abstract/Intro/Literature review). Get new ideas how to solve existing problems (artifacts) | I did not write the Thesis draft so in the following weeks I have to focus on that one, but I made a big progress on segmentation. |
| Week 6  |  03/05 - 09/05 | Try out solutions for solving problems. Improve teh Realted Work and dataset part.| Selected all 5600 images from VITON dataset. Created the python script which uses segmentation, center position image croping, build up the basic of Image Inpainting Network |
| Week 7 | 10/05 - 16/05 | Try out solutions for solving problems. Improve the Thesis Draft | Image Inpaiting network debugging + idea of resnet50 classifier |
| Week 8  | 17/05 - 23/05 | Writing Methodology + Results | Build a Resnet50 classifier to increase the training data using DeepFashion dataset, the training is ready, Image Inpainting network crash after 5 mins of training so debugging is in progress |
| Week 9 | 24/05 - 30/05 | Writing the Thesis draft + get the prediction from the classifier + start the inpainting training|  |
| Week 10  | 31/05 - 06/06 | Evaluation part |  |
| Week 11 | 07/06 - 13/06 | Finalise the Methodology part + Future work|  |
| Week 12  | 14/06 - 20/06 | Final version of Thesis Draft |  |
| Week 13 | 21/06 - 27/06 | Finishing the thesis and prepare for Thesis Defense |  |

## Most related research papers
| Name of the paper  | Link to paper | Link to code |
| ------------- | ------------- | ------------- |
| Parser-Free Virtual Try-on via Distilling Appearance Flows| https://arxiv.org/pdf/2103.04559v2.pdf | https://github.com/geyuying/PF-AFN |
|VITON-HD: High-Resolution Virtual Try-On via Misalignment-Aware Normalization| https://arxiv.org/pdf/2103.16874v1.pdf| Not available|
|VOGUE: Try-On by StyleGAN Interpolation Optimization| https://vogue-try-on.github.io/| Not available |
|Towards Photo-Realistic Virtual Try-On by Adaptively Generating↔Preserving Image Content|https://openaccess.thecvf.com/content_CVPR_2020/papers/Yang_Towards_Photo-Realistic_Virtual_Try-On_by_Adaptively_Generating-Preserving_Image_Content_CVPR_2020_paper.pdf|https://github.com/switchablenorms/DeepFashion_Try_On|
|CP-VTON+: Clothing Shape and Texture Preserving Image-Based Virtual Try-On| https://minar09.github.io/cpvtonplus/cvprw20_cpvtonplus.pdf| https://github.com/minar09/cp-vton-plus|
|Disentangled Cycle Consistency for Highly-realistic Virtual Try-On|https://arxiv.org/pdf/2103.09479.pdf| https://github.com/ChongjianGE/DCTON|
|Do Not Mask What You Do Not Need to Mask: a Parser-Free Virtual Try-On(WUTON)|https://arxiv.org/pdf/2007.02721.pdf| Not available|
|Image Based Virtual Try-on Network from unpaired data - Amazon research|https://assets.amazon.science/1a/2b/7a4dd8264ce19a959559da799aff/scipub-1281.pdf| Not available|
|Style and Pose Control for Image Synthesis of Humans from a Single Monocular View|https://arxiv.org/pdf/2102.11263.pdf| Not available|





## Experiments examples by paper
* Parser-Free Virtual Try-on via Distilling Appearance Flows
<p align="middle">
  <img src="images\parser_free_1.jpg" width="256"/>
  <img src="images\parser_free_2.jpg" width="256"/>
  <img src="images\parser_free_3.jpg" width="256"/>
</p>

* Towards Photo-Realistic Virtual Try-On by Adaptively Generating↔Preserving Image Content
<p align="middle">
  <img src="images\ACGPN_demo_1.jpg" width="256"/>
  <img src="images\ACGPN_demo_2.jpg" width="256"/>
</p>
<p align="middle">
  <img src="images\ACGPN_demo_3.jpg" width="256"/>
  <img src="images\ACGPN_demo_4.jpg" width="256"/>
</p>

* CP-VTON+: Clothing Shape and Texture Preserving Image-Based Virtual Try-On
<p align="middle">
  <img src="images\cp_viton_plus_demo_1.jpg" width="256"/>
  <img src="images\cp_viton_plus_demo_2.jpg" width="256"/>
  <img src="images\cp_viton_plus_demo_3.jpg" width="256"/>
</p>
<p align="middle">
  <img src="images\cp_viton_plus_demo_4.jpg" width="256"/>
  <img src="images\cp_viton_plus_demo_5.jpg" width="256"/>
</p>


## Segmentation and occlusion identification on hair
Since handling hands is more complex because those parts of the body are affected in the virtual tryon, I started build a network for hair extraction and occlusion identification using the target pose and target garment. In this section I present the current results.
* Step 0. - Target Model and target garment = result of Virtual Tryon network
<p align="middle">
  <img src="images\original_img.jpg" width="256"/>
  <img src="images\traget_garment.jpg" width="256"/>
  <img src="images\result_img_1.jpg" width="256"/>
</p>

* Step 1. - Hair mask + extract the hair from the original image
<p align="middle">
  <img src="images\hair_mask.jpg" width="256"/>
  <img src="images\extracted_original_hair.jpg" width="256"/>
</p>

* Step 2. - Warped target garment and mask of it
<p align="middle">
  <img src="images\warped_target_garemnt.jpg" width="256"/>
  <img src="images\warp_mask.jpg" width="256"/>
</p>

* Step 3. - Identify the occlusion parts
<p align="middle">
  <img src="images\hair_mask.jpg" width="256"/>
  <img src="images\warp_mask.jpg" width="256"/>
  <img src="images\hair_occlusion.jpg" width="256"/>
  <img src="images\extracted_occlusion_part.jpg" width="256"/>
</p>

* Step 4. - Example to how to change the hair
<p align="middle">
  <img src="images\original_without_hair.jpg" width="256"/>
  <img src="images\new_hair_mask.jpg" width="256"/>
  <img src="images\new_img.jpg" width="256"/>
</p>

## Hair inpainting network

* Preprocessing Step 1. - Hair and upperbody segmentation - Implementation: https://github.com/PeikeLi/Self-Correction-Human-Parsing
<p align="middle">
  <img src="images\segmentation_example_1.png" width="256"/>
  <img src="images\segmentation_example_2.png" width="256"/>
  <img src="images\segmentation_example_3.png" width="256"/>
</p>

* Preprocessing Step 2 - Image croping

Using the coordinates of the hair mask, I identified that 130x130 croping images will include almost all hair parts from the custom dataset. To get these value I plotted all max values assigned to hair mask in each image both horizontal and vertical way. In order to get the face in the center position (horizontal way) I adjust the croping by using the horizontal min and max cooridinates.

<p align="middle">
  <img src="images\croped_images\000061_0.png" width="256"/>
  <img src="images\croped_images\000073_0.png" width="256"/>
  <img src="images\croped_images\000139_0.png" width="256"/>
  <img src="images\croped_images\000141_0.png" width="256"/>
</p>



## Dataset

VITON contains a training set of 14,221 image pairs and a test set of 2,032 image pairs, each of which has a front-view woman photo and a top clothing image with the resolution 256 x 192. I used this dataset and manually selected those 5622 images where the target model has long hair and its is covering the shoulder or the garment. Using this custom dataset, I trained a Resnet50 classifier to extend my inpainting training data via select the proper images from DeepFashion dataset.

* Training Resnet50 "Long hair" classifier

The training data for "valid" images are which I selected manually from VITON dataset. For "invalid" images, I randomly selected 5600 images from those images which were not manually selected (short hair images or where the hair is not front of the body). After training the pretrained Resnet50 network with these data, the best accuracy on validation set was 91,5% after 5 epochs.

<p align="middle">
  <img src="Resnet50_hair_classifier\Model_prediction_example.jpg" width="256"/>
</p>


* Valid example -- Original image / Body part segmentation / Removing everything except hair and face mask (input of the model)

<p align="middle">
  <img src="Resnet50_hair_classifier\Valid_examples\000141_0.jpg" width="256"/>
  <img src="Resnet50_hair_classifier\Valid_segmentation_examples\000141_0.png" width="256"/>
  <img src="Resnet50_hair_classifier\Valid_model_input\000141_0.png" width="256"/>
</p>

* Invalid example -- Original image / Body part segmentation / Removing everything except hair and face mask (input of the model)

<p align="middle">
  <img src="Resnet50_hair_classifier\Invalid_examples\000044_0.jpg" width="256"/>
  <img src="Resnet50_hair_classifier\Invalid_segmentation_examples\000044_0.png" width="256"/>
  <img src="Resnet50_hair_classifier\Invalid_model_input\000044_0.png" width="256"/>
</p>

## Qualitative Evaluation

This thesis mainly perform visual comparison of my method with recent proposed parser-based methods including VITON, Parser-free implementation, CPVTON+ and ACGPN.

I will use a classification, published by ACGPN implementation on VITON test data to get three different image pools categorised by difficulty (easy, medium, difficult).

## Quantitative Evaluation

* **Frechet Inception Distance (FID)** : is a metric used to assess the quality of images created by the generator of a generative adversarial network (GAN). Unlike the earlier inception score (IS), which evaluates only the distribution of generated images, the FID compares the distribution of generated images with the distribution of real images that were used to train the generator.
  * https://machinelearningmastery.com/how-to-implement-the-frechet-inception-distance-fid-from-scratch/
  * https://jonathan-hui.medium.com/gan-how-to-measure-gan-performance-64b988c47732
  * https://www.coursera.org/lecture/build-better-generative-adversarial-networks-gans/frechet-inception-distance-fid-LY8WK
  * https://github.com/mseitzer/pytorch-fid

* **Structural similarity (SSIM)** :  is a method for predicting the perceived quality of digital television and cinematic pictures, as well as other kinds of digital images and videos. SSIM is used for measuring the similarity between two images. The SSIM index is a full reference metric; in other words, the measurement or prediction of image quality is based on an initial uncompressed or distortion-free image as reference.
  * https://medium.com/srm-mic/all-about-structural-similarity-index-ssim-theory-code-in-pytorch-6551b455541e


