# SOLO: Segmenting Objects by Locations（SOLO and SOLO V2）
## 用法

### A quick demo

安装完成后，下载训练好的models（在英文版readme.md），然后运行 [inference_demo.py](demo/inference_demo.py) to run a quick demo.

###  多显卡
    #  multiple GPUs trainng
    ./tools/dist_train.sh ${CONFIG_FILE} ${GPU_NUM}

    Example: 
    ./tools/dist_train.sh configs/solo/solo_r50_fpn_8gpu_1x.py  8

    # multi-gpu testing
    ./tools/dist_test.sh ${CONFIG_FILE} ${CHECKPOINT_FILE} ${GPU_NUM}  --show --out  ${OUTPUT_FILE} --eval segm
    
    Example: 
    ./tools/dist_test.sh configs/solo/solo_r50_fpn_8gpu_1x.py SOLO_R50_1x.pth  8  --show --out results_solo.pkl --eval segm

###  单显卡
    #  single GPU training
    python tools/train.py ${CONFIG_FILE}
    
    Example:
    python tools/train.py configs/solo/solo_r50_fpn_8gpu_1x.py

    ## single-gpu testing
    python tools/test_ins.py ${CONFIG_FILE} ${CHECKPOINT_FILE} --show --out  ${OUTPUT_FILE} --eval segm
    
    Example: 
    python tools/test_ins.py configs/solo/solo_r50_fpn_8gpu_1x.py  SOLO_R50_1x.pth --show --out  results_solo.pkl --eval segm


### Visualization

    python tools/test_ins_vis.py ${CONFIG_FILE} ${CHECKPOINT_FILE} --show --save_dir  ${SAVE_DIR}
    
    Example: 
    python tools/test_ins_vis.py configs/solo/solo_r50_fpn_8gpu_1x.py  SOLO_R50_1x.pth --show --save_dir  work_dirs/vis_solo


## 安装
安装以下包
- Linux (只支持linux)
- Python 3.5+
- PyTorch 1.1 or higher
- CUDA 9.0 or higher
- NCCL 2
- GCC 4.9 or higher
- [mmcv 0.2.16](https://github.com/open-mmlab/mmcv/tree/v0.2.16)

我用的：
- Python 3.6
- PyTorch 1.4
- CUDA 10.1
- mmcv 0.2.16
### 具体操作：
- 安装新环境
```shell
conda create -n solo python=3.6
conda activate solo
```
- 安装cudatoolkit和cudnn
```shell
conda install cudatoolkit=10.1 cudnn
```
- 安装PyTorch 和 torchvision
```shell
conda install pytorch=1.4 torchvision
```
- mmcv 0.2.16
```shell
pip install mmcv==0.2.16
```
- 安装SOLO包
```shell
git clone https://github.com/WXinlong/SOLO.git
cd SOLO
pip install -r requirements/build.txt
# 安装pycocotools（如果装不上就下下来，cd到PythonAPI文件夹，pip install setup.py）
pip install "git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI"
# 安装SOLO，倒腾完了
pip install -v -e .  # or "python setup.py develop"
```
SOLO以dev模式安装，对代码所做的任何本地修改都将生效，无需重新安装（除非您提交了一些提交并希望更新版本号）。

### 准备数据集
建议将数据集根目录符号链接到“$SOLO/data”。
如果文件夹结构不同，需要更改配置文件中相应的路径。
```
SOLO
├── mmdet
├── tools
├── configs
├── data
│   ├── coco
│   │   ├── annotations
│   │   ├── train2017
│   │   ├── val2017
│   │   ├── test2017
│   ├── cityscapes
│   │   ├── annotations
│   │   ├── train
│   │   ├── val
│   ├── VOCdevkit
│   │   ├── VOC2007
│   │   ├── VOC2012

```

## License

For academic use, this project is licensed under the 2-clause BSD License - see the LICENSE file for details. For commercial use, please contact [Xinlong Wang](https://www.xloong.wang/) and  [Chunhua Shen](https://cs.adelaide.edu.au/~chhshen/).


