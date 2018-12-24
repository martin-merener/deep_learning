# More challenging transfer learning with fastai

Continuing the experiments with transfer learning using fastai library, in this project I solve image classification problems with more challenging, larger and realistic datasets. 

### Models

I built 4 classifiers (one notebook for each) for different image recognition problems:
1. 57,000 images of fruits classified into 83 different categories.
2. 10,000 images of skin lesions classified into 7 types of skin-cancer diagnoses.
3. 5,800 Chest X-Ray images that are classified into Pneumonia or Normal.
4. 85,000 images of retinas, which are classified into 4 categories (normal, and 3 diseases).

### Approach

1. All datasets are publicly available, with links to sources provided in the corresponding notebooks.
2. When a Train vs Test partition was not provided, it was created at random, and stratified by label in the case of strong unbalance.
3. Transfer learning is applied, by tuning the last layer first, and then continuing with more tuning of earlier layers. Hyper-parameters are mostly left as default, except for size (of image), batch-size (for memory constraints), and the type of pre-trained NN (either resnet 34 or 50). 
4. All trial and error are done before computing the performances on Test set, which are reported at the end of each notebook. 

### Data sizes and performances on Validation and Test sets

1. Fruits: 25,679 (train), 17,119 (validation), 14,369 (test). Accuracies: 99.5% (validation), 99.0% (test). 
2. Skin-cancer: 5,029 (train), 2,024 (validation), 2,962 (test). Accuracies: 84.6% (validation), 82.6% (test). 
3. Pneumonia: 3,663 (train), 1,569 (validation), 624 (test). Accuracies: 96.9% (validation), 92.9% (test).
4. Retina: _______ (train), _____ (validation), _____ (test). Accuracies: ____% (validation), ____% (test).

### Confusion matrices on Validation and Test sets

# [KEEP EDITING BELOW]

#### 1. Fruits: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/dogs_CM.JPG)

#### 2. Skin-cancer: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/martial_CM.JPG)

#### 3. Pneumonia: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/toys_CM.JPG)

Validation
precision 0.9929824561403509
recall 0.9658703071672355
F1-score 0.9792387543252596

Test
accuracy 0.9294871794871795
precision 0.9042056074766355
recall 0.9923076923076923
F1-score 0.9462102689486552

#### 4. Retina: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/sushi_CM.JPG)
