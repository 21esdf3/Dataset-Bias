# Installation

We provide installation instructions for dataset classification experiments here.

## Dependency Setup
Create an new conda virtual environment
```
conda create -n bias python=3.8 -y
conda activate bias
```

Install [Pytorch](https://pytorch.org/)>=1.13.1, [torchvision](https://pytorch.org/vision/stable/index.html)>=0.14.1 following official instructions. For example:
```
pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 --extra-index-url https://download.pytorch.org/whl/cu117
```

Clone this repo and install required packages:
```
pip install timm==0.6.12 tensorboardX six numpy==1.23.1
```

The results in the paper are produced with `torch==1.13.1+cu117 torchvision==0.14.1+cu117 timm==0.6.12`.
