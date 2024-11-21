# SmallBambooCode 修改版 为了更加方便的训练&测试
- 增加了测试日志保存
- 修改了部分数据集文件的默认地址
- 增加shell脚本以更方便的训练&测试模型

## ConvLSR-Net
This is the code for our paper:

* [LSRFormer: Efficient Transformer Supply Convolutional Neural Networks with Global Information for Aerial Image Segmentation](https://ieeexplore.ieee.org/document/10438484) in IEEE Transactions on Geoscience and Remote Sensing 2024.

  
## Results

We repeated the experiment with 5 different random seeds. The average and best results of the 5 repetitions are as follows:

|    Method     |  Dataset  |  mIoU (Average) | mIoU (Best) |
|:-------------:|:---------:|:-----:|:-----:|
|  ConvLSR-Net   |   iSAID   |  70.8±0.11  | 70.89 |
|  ConvLSR-Net   | Vaihingen |  84.56±0.06 | 84.64 |
|  ConvLSR-Net   |  Potsdam  |  87.80±0.08 | 87.91 |
|  ConvLSR-Net   |  LoveDA   |  54.77±0.08 | [54.86](https://codalab.lisn.upsaclay.fr/my/competition/submission/340641/detailed_results)|

Due to some random operations in the training stage, reproduced results (run once) may slightly different from the reported in paper.


## Data Preprocessing

Please follw the [GeoSeg](https://github.com/WangLibo1995/GeoSeg) to preprocess the LoveDA, Potsdam and Vaihingen dataset.

Please follow the [mmsegmentation](https://github.com/open-mmlab/mmsegmentation/blob/main/docs/en/user_guides/2_dataset_prepare.md#isaid) to preprocess the iSAID dataset. 



## Training

"-c" means the path of the config, use different **config** to train different models.

```shell
python train_supervision.py -c ./config/isaid/convlsrnet.py
```

```shell
python train_supervision_dp.py -c ./config/potsdam/convlsrnet.py
```

```shell
python train_supervision_dp.py -c ./config/vaihingen/convlsrnet.py
```

```shell
python train_supervision_dp.py -c ./config/loveda/convlsrnet.py
```

## Testing

**iSAID** 
```shell
python test_isaid.py -c ./config/isaid/convlsrnet.py -o ./fig_results/isaid/convlsrnet_isaid/  -t "d4"
```

**Vaihingen**
```shell
python test_vaihingen.py -c ./config/vaihingen/convlsrnet.py -o ./fig_results/convlsrnet_vaihingen/ --rgb -t "d4"
```

**Potsdam**
```shell
python test_potsdam.py -c ./config/potsdam/convlsrnet.py -o ./fig_results/convlsrnet_potsdam/ --rgb -t "d4"
```

**LoveDA** ([Online Testing](https://codalab.lisn.upsaclay.fr/competitions/421))

My LoveDA results: [LoveDA Test Results](https://codalab.lisn.upsaclay.fr/my/competition/submission/340641/detailed_results/)

```shell
# 输出RGB图像（线下测试，直接输出mIOU）
python test_loveda.py -c ./config/loveda/convlsrnet.py -o ./fig_results/convlsrnet_loveda_rgb --rgb --val -t "d4"
```
```shell
# 输出标签图像（在线测试）
python test_loveda.py -c ./config/loveda/convlsrnet.py -o ./fig_results/convlsrnet_loveda_onlinetest -t "d4"
```


## Citation and Contact

If you find this project useful in your research, please consider citing our papers：

* R. Zhang, Q. Zhang and G. Zhang, "LSRFormer: Efficient Transformer Supply Convolutional Neural Networks With Global Information for Aerial Image Segmentation," in IEEE Transactions on Geoscience and Remote Sensing, vol. 62, pp. 1-13, 2024, Art no. 5610713, doi: 10.1109/TGRS.2024.3366709.


```shell
@ARTICLE{10438484,
  author={Zhang, Renhe and Zhang, Qian and Zhang, Guixu},
  journal={IEEE Transactions on Geoscience and Remote Sensing}, 
  title={LSRFormer: Efficient Transformer Supply Convolutional Neural Networks With Global Information for Aerial Image Segmentation}, 
  year={2024},
  volume={62},
  number={},
  pages={1-13},
  doi={10.1109/TGRS.2024.3366709}}
```

If you encounter any problems while running the code, feel free to contact me via [stdcoutzrh@gmail.com](stdcoutzrh@gmail.com). Thank you!


## Acknowledgement

Our training scripts comes from [GeoSeg](https://github.com/WangLibo1995/GeoSeg). Thanks for the author's open-sourcing code.
- [GeoSeg(UNetFormer)](https://github.com/WangLibo1995/GeoSeg)
- [pytorch lightning](https://www.pytorchlightning.ai/)
- [timm](https://github.com/rwightman/pytorch-image-models)
- [pytorch-toolbelt](https://github.com/BloodAxe/pytorch-toolbelt)
- [ttach](https://github.com/qubvel/ttach)
- [catalyst](https://github.com/catalyst-team/catalyst)
- [mmsegmentation](https://github.com/open-mmlab/mmsegmentation)
