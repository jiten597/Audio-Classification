# Cornell Birdcall Identification Competition
Solution to the [Cornell Birdcall Identification competition](https://www.kaggle.com/c/birdsong-recognition) hosted on Kaggle.

# Context
In this competition, you will identify a wide variety of bird vocalizations in soundscape recordings. Due to the complexity of the recordings, they contain weak labels. There might be anthropogenic sounds (e.g., airplane overflights) or other bird and non-bird (e.g., chipmunk) calls in the background, with a particular labeled bird species in the foreground. Bring your new ideas to build effective detectors and classifiers for analyzing complex soundscape recordings!
# Evaluation
Scores were evaluated based on their row-wise micro averaged F1-score.
# Model
* Used pretrained weight of ResNeSt50 (ResNeSt50-fast-1s1x64d) using this [repository](https://github.com/zhanghang1989/ResNeSt).
* Finetune this above model.
# Training
* Randomly crop 5 seconds for each train audio clip each epoch.
* Used BCELoss.
* Trained 50 epoch and saved the weight which got best loss (this is because f1 score relies on thresholds.)
* Adam optimizer (lr=0.001) with CosineAnnealingLR (T_max=10).
* Used StratifiedKFold(n_splits=5) to split dataset.
* batch_size: 50
* melspectrogram parameters
  * n_mels: 128
  * fmin: 20
  * fmax: 16000
* image size: 224x547
# Augmentation
## SpecAugment [arXiv 1904.08779](https://arxiv.org/pdf/1904.08779.pdf)
SpecAugment consists of three consecutive augmenatation methods:
* **Time warp:** exchange some tuple of points in a row audio signal.
* **Frequency masking:** mask some horizontal line inside a mel-spectrogram.
* **Time masking:** mask some vertical line inside a mel-spectrogram.
# Inference
**OOF (Out of Fold) Ensemble**
Ensemble the models from each fold which was saved the weight got best loss.

# Reference
## ResNeSt: Split-Attention Networks
author: Hang Zhang, Chongruo Wu, Zhongyue Zhang, Yi Zhu, Zhi Zhang, Haibin Lin, Yue Sun, Tong He, Jonas Muller, R. Manmatha, Mu Li and Alex Smola
paper: [arXiv 2004.08955](https://arxiv.org/abs/2004.08955)
code: [GitHub](https://github.com/koukyo1994/kaggle-birdcall-resnet-baseline-training)
## SpecAugment
paper: [arXiv 1904.08779](https://arxiv.org/pdf/1904.08779.pdf)
code: [GitHub](https://github.com/zcaceres/spec_augment)
