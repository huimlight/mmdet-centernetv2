## Introduction

This project is trying to Recreate CenternetV2 based on MMDET, which is proposed in paper [Probabilistic two-stage detection](https://arxiv.org/pdf/2103.07461.pdf). 

This project is also for the contest [OpenMMLab Algorithm Ecological Challenge](https://openmmlab.com/competitions/algorithm-2021).

This is NOT the official implementation.

Quick peek at the result:

> **The paper:** centernet2(CascadeRCNN-CenterNet w. prob.) mAP is 42.9.
>
> **This implementation:** we implement centernet2(CascadeRCNN-CenterNet w. prob.) mAP is 43.2.
> 
> **Note:** We will continue to maintain the code with trick.
> 
> **Note:** We always reproduce the weights, which Verification and inference part.

## Implementation

**Code:** we add detector in mmdet/models/detectors/centernetv2.py.

**Code:** we add config in configs/centernetv2/centernet2.py.

**Code:** we add centernet_head in mmdet/dense_heads/centernet_headv2.py.

**Code:** we add hm_binary_focal_loss in mmdet/losses/hm_binary_focal_loss.py.

**Code:** we modify mmdet/roi_heads/cascade_roi_head.py, add the super parameter add_agnostic_score to Control whether the first stage score.This hyperparameter does not affect the use of other configuration files

**Code:** we modify mmdet/bbox_head/bbox_head.py, add the super parameter add_agnostic_score to Control Whether to use softmax.This hyperparameter does not affect the use of other configuration files

## Experiments

**MMDetection:** this project is based on version v2.15.0.

**MMCV:** version v1.3.5

**Dataset:** coco_train_2017(117k) as training dataset and coco_val_2017(5k) as testing dataset. All the results are reported on coco_val_2017.

Results reported in the paper:

|                              | AP      | AP50   | AP75   | APs    | APm    | APl    |
| ---------------------------- | ------- | ------ | ------ | ------ | ------ | ------ |
| cascadeRCNN-CenterNet w.prob | 42.862  | 59.519 | 47.028 | 24.064 | 47.043 | 56.197 |


Results by this implementation:

|                              | AP     | AP50  | AP75   | APs    | APm    | APl    |
| ---------------------------- | ------ | ----- | ------ | ------ | ------ | ------ |
| cascadeRCNN-CenterNet w.prob | 43.2   | 60.6  | 47.9   | 25.3   | 46.6   | 56.2   |


Log and model:

|                      | backbone | Iter | bbox AP | Config                                                       | Log                                                          | Model                                                        | GPUs |
| -------------------- | -------- | ------- | ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| cascadeRCNN-CenterNet w.prob | R-50-FPN | 90000     | 43.2    | [config](https://github.com/huimlight/mmdet-centernetv2/blob/main/centernet2_res50_rpn_90k_coco.py) | [log](https://github.com/huimlight/mmdet-centernetv2/blob/main/20210814_232645.log) | [baidu ](https://pan.baidu.com/s/1fh39a9xxeurFVy57klql6A) [jip5] | single-v100(batch=20)    |



## Usage

You can train and inference the model like any other models in MMDetection, see [docs](https://mmdetection.readthedocs.io/) for details.

conda create -n centernetv2 python=3.7 -y

conda install pytorch cudatoolkit=10.1 torchvision -c pytorch

pip install mmcv-full

git clone https://github.com/yyz561/mmdetection

pip install -r requirements/build.txt

pip install -v -e .  # or "python setup.py develop"




## Acknowledgement

[Probabilistic two-stage detection](https://arxiv.org/pdf/2103.07461.pdf)

[MMDetection](https://github.com/open-mmlab/mmdetection)

[MMCV](https://github.com/open-mmlab/mmcv)
