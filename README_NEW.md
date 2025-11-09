# 环境配置
vggt-long

~~~
conda create -n vggt-long python=3.10
conda activate vggt-long
conda install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia 
# 注意这个完善过
pip install -r requirements.txt
bash ./scripts/download_weights.sh

# 以下代码可以加速sim3优化
python setup.py install
~~~

## 运行方法
由于TUM图像太多，这里加了个图像采样逻辑，需要在configs/base_config.yaml中修改
  sample_rate: 30
然后
~~~
CUDA_VISIBLE_DEVICES=3 python vggt_long_sample.py --image_dir /share/datasets/TUM/Dynamics/rgbd_dataset_freiburg2_desk_with_person/rgb 
~~~
会保存点云到
exps/_share_datasets_TUM_Dynamics_rgbd_dataset_freiburg2_desk_with_person_rgb/2025-11-09-17-17-48/pcd/combined_pcd.ply
vggt-long必须有回环才能运行，没有回环点云为空