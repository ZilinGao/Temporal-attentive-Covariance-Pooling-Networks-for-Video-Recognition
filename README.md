# Temporal-attentive-Covariance-Pooling-Networks-for-Video-Recognition
This is an implementation of [TCPNet][PAPER].

[PAPER]: https://arxiv.com.xxxx

## Introduction

For video recognition task, a global representation summarizing the whole contents of the video snippets plays an important role for the final performance. However,
existing video architectures usually generate it by using a simple, global average pooling (GAP) method, which has limited ability to capture complex dynamics
of videos. For image recognition task, there exist evidences showing that covariance pooling has stronger representation ability than GAP. Unfortunately, such
plain covariance pooling used in image recognition is an orderless representative, which cannot model spatio-temporal structure inherent in videos. Therefore, this
paper proposes a Temporal-attentive Covariance Pooling (TCP), inserted at the end of deep architectures, to produce powerful video representations. Specifi-
cally, our TCP first develops a temporal attention module to adaptively calibrate spatio-temporal features for the succeeding covariance pooling, approximatively
producing attentive covariance representations. Then, a temporal covariance pooling performs temporal pooling of the attentive covariance representations to char-
acterize both intra-frame correlations and inter-frame cross-correlations of the calibrated features. As such, the proposed TCP can capture complex temporal
dynamics. Finally, a fast matrix power normalization is introduced to exploit geometry of covariance representations. Note that our TCP is model-agnostic and
can be flexibly integrated into any video architectures, resulting in TCPNet for effective video recognition. The extensive experiments on six benchmarks (e.g.,
Kinetics, Something-Something V1 and Charades) using various video architectures show our TCPNet is clearly superior to its counterparts, while having strong
generalization ability.

## Citation

```
@InProceedings{Gao_2021_TCP,
                author = {Zilin, Gao and Qilong, Wang and Bingbing, Zhang and Qinghua, Hu and Peihua, Li},
                title = {Temporal-attentive Covariance Pooling Networks for Video Recognition},
                booktitle = {arxiv preprint axXiv:2021.06xxx},
                year = {2021}
  }
  ```

  

  ## Model Zoom
  

#### Kinetics-400

  |Method | Backbone       | frames | 1 crop Acc (%) | 30 views Acc (%) | Model GoogleDrive | Model BaiduDisk | 
  |:-----:|:------:|:------:|:--------------------------:|:-------------:|:---------------:|:---:|
  |TCPNet |TSN R50  |   8f   |           72.4/90.4        |         75.3/91.8            | TODO | TODO | 
  |TCPNet |TEA R50  |   8f   |        73.9/91.6        |         76.8/92.9            | TODO |TODO | 
  |TCPNet |TSN R152  |   8f   |          75.7/92.2        |         78.3/93.7            |  TODO | TODO | 
  |TCPNet |TSN R50  |   16f   |          73.9/91.2        |         75.8/92.1           | TODO |TODO | 
  |TCPNet |TEA R50  |   16f   |           75.3/92.2        |             77.2/93.1            | TODO |TODO | 
  |TCPNet |TSN R152  |   16f   |          77.2/93.1        |         79.3/94.0            |   TODO |TODO | 

#### Mini-Kinetics-200  


  |Method | Backbone       | frames | 1 crop Acc (%) | 30 views Acc (%) | Model GoogleDrive | Model BaiduDisk | 
  |:-----:|:------:|:------:|:--------------------------:|:-------------:|:---------------:|:---:|
  |TCPNet |TSN R50  |   8f   |           78.7        |        80.7            | TODO | TODO | 


  ## Environments
  
  pytorch 1.0+
  
  ffmpeg

TensorboardX

tqdm

scikit-learn
  
matplotlib

  ## Dataset Preparation
  
   TODO

  ## StartUp
  1. download the pretrained model and put it in `pretrained_model/`
  2. execute the training script file 
      e.g.: `sh script/k400/train_tcp_tsn_r50.sh`
 3. execute the inference script file 
      e.g.: `sh script/k400/test_tcp_tsn_r50.sh`
  

  ## Acknowledgement

Our code is  mainly based on [TSM][1] using [pytorch][5] toolbox and adopt some parts from [iSQRT][2], [TEA][3] and [Non-local][4], [S3D][S3D]. Thanks for their work!
  
  [1]: https://github.com/mit-han-lab/temporal-shift-module
  [2]: https://github.com/jiangtaoxie/fast-MPN-COV
  [3]: https://github.com/Phoenix1327/tea-action-recognition
  [4]: https://github.com/facebookresearch/SlowFast
  [5]: https://pytorch.org
  
  
