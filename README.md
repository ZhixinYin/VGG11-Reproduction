
# VGG Paper Reproduction (2015)

## Introduction
This project reproduces the original VGG11 architecture as described in the paper, which will later be used as parameter initilisation for other VGG networks.

## Architecture Summary
| Stage          | Layer Type         | Filters / Units | Kernel / Stride | Output Size     |
| -------------- | ------------------ | --------------- | --------------- | --------------- |
| Input          | Input              | –               | –               | 224 × 224 × 3   |
| **Block 1**    | Conv2D + BN + ReLU | 64              | 3×3 / 1         | 224 × 224 × 64  |
|                | MaxPool            | –               | 2×2 / 2         | 112 × 112 × 64  |
| **Block 2**    | Conv2D + BN + ReLU | 128             | 3×3 / 1         | 112 × 112 × 128 |
|                | MaxPool            | –               | 2×2 / 2         | 56 × 56 × 128   |
| **Block 3**    | Conv2D + BN + ReLU | 256             | 3×3 / 1         | 56 × 56 × 256   |
|                | Conv2D + BN + ReLU | 256             | 3×3 / 1         | 56 × 56 × 256   |
|                | MaxPool            | –               | 2×2 / 2         | 28 × 28 × 256   |
| **Block 4**    | Conv2D + BN + ReLU | 512             | 3×3 / 1         | 28 × 28 × 512   |
|                | Conv2D + BN + ReLU | 512             | 3×3 / 1         | 28 × 28 × 512   |
|                | MaxPool            | –               | 2×2 / 2         | 14 × 14 × 512   |
| **Block 5**    | Conv2D + BN + ReLU | 512             | 3×3 / 1         | 14 × 14 × 512   |
|                | Conv2D + BN + ReLU | 512             | 3×3 / 1         | 14 × 14 × 512   |
|                | MaxPool            | –               | 2×2 / 2         | 7 × 7 × 512     |
| **Classifier** | Flatten            | –               | –               | 25,088          |
|                | Dense + ReLU       | 4096            | –               | 4096            |
|                | Dropout            | p = 0.3         | –               | 4096            |
|                | Dense + ReLU       | 4096            | –               | 4096            |
|                | Dropout            | p = 0.3         | –               | 4096            |
| Output         | Dense (Logits)     | 200             | –               | 200             |



## Dataset
tiny-imagenet-200 is used as the dataset in this reproduction. Validation set is used as test set, as the actual test set is not labelled. Images are resized from 64×64 to 224×224.

## Reproduced Results
| Metric            | Value |
| ----------------- | ----- |
| Training accuracy | 98.89% |
| Test accuracy     | 42.88% |

The difference between training accuracy and
test accuracy is expected, as the training examples are few compared to the number of parameters in VGG11, which helps VGG11 memorise the training data set, instead of finding the patterns. For reducing overfitting in the future, some preprocessing techniques like PCA, crop, horizontal flipping and so on should be utilised.

## References
Simonyan, K., & Zisserman, A. (2015). Very deep convolutional networks for large-scale image recognition. International Conference on Learning Representations (ICLR). https://arxiv.org/abs/1409.1556

Tiny ImageNet Dataset
Wu, J., Zhang, J., Xie, Y., & others. (2017).
Tiny ImageNet Visual Recognition Challenge.
Stanford University.
https://tiny-imagenet.herokuapp.com/
