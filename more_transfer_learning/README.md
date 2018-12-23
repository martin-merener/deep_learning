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

### Data sizes and accuracies on Validation and Test sets

1. Fruits: 25,679 (train), 17,119 (validation), 14,369 (test). Accuracies: 99.5% (validation), 99.0% (test). 

# [KEEP EDITING BELOW]

2. Skin-cancer: _______ (train), _____ (validation), _____ (test). Accuracies: ____% (validation), ____% (test).
3. Pneumonia: _______ (train), _____ (validation), _____ (test). Accuracies: ____% (validation), ____% (test).
4. Retina: _______ (train), _____ (validation), _____ (test). Accuracies: ____% (validation), ____% (test).

### Confusion matrices on Test sets


1. Fruits: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/dogs_CM.JPG)

2. Skin-cancer: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/martial_CM.JPG)

3. Pneumonia: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/toys_CM.JPG)

4. Retina: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/quick_transfer_learning/images/sushi_CM.JPG)
