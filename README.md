# Data Science Thesis 2021

This repository pertains to the **Data Science Thesis** of Adam Horvath-Reparszky at University of Amsterdam in 2021.

**Title**: Virtual Try-on with Realistic Hair using Occlusion Aware Image Painting Network

**Author**: Adam Horvath-Reparszky

* **Student-ID**: 13326481

* **Email**: adam.horvath-reparszky@student.uva.nl

**Internal Supervisior**: Dr. Shaodi You

* **Email**: s.you@uva.nl

**Company Supervisor**: Hernani Costa

* **Email**: hernani@lalaland.ai

<p align="middle">
  <img src="images\Cover_Img.png" width="750"/>
</p>


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
|Large Scale Image Completion via Co-Modulated Generative Adversarial Networks|https://openreview.net/pdf?id=sSjqmfsk95O| https://github.com/zsyzzsoft/co-mod-gan|

## Collected Custom Hair Occlusion Dataset

In order to, train the image inpainting network, firstly approximately 5,600 training images were manually selected from the VITON train dataset.

VITON contains a training set of 14,221 image pairs and a test set of 2,032 image pairs, each of which has a front-view woman photo and a top clothing image with the resolution 256 x 192. I used this dataset and manually selected those 5622 images where the target model has long hair and its is covering the shoulder or the garment.

<p align="middle">
  <img src="images\Manually_selected.png" width="256"/>
  <img src="images\Manually_selected_2.png" width="256"/>
</p>

Considering the fact that around 5,600 images have been manually labelled by myself, idea of training a Resnet classifier arose to collect more training data, via applying the classifier on larger dataset than VITON.



* Transfer Learning on Resnet50

In order to increase the number of training images for inpainting, DeepFashion dataset has been chosen to select those potential images where occlusion by hair appears. Checking this amount of images manually would take a lot of time and effort, therefore, transfer learning, more specifically fine-tuning has been applied on the pre-trained Resnet50 convolutional neural network using the already selected images as training data to train a classifier that selects the potential images which include hair occlusion.

<p align="middle">
  <img src="images\Resnet_flowchart.png" width="550"/>
</p>

Approximately 16,759 valid images have been selected, which results in almost three times bigger data collection than the first manually selected dataset.

<p align="middle">
  <img src="images\Resnet50_manually.png" width="256"/>
</p>


## Novel Data Preprocessing Method

A novel data preprocessing stage is used to identify occlusion areas on the output images from virtual try-on network. To produce adequate images to feed into the image inpainting network, cropping and masking steps are applied. The entire process consists of four main steps to prepare the final input images to the inpainting network. In regard of the two different inpainting networks, only the last step differs. 


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


<p align="middle">
  <img src="images\Data_Preprocessing.png" width="550"/>
</p>


## Image Inpainting

The original Co-modulated implementation conducted face inpainting experiments at 512x512 resolution on the FFHQ dataset,
therefore the first training approach in this research used the manually collected custom dataset, crop all the images by using face centring to create a similar data collection as FFHQ but in lower resolution and most importantly including the extended upper body parts where occlusion can be identified. The cropped dataset has been fed into training phase to extend the facial learnt features with upper body and occlusion appearances.

In contrast to the first implementation, for the second training quantitative and qualitative changes have been applied. Since StyleGAN based approaches usually use approximately 70,000 - 100,000 training images, which is significantly bigger than it was used for the first training, in order to narrow the gap and increase the number of training data, 16,759 images have been selected from DeepFashion dataset. As a result, it is almost quadrupled the size of the training data.

## Experiments
 Experimnets were conducted on three different state-of-the-art virtual try-on networks outputs.
 * **Parser-Free Virtual Try-on via Distilling Appearance Flows**
 * **Towards Photo-Realistic Virtual Try-On by Adaptively Generating↔Preserving Image Content (ACGPN)**
 * **CP-VTON+: Clothing Shape and Texture Preserving Image-Based Virtual Try-On**

* First Image Inpainting Network (Parser-Free/ACGPN/CP_VTON+)
 <p align="middle">
  <img src="images\Appendix_PF_AFN_1.png" width="256"/>
  <img src="images\Appendix_ACGPN_1.png" width="256"/>
  <img src="images\Appendix_CP_VTON_1.png" width="256"/>
</p>

* Second Image Inpainting Network (Parser-Free/ACGPN/CP_VTON+)
 <p align="middle">
  <img src="images\Appendix_PF_AFN_2.png" width="256"/>
  <img src="images\Appendix_ACGPN_2.png" width="256"/>
  <img src="images\Appendix_CP_VTON_2.png" width="256"/>
</p>
