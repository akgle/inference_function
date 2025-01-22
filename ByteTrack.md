克隆官方源文件：
!git clone https://github.com/ifzhang/ByteTrack.git
进入官方文件：
cd ByteTrack/
安装依赖:
!pip3 install -r requirements.txt
将该库安装到本地，并处于开发者模式，方便更改文件就能修改安装的库：
!python3 setup.py develop
安装其他包：
!pip3 install cython; pip3 install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
!pip3 install cython_bbox
继续安装缺少的文件：
!pip3 install loguru==0.7.0
!pip install thop
!pip install lap
!pip3 install filterpy motmetrics
创建一个pretrained的文件夹：
!mkdir -p pretrained
下载yolox的权重：
!wget https://github.com/Megvii-BaseDetection/YOLOX/releases/download/0.1.1rc0/yolox_x.pth -O pretrained/yolox_x.pth

由于numpy版本不行，所以需要将/content/ByteTrack/yolox/tracker/matching.py文件下面np.float 替换为 float 或 np.float64还有tracker.py文件里面的np

exps/example/mot/yolox_x_mix_det.py中，检查 num_classes需要改为80，因为yolox用的是coco数据集

运行推理：
!python tools/demo_track.py video \
    --path /content/test2.mp4 \
    --fps 30 \
    --save_result \
    --device gpu \
    --exp_file exps/example/mot/yolox_x_mix_det.py \
    --ckpt pretrained/yolox_x.pth