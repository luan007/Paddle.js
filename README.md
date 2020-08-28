
# Paddle.js-Ext dev fork

> 🙋Maintained by friends of Emerge


Changes:

### Better dev experience 

- Progressively fix & upgrade `examples` - from either UX  / technical perspective

- Misc fixes - `.gitignore` & so on.

### Model conversion & Demos

- (Planned) Add support for tf.js -> paddle.js model conversion tools & documentations

### More Models!

- (Planned) Add more converted models from various communities. 

---

# Original Paddle.js Readme

[中文版](./README_cn.md)

# Paddle.js

Paddle.js is an Web project for Baidu Paddle, which is an an open source deep learning framework designed to work on web browser. Load a pretrained paddle.js SavedModel or Paddle Hub module into the browser and run inference through Paddle.js. It could run on nearly every browser with WebGL support.

## Key Features

### Modular

Web project is built on Atom system which is a versatile framework to support GPGPU operation on WebGL. It is quite modular and could be used to make computation tasks faster by utilizing WebGL.

### High Performance

Web project could run TinyYolo model in less than 30ms on chrome. This is fast enough to run deep learning models in many realtime scenarios.

### Browser Coverage

* PC: Chrome, firefox
* Mac: Chrome, Safari
* Android: Baidu App , UC, Chrome and QQ Browser

### Supported operations

Currently Paddle.js only supports a limited set of Paddle Ops. See the full list. If your model uses unsupported ops, the Paddle.js script will fail and produce a list of the unsupported ops in your model. Please file issues to let us know what ops you need support with.

[Supported operations Pages](./src/factory/fshader/README.md)


## Loading and running in the browser

```bash

import {runner as Paddlejs} from 'paddlejs';

const paddlejs = new Paddlejs({
        modelPath: 'model/mobilenetv2', // model path
        fileCount: 4, // model data file count
        feedShape: {  // input shape
            fw: 256,
            fh: 256
        },
        fetchShape: [1, 1, 1920, 10],  // output shape
        fill: '#fff',   // fill color when resize image
        needBatch: true, // whether need to complete the shape to 4 dimension
        inputType: 'image' // whether is image or video
    });

// load paddlejs model and preheat
await paddlejs.loadModel();

// run model
await paddlejs.predict(img, postProcess);

function postProcee(data) {
    // data is predicted result
    console.log(data);
}

```

Please see feed documentation for details.

Please see fetch documentation for details.


## Run the converter script provided by the pip package:

The converter expects a Paddlejs SavedModel, Paddle Hub module, paddle.js JSON format for input.


## Web-friendly format

The conversion script above produces 2 types of files:

 - model.json (the dataflow graph and weight manifest file)
 - group1-shard\*of\* (collection of binary weight files)


## Preview Demo

Paddle.js has some pre-converted models to Paddle.js format .There are some demos in the following URL, open a browser page with the demo.

[Supported Demo Pages](./examples/README.md)


## Feedback and Community Support
- Online video tutorial [start video](https://www.bilibili.com/video/BV1gZ4y1H7UA?p=6)
- Questions, reports, and suggestions are welcome through Github Issues!
- Forum: Opinions and questions are welcome at our [PaddlePaddle Forum](https://ai.baidu.com/forum/topic/list/168)！
- QQ group chat: 696965088
