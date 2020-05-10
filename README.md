# Fast-AutoAug-Torch

Search for [Fast AutoAugment](https://arxiv.org/abs/1905.00397) using [AutoTorch](http://autotorch.org/). 

| model | augment| epoch | Acc |
|-------|--------|-------|-----|
|ResNet-50| baseline | 120 | 76.48 |
|ResNet-50| baseline | 270| 77.17 |
|ResNet-50| Rand AA | 270| |
|ResNet-50| Fast AA | 270| **77.73** |

## Quick Start
### Prepare dataset

```bash
# assuming you have downloaded the dataset in the current folder
python prepare_imagenet.py --download-dir ./
```

### Search policy
```bash
python search_policy.py --reduced-size 60000 --epochs 120 --nfolds 8 --num-trials 200  --save-policy imagenet_policy.at
```

[An example learned policy](./imagenet_policy.md)

### Train with searched policy

```bash
python train.py --dataset imagenet --model resnet50 --lr-scheduler cos --epochs 270 --checkname resnet50_fast_aa --lr 0.025 --batch-size 64 --auto-policy imagenet_policy.at
```

### Train with random AA
```bash
python train.py --dataset imagenet --model resnet50 --lr-scheduler cos --epochs 270 --checkname resnet50_rand_aug --lr 0.025 --batch-size 64 --rand-aug
```
