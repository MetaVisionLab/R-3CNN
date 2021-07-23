# R<sup>3</sup>CNN: Regression Guided by Relative Ranking Using Convolutional Neural Network for Facial Beauty Prediction

R<sup>3</sup>CNN is a general CNN architecture to integrate the relative ranking of faces in terms of aesthetics to improve the performance of facial beauty prediction.

## Requirements
* Caffe (compiled with pycaffe)
* python
* numpy
* matplotlib
* skimage

## Caffe Installation
+ Build caffe
`make all -j16
 make test
 make pycaffe`

+ Add the python directory of caffe into the environment variable
   + Open bash file:
      `sudo gedit ~/.bashrc`
   + Add the following setence into the file:
   `export PYTHONPATH=brl/caffe/python:$PYTHONPATH`
   + Update the environment variable:
   `source ~/.bashrc`
   
## Data Preparation
+ Dataset download: our method is trained and verified on the SCUT-FBP5500 benchmark [Download](     
https://github.com/HCIILAB/SCUT-FBP5500-Database-Release).The images of SCUT-FBP5500 should be packed and renamed as 'faces', and put under './examples/data', where train and test set have been already provided.

+ Image pairs generation: 
`cd examples/data/
python create_pair.py`

+ Mean file generation:
`sh mean.sh`
   
## Training
+ First stage: conventional training for ResNeXt model, using pretrained model on ImageNet (download link: https://pan.baidu.com/s/12AtCeQYuYDZtUd9jZPIo1w  password:enfc):
`cd examples/first_stage
 sh train.sh`
 
+ Second stage:
   + rename the caffemodel obtained in the first stage as the format of 'R2Net_hinge_iter_0.caffemodel' (download link: https://pan.baidu.com/s/1Dx3H108gCvJ71fcVg3BzjQ  password:p3jk) ;
   + put 'R2Net_hinge_iter_0.caffemodel' under 'examples/hinge_loss/snapshot/1';
   + use hinge loss to train  R<sup>3</sup>CNN:
   `cd examples/hinge_loss
    sh train.sh`
   + if using LSEP loss to train R<sup>3</sup>CNN, you can run the codes in './examples/lsep_loss'；
   + if using other backbone networks (i.e., AlexNet and ResNet-18) to train R<sup>3</sup>CNN, you can run the codes in './examples/other_networks';

## Cross Validation
+ Download the trained ResNeXt-based R<sup>3</sup>CNN caffemodel from the link: https://pan.baidu.com/s/1YVwKrBZS4kpNWHTRs-9qTA  password: xcx7 (1.6GB)
+ Run the testing file:
```
cd examples/test_inference
python test_forward.py 
```

## Citation
Please cite our paper:
```
@article{lin2019regression,
  title={Regression guided by relative ranking using convolutional neural network (R3CNN) for facial beauty prediction},
  author={Lin, Luojun and Liang, Lingyu and Jin, Lianwen},
  journal={IEEE Transactions on Affective Computing},
  year={2019},
  publisher={IEEE}
}
```

## Contact Us
For any questions, please feel free to contact Dr. Lin (linluojun2009@126.com) or Prof. Jin (eelwjin@scut.edu.cn).

## Copyright
This code is free to the academic community for research purpose only. For commercial purpose usage, please contact Prof. Lianwen Jin (eelwjin@scut.edu.cn).
