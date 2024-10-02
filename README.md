# A Decade’s Battle on Dataset Bias: Are We There Yet ?

## Installation
Please check [INSTALL.md](INSTALL.md) for installation instructions. 

## Dataset Preparation

Download images from each dataset and organize them as follows:
```
/path/to/dataset/
  train/
    dataset1/
      ...
    dataset2/
      ...
    dataset3/
      ...
  val/
    dataset1/
      ...
    dataset2/
      ...
    dataset3/
      ...
```

## Training

### Basic Recipe
We list commands for training `convnext_tiny` on classifying three datasets, each of which contains 1M samples.
- For training other models, change `--model` accordingly, e.g., to `vit_small`, `resnet50`, `vgg16`, `alexnet`.
- Our results were produced with 4 nodes, each with 8 gpus. Below we give example commands on both multi-node and single-machine setups.

multi-node
```
python run_with_submitit.py --nodes 4 --ngpus 8 \
--model convnext_tiny \
--batch_size 128 --lr 1e-3 --opt_betas 0.9 0.95 \
--mixup 0.8 --cutmix 1.0 --mixup_mode elem \
--weight_decay 0.3 --reprob 0.0 --color_jitter 0 \
--data_path /path/to/data/ \
--output_dir /path/to/results/
```

single-machine
```
python -m torch.distributed.launch --nproc_per_node=8 main.py \
--model convnext_tiny --update_freq 4 \
--batch_size 128 --lr 1e-3 --opt_betas 0.9 0.95 \
--mixup 0.8 --cutmix 1.0 --mixup_mode elem \
--weight_decay 0.3 --reprob 0.0 --color_jitter 0 \
--data_path /path/to/data/ \
--output_dir /path/to/results/
```

### Evaluation

single-GPU
```
python main.py --model convnext_tiny --eval true \
--resume /path/to/model \
--data_path /path/to/data
```

multi-GPU
```
python -m torch.distributed.launch --nproc_per_node=8 main.py \
--model convnext_tiny --eval true \
--resume /path/to/model \
--data_path /path/to/data
```


## Acknowledgement
This repository is built using the [timm](https://github.com/rwightman/pytorch-image-models) library and [ConvNeXt](https://github.com/facebookresearch/ConvNeXt) codebase.
