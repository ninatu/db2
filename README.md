# DB2: DeBiasing Video Datasets for Enhanced Video Understanding

by [<ins>Nina Shvetsova</ins>](https://ninatu.github.io/), 
[<ins>Arsha Nagrani</ins>](https://a-nagrani.github.io/),
[<ins>Bernt Schiele</ins>](https://www.mpi-inf.mpg.de/departments/computer-vision-and-machine-learning/people/bernt-schiele),
[<ins>Hilde Kuehne</ins>](https://hildekuehne.github.io/),
[<ins>Christian Rupprecht</ins>](https://chrirupp.github.io/).

# DB2 Dataset

Our DB2 Dataset consist of two parts: 
1. **DB2-Annotations**: This includes frame annotations for four conceptual categories 
visible in video frames: *objects, activities, verbs*, and *objects+composition+activities*. 
DB2-Annotations are provided for 8 uniformly sampled frames from the training and 
test/val sets of 12 action recognition and text-to-video retrieval datasets. 
The annotations for *objects+composition+activities* are generated using the [LLaVA-1.6-7B-mistral](https://github.com/haotian-liu/LLaVA/blob/main/docs/MODEL_ZOO.md) 
VLM prompted to describe visible object relationships in a frame. 
From these descriptions, *objects, activities,* and *verbs (activities without associated objects)*
are derived using the [Mistral-7B-Instruct-v0.2](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.2) model.
2. **DB2-Splits**: This includes object-debiased test/val splits, 
which are subsets of the original test/val splits with object-biased items removed.
These debiased splits are provided for the 12 considered activities recognition and text-to-video
retrieval datasets.

Considered 6 activities recognition datasets:
* [UCF101 (UCF)](https://arxiv.org/pdf/1212.0402)
* [SomethingSomethingv2 (SSv2)](https://openaccess.thecvf.com/content_ICCV_2017/papers/Goyal_The_Something_Something_ICCV_2017_paper.pdf) 
* [Kinetics400 (K400)](https://arxiv.org/pdf/1705.06950)
* [Kinetics600 (K600)](https://arxiv.org/pdf/1808.01340)
* [Kinetics700 (K700)](https://arxiv.org/pdf/1907.06987)
* [Moments In Time (MiT)](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8651343) 

Considered 6 text-to-video retrieval datasets:
* [MSRVTT (MSR)](https://openaccess.thecvf.com/content_cvpr_2016/papers/Xu_MSR-VTT_A_Large_CVPR_2016_paper.pdf)
* [YouCook2 (YC2)](http://youcook2.eecs.umich.edu/static/YouCookII/youcookii_readme.pdf)
* [DiDeMo (DDM)](https://openaccess.thecvf.com/content_ICCV_2017/papers/Hendricks_Localizing_Moments_in_ICCV_2017_paper.pdf)
* [LSMDC](https://openaccess.thecvf.com/content_cvpr_2015/papers/Rohrbach_A_Dataset_for_2015_CVPR_paper.pdf) 
* [ActivityNet (ANet)](https://openaccess.thecvf.com/content_cvpr_2015/papers/Heilbron_ActivityNet_A_Large-Scale_2015_CVPR_paper.pdf)
* [Spoken Moments in Time (S-MiT)](https://openaccess.thecvf.com/content/CVPR2021/papers/Monfort_Spoken_Moments_Learning_Joint_Audio-Visual_Representations_From_Video_Descriptions_CVPR_2021_paper.pdf)


## Dataset: DB2-Annotations 

DB2-Annotations include frame annotations for four different concept categories: *objects,  activities, verbs*, 
and *objects+composition+activities* for the 12 considered datasets for both train and test/val splits. For test/val splits, 
we additionally provide *objects+composition+activities*_15_words -- a ~15-words summary of *objects+composition+activities* 
descriptions. 

We follow standard train/test/val splits of each corresponding dataset. Namely, as test/val sets we use validation sets for 
SSv2, K400, K600, K700, MiT, YC2, and ANet dataset, and test sets for UCF (testlist01), MSR (1k test set), DDM, LSMDC, S-MiT datasets. 

We provide annotation for 8 uniformly sampled frames of each video. Namely, we split each video on 8 equal temporal segments 
and select a central frame of each segment. 

**Note:** Due to the large size of the train sets of the MiT and S-MiT datasets 
and significant overlap in training videos, we provide annotations for approximately 
300k train videos contained in both datasets. 
For all other datasets, we provide annotations for the full train sets. 

### Get the dataset: 
**DB2-Annotations** for all 12 datasets are available at the following link: [Link](https://drive.google.com/drive/folders/1Gi38ebUnTRRKznOgWD979EnfzbV1aMlh?usp=sharing) 

The folder also contrain **DB2-Annotations-raw** : this version stores the raw outputs of VLM and LLM for concept categories.
In the DB2-Annotation version, textual descriptions of objects, activities, and verbs 
have been post-processed by removing numbering and text within brackets.

[comment]: <> (|                      | [UCF]&#40;https://arxiv.org/pdf/1212.0402&#41; | [SSv2]&#40;https://openaccess.thecvf.com/content_ICCV_2017/papers/Goyal_The_Something_Something_ICCV_2017_paper.pdf&#41; | [K400]&#40;https://arxiv.org/pdf/1705.06950&#41; | [K600]&#40;https://arxiv.org/pdf/1808.01340&#41; | [K700]&#40;https://arxiv.org/pdf/1907.06987&#41; | [MiT]&#40;https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8651343&#41;  | [MSR]&#40;https://openaccess.thecvf.com/content_cvpr_2016/papers/Xu_MSR-VTT_A_Large_CVPR_2016_paper.pdf&#41; | [YC2]&#40;http://youcook2.eecs.umich.edu/static/YouCookII/youcookii_readme.pdf&#41; | [DDM]&#40;https://openaccess.thecvf.com/content_ICCV_2017/papers/Hendricks_Localizing_Moments_in_ICCV_2017_paper.pdf&#41; | [LSMDC]&#40;https://openaccess.thecvf.com/content_cvpr_2015/papers/Rohrbach_A_Dataset_for_2015_CVPR_paper.pdf&#41;  | [ANet]&#40;https://openaccess.thecvf.com/content_cvpr_2015/papers/Heilbron_ActivityNet_A_Large-Scale_2015_CVPR_paper.pdf&#41; | [S-MiT]&#40;https://openaccess.thecvf.com/content/CVPR2021/papers/Monfort_Spoken_Moments_Learning_Joint_Audio-Visual_Representations_From_Video_Descriptions_CVPR_2021_paper.pdf&#41; |)

[comment]: <> (|:-----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|)

[comment]: <> (| **DB2-Annotation** &#40;train set&#41;   | [Link]&#40;https://drive.google.com/file/d/1qcjq0SzBwVmb2_CpeFjrMpOdti1fGIBQ/view?usp=sharing&#41; | | | | | | | | | | | |)

[comment]: <> (| **DB2-Annotation** &#40;test/val set&#41;   | | | | | | | | | | | | |)

[comment]: <> (| **DB2-Annotation-raw** &#40;train set&#41;   | [Link]&#40;&#41; | | | | | | | | | | | |)

[comment]: <> (| **DB2-Annotation-raw** &#40;test/val set&#41;   | | | | | | | | | | | | |)

### How To Use

* Each file is a JSON file that contains a dictionary with video IDs as keys.
* For each video ID, we provide `objects+composition+activities`, `objects`, `activities`, and `verbs` lists. 
These are lists containing textual descriptions of the respective concepts for 8 uniformly sampled frames.
* For the test/val set, we additionally provide `objects+composition+activities_15_words`.
 
**Example**:
```python
import json
with open('annotations_ucf_testlist01.json') as fin:
    data = json.load(fin)

data['v_ApplyEyeMakeup_g01_c02']
```

```shell
{'objects+composition+activities': ["In the photo, there is a person applying makeup, specifically eyeliner, to their eye. The person is holding a makeup brush in their right hand, which is being used to apply the eyeliner. The person's left hand is holding a small, pointed object, which appears to be a makeup applicator or a similar tool, possibly used for blending or smudging the eyeliner.\n\nThe person is seated in front of a mirror, which is reflecting their face and the objects they is using. The mirror is positioned on a surface that is not fully visible in the photo, but it seems to be a flat surface, possibly a table or a countertop.\n\nIn the background, there is a chair and a suitcase, suggesting that the setting might be a bedroom or a dressing room. The suitcase is closed and placed on the floor, while the chair is positioned against a wall. The objects in the background are not the main focus of the photo, but they provide context for the environment in which the person is applying makeup. ",
  "In the photo, there is a person who appears to be applying makeup. The person is holding a makeup brush in their right hand, which is raised towards their face. The makeup brush is being used to apply makeup, likely eyeshadow or eyeliner, to the person's eye area. The person's left hand is holding a small, round object that could be a compact mirror or a small makeup brush.\n\nThe person is seated in front of a mirror, which is mounted on a wall. The mirror reflects the person's face and the objects in the room, including a chair and a suitcase. The chair is positioned to the left of the person, and the suitcase is placed on the floor to the right of the person.\n\nThe room has a dark color scheme, with the walls and furniture appearing to be black or dark brown. The lighting in the room is not very bright, which suggests that the photo may have been taken in a dimly lit environment. The overall setting appears to be a personal space, possibly a bedroom or a bathroom, where the person is engaged in a personal grooming activity. ",
  ...]
 'objects': ['person, makeup brush, makeup applicator, mirror, table or countertop, chair, suitcase.',
  'person, makeup brush, right hand, face, mirror, wall, chair, suitcase, left hand, compact mirror or small makeup brush, dark walls, dark furniture, lighting, bedroom or bathroom',
  ...],
 'activities': ['A person is applying eyeliner. A person is holding a makeup brush. A person is holding a makeup applicator or a similar tool.',
  'The person is applying makeup.',
  ...],
 'verbs': ['Someone is applying something. Someone is holding something. Someone is holding something.',
  'Someone is applying something.',
  ...],
 'objects+composition+activities_15_words': ['Person applying eyeliner with a brush in hand, using a blending tool in the other, seated at a table near a mirror and a chair, with a suitcase in the background.',
  'Person applying makeup with raised hand, using mirror and brush in dimly lit, personal space, seated in front of a mounted mirror with a chair and suitcase nearby.',
  ...]}```
```

## Dataset: DB2-Splits 

DB2-Splits include objects debiased test/val splits for the 12 considered datasets. 
Object-debiased test/val splits are subsets (subsets of video ids) of the original test/val splits with object-biased items removed.

Note: Due to unavailability of some videos in some datasets, some video ids might be excluded completely. 

### Get the dataset: 
**DB2-Splits** for all 12 datasets are available at the following link: [Link](https://drive.google.com/drive/folders/1Gi38ebUnTRRKznOgWD979EnfzbV1aMlh?usp=sharing)

[comment]: <> (|                      | [UCF]&#40;https://arxiv.org/pdf/1212.0402&#41; | [SSv2]&#40;https://openaccess.thecvf.com/content_ICCV_2017/papers/Goyal_The_Something_Something_ICCV_2017_paper.pdf&#41; | [K400]&#40;https://arxiv.org/pdf/1705.06950&#41; | [K600]&#40;https://arxiv.org/pdf/1808.01340&#41; | [K700]&#40;https://arxiv.org/pdf/1907.06987&#41; | [MiT]&#40;https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8651343&#41;  | [MSR]&#40;https://openaccess.thecvf.com/content_cvpr_2016/papers/Xu_MSR-VTT_A_Large_CVPR_2016_paper.pdf&#41; | [YC2]&#40;http://youcook2.eecs.umich.edu/static/YouCookII/youcookii_readme.pdf&#41; | [DDM]&#40;https://openaccess.thecvf.com/content_ICCV_2017/papers/Hendricks_Localizing_Moments_in_ICCV_2017_paper.pdf&#41; | [LSMDC]&#40;https://openaccess.thecvf.com/content_cvpr_2015/papers/Rohrbach_A_Dataset_for_2015_CVPR_paper.pdf&#41;  | [ANet]&#40;https://openaccess.thecvf.com/content_cvpr_2015/papers/Heilbron_ActivityNet_A_Large-Scale_2015_CVPR_paper.pdf&#41; | [S-MiT]&#40;https://openaccess.thecvf.com/content/CVPR2021/papers/Monfort_Spoken_Moments_Learning_Joint_Audio-Visual_Representations_From_Video_Descriptions_CVPR_2021_paper.pdf&#41; |)

[comment]: <> (|:-----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|:-----:|:-----:|:----:|)

[comment]: <> (| **DB2-Splits**   | | | | | | | | | | | | |)

### How To Use

Each file is a JSON file that contains a dictionary with 3 keys: 
* `full` -- list of video ids of the original test/val split of a corresponding dataset  
* `debiased` -- list of video ids for our debiased test/val split of a dataset, 
where object-biased videos were removed.
* `splits_for_auc` -- list of lists of video ids for the area under the curve (AUC) 
computation over sequence of debiased splits where items with different strengths of object bias
removed, namely, starting from a `full` test\val set 
and sequentially debiasing wrt object bias, stopping when 10\% of test/val set is reached.  

**Example**:
```python
import json
with open('splits_ucf_testlist01.json.json') as fin:
    data = json.load(fin)

data
```

```shell
{'full': ['v_ApplyEyeMakeup_g01_c01',
  'v_ApplyEyeMakeup_g01_c02',
  ...],
  
  'debiased': ['v_ApplyEyeMakeup_g01_c01',
  'v_ApplyLipstick_g01_c03',
  ...],
  
  'splits_for_auc': [
  ['v_ApplyEyeMakeup_g01_c01',
  'v_ApplyEyeMakeup_g01_c02', ...],
  ['v_ApplyEyeMakeup_g01_c01',
  'v_ApplyLipstick_g01_c03', ...],
  ...]}
```

# License

The dataset is under the Creative Commons Attribution 4.0 (CC BY 4.0) license.
The terms of this license can be found at: [http://creativecommons.org/licenses/by/4.0](http://creativecommons.org/licenses/by/4.0). 
However, certain parts of the underlying dataset may be subject to stricter licensing conditions from the corresponding video datasets.



