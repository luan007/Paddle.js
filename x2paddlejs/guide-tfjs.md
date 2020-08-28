# Converting [Tensorflow](https://tfhub.dev/) to Paddle.js


## convert tfjs to pb using tfjs-graph-converter[Github](https://pypi.org/project/tfjs-graph-converter/)

![](https://raw.githubusercontent.com/patlevin/tfjs-to-tf/master/docs/logo.png)


```shell
pip3 install --upgrade virtualenv==16.7.9
mkdir vv
cd vv
virtualenv --no-site-packages venv
. venv/bin/activate
pip install tensorflowjs
pip install tfjs-graph-converter

pip uninstall tensorflow-estimator
pip uninstall tensorflow-cpu 
pip install tensorflow-cpu==1.15.0 
```

* rename `modelxxx.json` -> `model.json`
```
tfjs_graph_converter ./resnet/ ./out.pb
```

## convert pb to model

* install tensorflow
```
mkdir pb
cd pd
virtualenv --no-site-packages venv
. venv/bin/activate
pip install termcolor
pip install tensorflow==1.14.0
```

* install X2Paddle [Github](https://github.com/PaddlePaddle/X2Paddle)
```
pip install paddlepaddle
git clone https://github.com/PaddlePaddle/X2Paddle.git
cd X2Paddle
git checkout develop
python setup.py install
```

* run X2Paddle / maybe need input shape [Github](https://github.com/PaddlePaddle/X2Paddle/blob/develop/tools/README.md)
```shell
X2Paddle -f tensorflow -m ./out.pb  -s ./out_model --without_data_format_optimization=False
python tools/merge_params.py ./out_model/inference_model ./out_model/new_model_dir
```

* add command `tools/check_for_lite.py` (python >= 2.79)
```
import ssl
ssl._create_default_https_context = ssl._create_unverified_context
```

* check op support PaddleLite
`python tools/check_for_lite.py ./out_model/inference_model/__model__`


## convert out_model to paddle model

```
cd Paddle.js/tools/ModelConverter
python3 convertToPaddleJSModel.py --modelPath="./out_model/new_model_dir/__model__" --paramPath="./out_model/new_model_dir/__params__" --outputDir="./model-out"
```

* move `model-out` -> `dist/model/model-out`

