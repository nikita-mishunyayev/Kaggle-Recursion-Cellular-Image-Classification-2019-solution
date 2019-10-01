## Kaggle Recursion Cellular Image Classification 2019

Our team ranked 83rd place (TOP 10%) in the [Recursion Cellular Image Classification 2019 on Kaggle platform](https://www.kaggle.com/c/recursion-cellular-image-classification/leaderboard). This repository consists of code and configs that we used to train our best models. The solution is powered by awesome [PyTorch](https://pytorch.org), [Ignite](https://github.com/pytorch/ignite), [Cadene models](https://github.com/Cadene/pretrained-models.pytorch), [EfficientNet](https://www.kaggle.com/chanhu/efficientnet) and [Albumentations](https://github.com/albu/albumentations) libraries.

## In this repository you can find:
* `models` - folder with our models (**EfficientNet-B2, EfficientNet-B5, DenseNet201, SeResNext101_32x4d**)
* `utils` - folder with helper scripts

## Solution description

### Models
From the beginning, efficientnet outperformed other models. Using allowed to use bigger batch size - speeded up training and inference. Other models (like ResNet, ResNext or Inception) worked worse for us.

Models used in the final submission:
1. EfficientNet-B5 (best single model): AMSoftmaxLoss(margin_type='cos'), RAdam, ExponentialLR, freezing all layers without last linear on 1 epoch
2. DenseNet201 (similar score with effnet-b5): AMSoftmaxLoss(margin_type='cos'), Adam, ExponentialLR, freezing all layers without last linear on 1 epoch
3. EfficientNet-B2: CrossEntropyLoss, Adam, ExponentialLR, without freezing
4. SeResNext101_32x4d: AMSoftmaxLoss(margin_type='cos'), RAdam, OneCycleLR, without freezing, fastai library

### Augmentations
From [Albumentations](https://github.com/albu/albumentations) library:
We tried Horizontalflip, VerticalFlip, RandomRotate90, ShiftScaleRotate, Cutout, RandomBrightnessContrast but models with augmentations were not included in the final solution.

### Training
First 3 models were trained using [Ignite](https://github.com/pytorch/ignite) library and the last one with [FastAi](https://github.com/fastai/fastai), all of them work on top of [PyTorch](https://pytorch.org).

Each model trained on 6 channel images using the entire dataset and them finetuning for each cell type. Adam/RAdam were used for training as optimizers and ExponentialLR/OneCycleLR as loss functions. 

### Hardware
We used 1x* *Tesla V40 (8gb)*, Kaggle Kernels, sometimes Gcloud SDK (8x* *Tesla v100 (16gb)* or 4x* *Tesla v4 (16gb) with fp16*)

## Team:
- Mishunyayev Nikita: [Kaggle](https://www.kaggle.com/mnikita), [GitHub](https://github.com/Mishunyayev-Nikita)
- Zack Pashkin: [Kaggle](https://www.kaggle.com/tienen), [GitHub](https://github.com/ZackPashkin)
- Alexander Romakhin: [Kaggle](https://www.kaggle.com/asromhain), [GitHub](https://github.com/asromahin)
