# Machine Learning for Healthcare

## Phase 1:

In this project, we have a dataset of approximately 1200 microscopic-level oral histopathological images, and we have to predict whether the cells are cancerous or non-cancerous. Oral Squamous Cell Carcinoma (OSCC) is a type of head and neck cancer. It is the 7th most common type of cancer worldwide and accounts for more than 90% of oral malignancies. Early detection of OSCC is thus essential for effective treatment. However, the gold standard method of microscopy-based histopathological investigation is often challenging, time-consuming, and depends on human experience. Thus, automation in the analysis of oral biopsy is needed for speed and accuracy in diagnosis. In this project, various deep learning models have been implemented for classification of oral histopathological images as cancerous or non-cancerous.

In this project, three pre-trained CNN architectures, viz. VGG-16, ResNet-50, and Inception-v3, have been used. These architectures have first been individually, and then a new model has been designed by concatenating the outputs generated by each one of them.

First of all, the VGG-16 architecture has been loaded with the input tensor, and its fully connected layers have been removed. Then, we have frozen all the layers of the architecture. After that, we have added two fully connected layers and, at last, a Sigmoid layer since we have to perform binary classification. The model has then been compiled using the Binary Cross Entropy loss function and the Adam optimizer. Afterward, we have trained the fully connected layers on our dataset and finally performed testing. We have performed these same operations on ResNet-50 and Inception-v3 as well- i.e., first, we built the model, then trained it, and finally tested it.

Finally, a new model has been designed. Each of the three architectures have been loaded with the input tensors, and all of their fully connected layers have been removed. Then, we have frozen all the layers of these architectures. The output of each model has then been flattened, and these outputs have been concatenated together. After that, we have added three fully connected layers and, at last, a Sigmoid layer since we have to perform binary classification. The model has then been compiled using the Binary Cross Entropy loss function and the Adam optimizer. Afterward, we have trained the fully connected layers on our dataset and finally performed testing.

On testing, among all four models, viz. VGG-16, ResNet-50, Inception-v3, and the concatenated model, it has been found that the concatenated model achieved the highest Accuracy and F1-score of 85.19% and 91.18%, respectively.

The high performance of the concatenated model is because the combined features may contain multiple patterns like circularity, roundness, compactness, etc.


## Phase 2:

In the 2nd phase, we have worked on the segmentation of cancerous images into cancerous and non-cancerous regions. For this task, we have used a labelled dataset of approximately 800 images. For modelling, we have used Generative Adversarial Networks (GANs), which consist of two components: a Generator and a Discriminator. We feed a real image to the Generator, and it generates a fake segmentation mask corresponding to that image. Along with this fake mask, we concatenate the real image, which serves as the fake input to the Discriminator. Now, the Discriminator receives both the fake input and the real input. The real input is actually the concatenation of the real mask and the real image. We feed both the fake input and the real input to the Discriminator, which classifies whether the fake input is indeed fake. The aim of the Generator is to produce a fake mask that is as close to the real mask as possible.

![GAN](https://github.com/user-attachments/assets/f8d820da-c643-4317-810a-3a0d4ef44199)


We have used U-Net as our Generator. It is a U-shaped CNN architecture developed for biomedical image segmentation. It follows an encoder-decoder architecture. On the left side of this architecture, we have four encoder blocks, and on the right side, we have four decoder blocks. The encoder receives the input image, then extracts useful features from that image using multiple convolutional layers. The decoder then upsamples the features using transpose convolution and concatenates them using skip connections. As a result, we get a segmentation mask as the output from this network. Another important feature of U-Net is the use of skip connections. Skip connections bypass some layers in the neural network and feed the output of one layer directly as the input to the next layer. This process helps transfer selected features directly from the encoder to the decoder part of the network, which, in turn, helps the decoder generate a better segmentation mask. We feed our original image to the Generator, which generates the fake mask. The fake mask is then compared with the ground truth, and the Mean Absolute Error (MAE) is calculated. The fake input is fed to the Discriminator, and the output of the Discriminator is compared with 1 to compute the Binary Cross Entropy (BCE) loss. Since, even for a fake image, we want the Discriminator to predict it as real, the loss is computed against 1. This ensures that the Generator improves its ability to generate fake masks that closely resemble the ground truth. The two losses are combined as: L = λ × (MAE) + (BCE). The MAE loss alone gives blurry results, while the BCE loss alone gives sharper results but introduces visual artifacts. Therefore, these two are combined with λ = 100 to achieve sharper results with minimal artifacts. Finally, gradients are backpropagated, and the whole process is repeated.

![Generator](https://github.com/user-attachments/assets/2a2cffc2-3c4f-4be3-bfb5-90ff16ce4d6e)

![Weight Updation in Generator](https://github.com/user-attachments/assets/bbacce8a-0085-4ef5-84c5-685eaf838374)

We have implemented PatchGAN as our Discriminator. It tries to classify whether each N × N patch in an image is real or fake. We have used N = 70. The Discriminator runs convolutionally across the image, averaging all responses to provide the final output. For real input to the Discriminator, we compare it with 1, and for the fake input, we compare it with 0. The BCE losses are calculated and combined. Finally, the gradients are backpropagated, and the whole process is repeated.

![Weight Updation in Discriminator](https://github.com/user-attachments/assets/9382e339-7088-44f8-9046-e6570275f3cc)

The Generator and Discriminator have been trained alternatively, with a batch size of 32 and number of epochs set to 10. For optimization, we have used the Adam optimizer. Finally, on testing, we have achieved a Mean Squared Error (MSE) of 4.81, a Peak Signal-to-Noise Ratio (PSNR) of 18.92, and a Structural Similarity Index Measure (SSIM) of 0.71.

![Result](https://github.com/user-attachments/assets/02620e27-7825-426c-b311-b43a310b10ed)

