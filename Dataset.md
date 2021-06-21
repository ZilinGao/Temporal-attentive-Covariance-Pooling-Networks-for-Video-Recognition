
  ## Dataset Preparation(K-400 & Mini-K200)
  
####  Kinetics-400
We train Kinetics-400 with frame data. Extracted manner evolves from [TSM][1]. 

1. Download the [Kinetics-400][K-400](K-400) video samples, and it would be organized as following:

[1]: https://github.com/mit-han-lab/temporal-shift-module
[K-400]: https://deepmind.com/research/open-source/kinetics

```
├── train_256 (/path/to/K400/video/trainset/folder)
│   ├──class_1
│   │   ├── video1 (xxx.mp4 / xxx.mkv)
│   │   ├── video2
│   │   ├── ....
│   │   └── ...
│   ├── class_2
│   │   ├── video...
│   │   └── ...
│   └── class...
└── val_256 (/path/to/K400/video/valset/folder)
    ├──class_1
    │   ├── video1
    │   ├── video2
    │   ├── ....
    │   └── ...
    ├── class_2
    │   ├── video...
    │   └── ...
    └── class...
```

2. Extract frame from prepared videos:


`python tools/vid2img_kinetics.py  /path/to/K400/video/trainset/folder  /path/to/K400/frame/trainset/folder`
 
`python tools/vid2img_kinetics.py  /path/to/K400/video/valset/folder  /path/to/K400/frame/valset/folder`


File `vid2img_kinetics.py` is a modified version  from TSM toolbox, in which height is changed from 331 to 256 (needs ~1.4T space for train&val sets).

The extracted frame data would be organized like:
```
├── train (/path/to/K400/frame/trainset/folder)
│   ├──class_1
│   │   ├── video1(folder)
│   │   │      ├──img_00001.jpg
│   │   │      ├──img_00002.jpg
│   │   │      ├── ....
│   │   │      └── ...
│   │   └── video2
│   │          ├──img_00001.jpg
│   │          ├──img_00002.jpg
│   │          ├── ....
│   │          └── ...
│   └── class...
└── val (/path/to/K400/frame/valset/folder)
    ├──class_1
    │   └── video1
    │          ├──img_00001.jpg
    │          ├──img_00002.jpg
    │          ├── ....
    │          └── ...
    └── class...
```

**We strongly recommend to check whether the extracted samples are consistent with the number of videos in both training set and validation set after this step.**

3. generate `train.txt` and `val.txt`

```
python tools/txt_generator.py /path/to/K400/frame/trainset/folder  train.txt
python tools/txt_generator.py /path/to/K400/frame/valset/folder  val.txt
```

4. merge train dataset and val dataset

(move val set samples into training set)


```
python tools/merge_train_val.py /path/to/K400/frame/valset/folder /path/to/K400/frame/trainset/folder
```

the txt file would be  like:

`class_name/video_name  frames class_id`

e.g.:
```
playing_paintball/NVeQN7sDOUQ 360 0
finger_snapping/8XysUNy0gLE 360 1
```

5. assign  txt file path
modified the txt path and dataset root path to `ops/dataset_config.py`
```
        root_data = '/path/to/K400/frame/trainset/folder'
        filename_imglist_train = 'train.txt'
        filename_imglist_val = 'val.txt'
```

### Mini-Kinetics-200

Mini-Kinetics-200(Mini-K200) is a subset of K-400. So there are two manners to collect Mini-K200:

A: If you have extracted K-400 frames as above, generate your own Mini-K200 txt files directly:

(some links are broken, full Mini-K200 dataset is not available)


```
cd tools/Mini_K200/

#K400_to_K200_labels_as_K400.py inputs:   k400_txt   k200_full_txt   k200_our_txt
python K400_to_K200_labels_as_K400.py train.txt   train_ytid_list.txt  train_K200_old_labels.txt
python K400_to_K200_labels_as_K400.py val.txt   val_ytid_list.txt   val_K200_old_labels.txt


python   reset_K200_labels.py  train_K200_old_labels.txt  train_K200.txt
python   reset_K200_labels.py   val_K200_old_labels.txt   val_K200.txt

```

B: If you don't have K-400 frames data, extract Mini-K200 frames from full K-400 videos:

1. prepare K-400 videos (see  step1 in  section K-400), ~130G
2. extract the frames needed by Mini-K200 (~430G)


```
cd tools/Mini_K200/

python  vid2img_k200.py  /path/to/K400/video/trainset/folder /path/to/K200/frame/trainset/folder   train_ytid_list.txt
 
python  vid2img_k200.py  /path/to/K400/video/valset/folder /path/to/K200/frame/valset/folder   val_ytid_list.txt

```



3. generate your own Mini-K200 txt files(some links are broken, full Mini-K200 dataset is not available)

```
TO DO
```


4. merge train dataset and val dataset

(move val set samples into training set)


```
python  merge_train_val.py /path/to/K200/frame/valset/folder /path/to/K200/frame/trainset/folder
```

the txt file would be  like:

`class_name/video_name  frames class_id`

e.g.:
```
playing_paintball/NVeQN7sDOUQ 360 0
finger_snapping/8XysUNy0gLE 360 1
```

5. assign  txt file path
modified the txt path and dataset root path to `ops/dataset_config.py`
```
        root_data = '/path/to/K200/frame/trainset/folder'
        filename_imglist_train = 'tools/Mini_K200/train_K200.txt'
        filename_imglist_val = 'tools/Mini_K200/val_K200.txt'
```
