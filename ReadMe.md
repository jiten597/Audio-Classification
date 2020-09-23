# Cornell Birdcall Identification Competition
Solution to the [Cornell Birdcall Identification competition](https://www.kaggle.com/c/birdsong-recognition) hosted on Kaggle.

# Context
In this competition, you will identify a wide variety of bird vocalizations in soundscape recordings. Due to the complexity of the recordings, they contain weak labels. There might be anthropogenic sounds (e.g., airplane overflights) or other bird and non-bird (e.g., chipmunk) calls in the background, with a particular labeled bird species in the foreground. Bring your new ideas to build effective detectors and classifiers for analyzing complex soundscape recordings!
# Evaluation
Scores were evaluated based on their row-wise micro averaged F1-score.
# Model
* ResNeSt50 (pretrained)
* Finetune this above model
* 4 Stratified folds
