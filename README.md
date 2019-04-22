# Paramertic Noise Injection for Adversarial Defense
  
  
This repository contains a Pytorch implementation of our paper titled "[Parametric Noise Injection: Trainable Randomness to Improve Deep Neural Network Robustness against Adversarial Attack](./CVPR19_PNI.pdf )"
  
If you find this project useful to you, please cite [our work]( ):
  
```bibtex
@inproceedings{he2019PNI,
 title={Parametric Noise Injection: Trainable Randomness to Improve Deep Neural Network Robustness against Adversarial Attack},
 author={He, Zhezhi and Adnan Siraj Rakin and Fan, Deliang},
 booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
 pages={},
 year={2019}
}
```
  
## Table of Contents
  
  
- [Introduction](#Introduction ) 
- [Dependencies](#Dependencies )
- [Usage](#Usage )
- [Result](#Result )
- [Notes for Experiments setup](#Notes )
  
  
  
## Introduction:
  
  
## Dependencies:
  
  
  
* Python 3.6 (Anaconda)
* Pytorch 4.1
* TensorboardX 
  
## Set up A Conda python Environment
  
Anaconda allows you to have different environments installed on your computer to access different versions of `python` and different libraries. Sometimes, the conflict of library versions may causes errors and packages not working.
  
  
  
  
  
## Usage
  
Please modify the example bash code we provide for running the code.
  
- Number of epochs that delaying the adversarial training is controlled by `epoch_delay`, where the default setup is 5. You can disable it by setting `--epoch_delay 0` in the bash script.
  
- through enable `--adv_eval`, users can monitor the accuracy of perturbed test data (i.e., input image under attack) evolving with the adversarial training progress. For fast training, users can also choose to disable the evaluation, then only perfrom the evaluation with the model after adversarial traning.
  
  
## Result
  
Hereby, we choose the ResNet-20 on CIFAR-10 as a simple example. Besides the Layer-wise PNI we introduced in our paper, we also implement the PNI in channel-wise and element-wise fashion. 
  
|      | Clean data | PGD | FGSM |
|:----:|:---------:|:---------:|:---------:|
| vanilla adv. training |83.84%|39.14<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.05%|46.55%|    
| PNI-W (layer-wise) |84.89<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.11%|45.94<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.11%|54.48<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.44%| 
| PNI-W (channel-wise) |85.17<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.12%|48.40<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.37%|56.51<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.75%| 
| PNI-W (element-wise) |80.69<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.16%|49.07<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.41%|55.13<img src="https://latex.codecogs.com/gif.latex?&#x5C;pm"/>0.51%|   
  
  
## Notes for Experiments setup
  
  
1. Based on our experiments, since the PNI-W (i.e., Parametric Noise Injection on Weight) outperforms other PNI variants on activations and etc., we choose PNI-W as the default setup.
  
2. Previous works remove the normalization layer from the data-preprocessing. Since we still expect the fast convergence benefit from the normalization of input image, we add a normalization in front of the neural network which perform the identical functionality but with the normalization incoporated within the backward computation graph.
  
3. During the adversarial training, we take the prevention of label leaking into the consideration. Rather than directly use the groundtruth as the label to perform the adversarial attack, we take the network's output w.r.t the clean data (i.e., attack free) as the label.
  
  
  
  