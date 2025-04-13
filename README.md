# Image-classification---blood-cells
Deep learning for image classification of blood cells.

First challenge of the ANNDL course, polytecnic of Milan

## Introduction
Changes in blood cell counts can signal diseases like infections or cancer. Blood analysis is conducted via complete blood count or peripheral blood smear which take a long time and have low accuracy. Conventional machine learning methods aid blood cell classification but often require complex feature extraction. Deep learning approaches, particularly convolutional neural networks, could improve this by learning features autonomously, providing faster and more accurate diagnostics [4]. The main goal of this study was to find the best pipeline to train different classification models on the given blood cells dataset, highlighting pros and cons of each architecture, to select the best one for the specific task.

## Data
A dataset containing 13759 images of size 96x96x3 was provided. Each image pictured a blood cell and was labeled with one of the 8 possible classes: Basophil, Eosinophil, Erythroblast, Immaturegranulocytes, Lymphocyte, Monocyte, Neutrophil, Platelet.

## Methods
### Preprocessing
- CleanLab for data cleaning
- Train-val split
- Normalization
- Resize (depending on the network requirement)
- Augmentation (first start with few agumentation; then moved to strong augmentation (RandAugment, cutmix, mixup, ...))

### Network
Different network were created and their performance were compared:
- Basic CNN: 5 convolutional layer (serves as baseline)
- pretrained backbone on Imagenet (VGG16, Xceptionet, EfficientNetB7, SE-ResNet50, ConvNeXtBase) + classification head (GAP + dense layer)

### Training
- callback: early stopping, reduce on platoe
- loss: Categorical crossentropy + label smoothing(0.1)
- optimizer: AdamW
- class weights (to address class imbalance)

## Results
Basic augmentation gave pour results.
Increasing both the number and complexity of the augmentation the performance increased.
Performance obtained on the external test set using different networks can be seen in the following table:
|           | Accuracy  | 
|-----------|-----------|
| Basic CNN | 0.62      |
| VGG16     | 0.86      | 
| Xception  | 0.92      | 
| Efficientnet B7|0.88  |
| Se-ResNet50| 0.75     |
| ConvNeXtBase| 0.91    |

## Conclusion
This study explored CNN architectures for blood cell classification, achieving significant results with Xception, which reached 92% test accuracy. Key contributions include  effective data cleaning with Cleanlab, aggressive data augmentation (e.g., RandAugment, MixUp, CutMix), and a comprehensive evaluation of model performances. The findings
highlight that deeper models generally perform better but require careful tuning for task-specific data. Future work could focus on real-time augmentation during training, systematic hyperparameter tuning, testing hybrid or transformer-based models, and expanding the dataset to improve robustness. This research demonstrates the potential of deep learning for rapid and accurate blood cell classification.
