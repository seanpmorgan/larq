# Larq Zoo Pretrained Models

Larq Zoo provides reference implementations of deep neural networks with extremely low precision weights and activations that are made available alongside pre-trained weights.
These models can be used for prediction, feature extraction, and fine-tuning.

We believe that a collection of tested implementations with pretrained weights is greatly beneficial for the field of Extremely Quantized Neural Networks. To improve reproducibility we have implemented a few commonly used models found in the literature. If you have developed or reimplemented a Binarized or other Extremely Quantized Neural Network and want to share it with the community such that future papers can build on top of your work, please add it to Larq Zoo or get in touch with us if you need any help.

## Available models

The following models are trained on the [ImageNet](http://image-net.org/) dataset. The Top-1 and Top-5 accuracy refers to the model's performance on the ImageNet validation dataset, memory refers to the memory after quantization of the weights.

The model definitions and the train loop are available in the [Larq Zoo repository](https://github.com/larq/zoo).

| Model                                          | Top-1 Accuracy | Top-5 Accuracy | Parameters | Memory   |
| ---------------------------------------------- | -------------- | -------------- | ---------- | -------- |
| [Bi-Real Net](/api/larq_zoo/#birealnet)        | 58.01 %        | 80.27 %        | 11 736 232 | 4.04 MB  |
| [XNOR-Net](/api/larq_zoo/#xnornet)             | 44.96 %        | 69.18 %        | 62 396 768 | 22.81 MB |
| [Binary AlexNet](/api/larq_zoo/#binaryalexnet) | 36.30 %        | 61.53 %        | 61 859 192 | 7.49 MB  |

## Training Models from Scratch

Larq Zoo ships with a command line interface powered by [`zookeeper`](https://github.com/larq/zookeeper/), allowing you to reproduce the entire training process. If you want to improve an existing model or implement your own, we recommend to install Larq Zoo in [development mode](https://github.com/larq/zoo/blob/master/CONTRIBUTING.md#project-setup).

E.g. to reproduce the training of [Binary AlexNet](/models/api/#binaryalexnet) run:

```shell
lqz train binary_alexnet --dataset imagenet2012 --dataset-version 5.0.0
```

To experiment with different hyperparameters you can either edit the [`HParams` for this model](https://github.com/larq/zoo/blob/master/larq_zoo/binarynet.py#L72-L85) or overwrite them from the command line, e.g.:

```shell
lqz train binary_alexnet --dataset imagenet2012 --dataset-version 5.0.0 --hparams epochs=150,batch_size=256
```

To view a TensorBoard for the current training, replace the `lqz train` command with `lqz tensorboard`.

For all available commands and options run `lqz --help` or `lqz train --help` or checkout the documentation of [`zookeeper`](https://github.com/larq/zookeeper/) if you want to implement your own model for Larq Zoo.

## Installation

Larq Zoo is not included in Larq by default. To start using it, you can install it with Python's [pip](https://pip.pypa.io/en/stable/) package manager:

```shell
pip install larq-zoo
```

Weights can be downloaded automatically when instantiating a model. They are stored at `~/.larq/models/`.