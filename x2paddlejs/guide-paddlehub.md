
# Converting From [PaddleHub](https://github.com/PaddlePaddle/PaddleHub) to Paddle.js

![](https://github.com/PaddlePaddle/PaddleHub/blob/release/v1.8/docs/imgs/paddlehub_logo.jpg)

## install [PaddleHub](https://github.com/PaddlePaddle/PaddleHub/blob/release/v1.8/docs/installation.md) ([control.md](https://github.com/PaddlePaddle/PaddleHub/blob/release/v1.8/docs/tutorial/cmdintro.md))

```
python3 -m pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
pip install paddlehub
hub install human_pose_estimation_resnet50_mpii
cd ~/.paddlehub
cd modules
open .
cp -R ~/.paddlehub/modules/human_pose_estimation_resnet50_mpii/pose-resnet50-mpii-384x384 ./{target}
```

## convert out_model to paddlejs model

```
cd Paddle.js/tools/ModelConverter
python3 convertToPaddleJSModel.py --inputDir="./out_model/new_model_dir" --outputDir="./model-out"
```
