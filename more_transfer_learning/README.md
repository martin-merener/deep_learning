# More challenging transfer learning with fastai

Continuing the experiments with transfer learning using fastai library, in this project I solve image classification problems with more challenging, larger and realistic datasets. 

## Models

I built 4 classifiers for different image recognition problems (one notebook for each):
1. 57,000 images of fruits, for classification into 83 different categories.
2. 10,000 images of skin lesions, for classification into 7 types of skin-cancer diagnoses.
3. 5,800 Chest X-Ray images, for a binary classification, Pneumonia or Normal.
4. 85,000 images of retinas, for classification into classified into 4 categories (normal, and 3 diseases).

## Approach

1. All datasets are publicly available, with links to sources provided in the corresponding notebooks.
2. When a Train vs Test partition was not provided, it was created at random, and stratified by label in the case of strong unbalance.
3. Transfer learning is applied, by tuning the last layer first, and then continuing with more tuning of earlier layers. Hyper-parameters are mostly left as default, except for size (of image), batch-size (for memory constraints), and the type of pre-trained NN (either resnet 34 or 50). 
4. All trial and error are done before computing the performances on Test set, which are reported at the end of each notebook. 

## Data sizes and performances on Validation and Test sets

1. Fruits: 25,679 (train), 17,119 (validation), 14,369 (test). Accuracies: 99.5% (validation), 99.0% (test). 
2. Skin-cancer: 5,029 (train), 2,024 (validation), 2,962 (test). Accuracies: 84.6% (validation), 82.6% (test). 
3. Pneumonia: 3,663 (train), 1,569 (validation), 624 (test). Accuracies: 96.9% (validation), 92.9% (test).
4. Retina: 75,136 (train), 8,348 (validation), 1,000 (test). Accuracies: 96.8% (validation), 99.0% (test).

## Confusion matrices on Validation and Test sets

### 1. Fruits 

##### Validation:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/fruits_va_CM.JPG)

##### Test:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/fruits_te_CM.JPG)

### 2. Skin-cancer: 

##### Validation:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/skincancer_va_CM.JPG)

##### Test:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/skincancer_te_CM.JPG)

##### Normalized confusion matrices:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/skin_normalized_cms.JPG)

### 3. Pneumonia: 

##### Validation:

- Precision 0.993
- Recall 0.966
- F1-score 0.980

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/pnemounia_va_CM.JPG)

##### Test:

- Precision 0.904
- Recall 0.992
- F1-score 0.946

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/pnemounia_te_CM.JPG)

### 4. Retina: 

##### Validation:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/retina_va_CM.JPG)

##### Test:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/more_transfer_learning/images/retina_te_CM.JPG)
