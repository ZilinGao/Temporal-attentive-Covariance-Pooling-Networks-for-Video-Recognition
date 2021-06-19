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
  |TCPNet |TSN R50  |   8f   |           72.4/90.4  |         75.3/91.8          | [link][TCP_TSN8f_google] |[link][TCP_TSN8f_baidu] extract code:  8bqf| 
  |TCPNet |TEA R50  |   8f   |        73.9/91.6     |         76.8/92.9            | [link][TCP_TEA8f_google] |[link][TCP_TEA8f_baidu] extrace code: qn1k| 
  |TCPNet |TSN R152  |   8f   |          75.7/92.2  |         78.3/93.7          | [link][TCP_R1528f_google] |[link][TCP_R1528f_baidu] extract code: f6e5| 
  |TCPNet |TSN R50  |   16f   |          73.9/91.2  |         75.8/92.1          | [link][TCP_TSN16f_google] |[link][TCP_TSN16f_baidu] extract code: wjop| 
  |TCPNet |TEA R50  |   16f   |           75.3/92.2 |             77.2/93.1      | [link][TCP_TEA16f_google] |[link][TCP_TEA16f_baidu] extract code: budr| 
  |TCPNet |TSN R152  |   16f   |          77.2/93.1 |         79.3/94.0        | [link][TCP_R15216f_google] |[link][TCP_R15216f_baidu] extract code: 89rs|
   
   
   [TCP_TSN8f_google]: https://drive.google.com/file/d/1p05CaIv50Y2hzELFD4tXYYCZXizjkKAr/view?usp=sharing
   [TCP_TSN16f_google]: https://drive.google.com/file/d/1tCg-1JiM8l0_lC_YCyBqeVY_BohiQ3PS/view?usp=sharing
   
   [TCP_TSN8f_baidu]: https://pan.baidu.com/s/1mXx3c0PWMB0rRerDK9wkBg
   [TCP_TSN16f_baidu]: https://pan.baidu.com/s/1ocj0-3V0HWbKwZm0nCHonQ
   
   [TCP_TEA8f_google]: https://drive.google.com/file/d/1YnYE9Jcrv7MXE-Uom0XqML-drSJ3kn1y/view?usp=sharing
   [TCP_TEA16f_google]: https://drive.google.com/file/d/1_NNRE1DEeghX9MvRi0-w3abmEE2dmxny/view?usp=sharing
   
   [TCP_TEA8f_baidu]: https://pan.baidu.com/s/1grKR6UWLVpQBrNHoaFNlJQ
   [TCP_TEA16f_baidu]: https://pan.baidu.com/s/1YfjpwcWWzxFYLS22f2OZ5Q
   
   [TCP_R1528f_google]: https://drive.google.com/file/d/108pRkpSOZ8uyaej_PYlkn2lfuOMWSl39/view?usp=sharing
   [TCP_R15216f_google]: https://drive.google.com/file/d/15A1OhUXE_5YRH_TS5H914_BHfsZgrMNd/view?usp=sharing
   [TCP_R1528f_baidu]: https://pan.baidu.com/s/10Or9C6R1GM6maRe6YL618w
   [TCP_R15216f_baidu]: https://pan.baidu.com/s/1sNdlxl9WBQN0jdpOHsOjWA
   
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

- We thank [TSM][1] for providing the base basic tool box.
- We also adopt some parts from [iSQRT][2], [TEA][3] and [Non-local][4] and [S3D][S3D]. 
- We would like to thank Facebook for developing pytorch toolbox.

Thanks for their work!
  
  [1]: https://github.com/mit-han-lab/temporal-shift-module
  [2]: https://github.com/jiangtaoxie/fast-MPN-COV
  [3]: https://github.com/Phoenix1327/tea-action-recognition
  [4]: https://github.com/facebookresearch/SlowFast
  [5]: https://pytorch.org
  [S3D]: https://github.com/s9xie/Mini-Kinetics-200
  
  
