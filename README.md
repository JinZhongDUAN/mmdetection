# mmdetection0.5.7
mmdetection for ReasoningRCNN
对官方mmetection0.5.7进行了一些修改使其能够用于Reasoning-RCNN《Reasoning-RCNN Unifying Adaptive Global Reasoning into Large-scale Object Detection》
# 安装
1：创建conda虚拟环境，安装所需要的库，包括mmcv，pytorch，torchvision等并激活环境（先安装mmcv后安装mmdetection）

2：git clone https://github.com/Jinzhong-Duan/mmdetection.git

3：cd mmdetection

4：onda install cython #pip install cython

5：./compile.sh

6：python setup.py install #pip install .

#测试代码
预训练模型需要自己下载
```import mmcv
from mmcv.runner import load_checkpoint
from mmdet.models import build_detector
from mmdet.apis import inference_detector, show_result
 
cfg = mmcv.Config.fromfile('/home/stardust/mmdetection/configs/faster_rcnn_r50_fpn_1x.py')
cfg.model.pretrained = None
 
# 构建网络，载入模型
model = build_detector(cfg.model, test_cfg=cfg.test_cfg)
 
# _ = load_checkpoint(model, 'https://s3.ap-northeast-2.amazonaws.com/open-mmlab/mmdetection/models/faster_rcnn_r50_fpn_1x_20181010-3d1b3351.pth')
# 如果通过网盘下载，取消下一行代码的注释，并且注释掉上一行
_ = load_checkpoint(model, 'model/faster_rcnn_r50_fpn_1x_20181010-3d1b3351.pth')
 
# 测试一张图片
img = mmcv.imread('test.jpg')
result = inference_detector(model, img, cfg)
show_result(img, result)
 
# 测试多张图片
# imgs = ['test1.jpg', 'test2.jpg']
# for i, result in enumerate(inference_detector(model, imgs, cfg, device='cuda:0')):
#     print(i, imgs[i])
#     show_result(imgs[i], result)
```
