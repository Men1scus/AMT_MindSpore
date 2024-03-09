# $\rm{[MindSpore-phase3]}$ $AMT$

本项目包含了以下论文的mindspore实现：

> **AMT: All-Pairs Multi-Field Transforms for Efficient Frame Interpolation**<br>
> [Zhen Li](https://paper99.github.io/)<sup>\*</sup>, [Zuo-Liang Zhu](https://nk-cs-zzl.github.io/)<sup>\*</sup>, [Ling-Hao Han](https://scholar.google.com/citations?user=0ooNdgUAAAAJ&hl=en), [Qibin Hou](https://scholar.google.com/citations?hl=en&user=fF8OFV8AAAAJ&view_op=list_works), [Chun-Le Guo](https://scholar.google.com/citations?hl=en&user=RZLYwR0AAAAJ),  [Ming-Ming Cheng](https://mmcheng.net/cmm)<br>
> (\* denotes equal contribution) <br>
> Nankai University <br>
> IEEE/CVF Conference on Computer Vision and Pattern Recognition (**CVPR**), 2023<br>

[[Paper](https://arxiv.org/abs/2304.09790)] [[Project Page](https://nk-cs-zzl.github.io/projects/amt/index.html)]   [[Web demos](#web-demos)]

文章官方版本仓库链接: [MCG-NKU/AMT: Official code for "AMT: All-Pairs Multi-Field Transforms for Efficient Frame Interpolation" (CVPR2023) (github.com)](https://github.com/MCG-NKU/AMT)

目前已经完成推理部分以及训练部分大部分代码的mindspore转化

## 正在进行中的工作

-  完整代码的mindspore实现

## Dependencies and Installation
>python 3.8 <br>
>cuda: 11.6 <br>
>mindspore: 2.2.11 

1. Clone Repo

   ```bash
   git clone https://github.com/Men1scus/AMT_MindSpore.git
   ```

2. Create Conda Environment and Install Dependencies

   ```bash
   conda env create -f environment.yaml
   conda activate amt
   pip install https://ms-release.obs.cn-north-4.myhuaweicloud.com/2.2.11/MindSpore/unified/x86_64/mindspore-2.2.11-cp38-cp38-linux_x86_64.whl --trusted-host ms-release.obs.cn-north-4.myhuaweicloud.com -i https://pypi.tuna.tsinghua.edu.cn/simple
   ```
3. Download pretrained models for demos from [Pretrained Models](#pretrained-models) and place them to the `pretrained` folder

## Quick Demo

**Note that the selected pretrained model (`[CKPT_PATH]`) needs to match the config file (`[CFG]`).**

 > Creating a video demo, increasing $n$ will slow down the motion in the video. (With $m$ input frames, `[N_ITER]` $=n$ corresponds to $2^n\times (m-1)+1$ output frames.)


 ```bash
 python demos/demo_2x.py -c [CFG] -p [CKPT] -n [N_ITER] -i [INPUT] -o [OUT_PATH] -r [FRAME_RATE]
 # e.g. [INPUT]
 # -i could be a video / a regular expression / a folder contains multiple images
 # -i demo.mp4 (video)/img_*.png (regular expression)/img0.png img1.png (images)/demo_input (folder)

 # e.g. a simple usage
 python demos/demo_2x.py -c cfgs/AMT-S.yaml -p pretrained/amt-s.ckpt -n 6 -i assets/quick_demo/img0.png assets/quick_demo/img1.png

 ```

 + Note: Please enable `--save_images` for saving the output images (Save speed will be slowed down if there are too many output images)
 + Input type supported: `a video` / `a regular expression` / `multiple images` / `a folder containing input frames`.
 + Results are in the `[OUT_PATH]` (default is `results/2x`) folder.