# Enhanced-Oral-Cancer-Analysis-using-Multi-Model-Fusion-and-GAN

Phase 1:

In this project, we have a dataset of approximately 1200 microscopic-level oral histopathological images, and we have to predict whether the cells are cancerous or non-cancerous. Oral Squamous Cell Carcinoma (OSCC) is a type of head and neck cancer. It is the 7th most common type of cancer worldwide and accounts for more than 90% of oral malignancies. Early detection of OSCC is thus essential for effective treatment. However, the gold standard method of microscopy-based histopathological investigation is often challenging, time-consuming, and depends on human experience. Thus, automation in the analysis of oral biopsy is needed for speed and accuracy in diagnosis. In this project, various deep learning models have been implemented for classification of oral histopathological images as cancerous or non-cancerous.
In this project, three pre-trained CNN architectures, viz. VGG-16, ResNet-50, and Inception-v3, have been used. These architectures have first been individually, and then a new model has been designed by concatenating the outputs generated by each one of them.

First of all, the VGG-16 architecture has been loaded with the input tensor, and its fully connected layers have been removed. Then, we have frozen all the layers of the architecture. After that, we have added two fully connected layers and, at last, a Sigmoid layer since we have to perform binary classification. The model has then been compiled using the Binary Cross Entropy loss function and the Adam optimizer. Afterward, we have trained the fully connected layers on our dataset and finally performed testing. We have performed these same operations on ResNet-50 and Inception-v3 as well- i.e., first, we built the model, then trained it, and finally tested it.

Finally, a new model has been designed. Each of the three architectures have been loaded with the input tensors, and all of their fully connected layers have been removed. Then, we have frozen all the layers of these architectures. The output of each model has then been flattened, and these outputs have been concatenated together. After that, we have added three fully connected layers and, at last, a Sigmoid layer since we have to perform binary classification. The model has then been compiled using the Binary Cross Entropy loss function and the Adam optimizer. Afterward, we have trained the fully connected layers on our dataset and finally performed testing.

On testing, among all four models, viz. VGG-16, ResNet-50, Inception-v3, and the concatenated model, it has been found that the concatenated model achieved the highest Accuracy and F1-score of 85.19% and 91.18%, respectively.

The high performance of the concatenated model is because the combined features may contain multiple patterns like circularity, roundness, compactness, etc.


