# Combinatorial Data Augmentation

In this project I develop a data augmentation approach that provides a strong reduction in test error rate for image classification of images from the Fashion MNIST dataset (10 classes).

The technique, which I call _Combinatorial Data Augmentation_ (CDA), shows very promising results when very few labelled images are available even for transfer learning, e.g., 10 labelled images from each category. 

The technique assumes that a pre-trained neural network is available, and that it has not been trained on the classes that the current problem aims to classify (otherwise, there is no problem to solve). For example, resnet34.

The two accompanying notebooks cover: 

#### 1. Binary Case and Analysis

All 45 pairs of classes in Fashion MNIST are tested, and then two specific pairs (one hard to distinguish, one easy) are analyzed in more detail. 

#### 2. Multi-class case

All 10 categories are classified at once.

### Dataset

The Fashion-MNIST dataset https://github.com/zalandoresearch/fashion-mnist contains images for 10 categories of clothing. It is partitioned into two subsets, one with 60,000 images (6,000 for each class), and a second one with 10,000 images (1,000 for each class). Typically the first one would be used for training, and the second for testing. However, in the multi-class case, we switch them, and use the 60K for testing (to have a reliable performance measure), and the 10K for training, because we require precisely a low number of training images. 

The list of categories is:

tshirt; trouser; pullover; dress; coat; sandal; shirt; sneaker; bag; boot

Some examples:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/images_multiclass.JPG)



## 1. Binary case and analysis

https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/MM_project_combinatorialDataAugmentation_binary_saveBestModel.ipynb

### 1.1 How CDA works

Suppose that we want to classify images from these two categories: 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_images_easy_pair.JPG) 

And suppose that we have only 12 images from each class, so 24 labelled images in total. We could leave 8 images for validation and use the other 16 for transfer learning on resnet34, tuning the weights of the last layer. That's going to be the benchmark, but it is unlikely to yield very accurate results due to the low number of examples.

What CDA does is to produce a large set of _collages_ from the 16 images used for training. These collages are simply 3x3 arrays of images taken randomly among the 16 available for training. 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_collages_easy_pair.JPG)

Because there are 9=3x3 locations, and 16 images available, the number of different collages is $16^9>10^{10}$. We would obviously not consider all possible collages, but only a subset large enough, say around 50,000. The label of a collage is given by the class that occurs the most among the 9 images in it.

Once the desired number of collages is generated, a transfer learning from resnet34 is applied using them, and because the number of collages is now large, one can tune more than just the last layer of resnet34, which gives a neural network $N_{alt}$. 

Finally, one applies a transfer learning on $N_{alt}$, based on the 16 original training images, just as it was done for the benchmark, adjusting the weights in the last layer. 

The intuition is that because $N_{alt}$ has learned to classify the collages according to the majority class in them, and this has been done for thousands of images (potentially millions), $N_{alt}$ has learned already a lot of useful patterns related to the problem of interest. Therefore, a further transfer learning starting at $N_{alt}$, and based on the 16 original images, would likely do a better job at classifying the two original classes. 

### 1.2 Experiments

The notebook shows that for the 45 possible binary classification problems induced by the Fashion MNIST dataset (which has 10 classes, therefore 45 possible un-ordered pairs), the CDA approach achieves a much smaller error rate than the benchmark on a dataset.

In addition, two specific pairs, one "easy" and one "hard" to classify, are analyzed in more detail, by looking at how the error rate in the test set behaves as a function of $m=|X_t|$, the number of training images.

### 1.3 Results

#### Easy pair 

Both solutions, the benchmark and CDA are obtained, for different values of $m=|X_t|$, for the "easy" pair: _coat_ vs _boot_. 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_collages_easy_pair.JPG)

The following graph shows the error rate on a test set having 1000 images for each class.

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_error_rates_easy_pair.JPG)

The following graph shows the ratio between the error rate for CDA and the benchmark, which expresses the error rate of CDA as a percentage of the error rate of the benchmark. 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_ratio_error_rates_easy_pair.JPG)

#### Hard pair

The same for the "hard" pair: _pullover_ vs _shirt_.

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_images_hard_pair.JPG)

Their collages look like:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_collages_hard_pair.JPG)

Error rates on test set:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_error_rates_hard_pair.JPG)

Ratios between error rates:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_ratio_error_rates_hard_pair.JPG)

#### All pairs

In addition, all 45 possible pairs among the 10 categories are considered, for some value of $m=|X_t|$ between 4 and 180, and the error rates on a test set are shown for both the benchmark and CDA. In all, but 1 case, CDA performs better than the benchmark. The results are shown here increasingly with respect to the ratio of error rates between CDA and the benchmark

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/project4_performances_all_pairs_.JPG)





## 2. Multi-class case

https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/MM_project_combinatorialDataAugmentation_multiclass_allData_fashionMNIST.ipynb

### 2.1 How CDA works

Similarly to the binary case, we now want to classify images into one of the 10 possible classes. 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/images_multiclass.JPG) 

As before, we are going to have a low number of images from each class: such as 8 images to train and 2 for validation (from each class), so 100 labelled images in total to build a classifier. The benchmark would be to do transfer learning on the 80 training images, and selecting the best model across many epochs based on the 20 validation images.

With CDA instead, we create more than 100,000 collages. These collages are generated by picking two classes at random, and then randomly selecting 9 images from these two classes and placing them in a $3 \times 3$ array. The label is given by the class that appears more often among the 9 images. 

The number of possible collages is actually much higher than 100,000. The upper bound is $45 \times 16^9>10^{12}$). 

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/collages_multiclass.JPG)

The process then follows in exactly the same was as the binary case.

### 1.2 Experiments

The notebook shows the error rate obtained on the test set (60,000 images), for both the Benchmark and CDA, for different number of training images. 

### 1.3 Results

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/error_rates_cda_benchmark_multiclass.JPG)

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/errors_ratio_multiclass.JPG)


#### Confusion matrix with $|X_t|+|X_v|=200$

This is the case in which $s=2$, so $|X_t|=160$ (16 images per class), and $|X_v|=40$ (4 images per class).

Benchmark:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/conf_matrix_benchmark_testset_m200.JPG)

CDA:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/combinatorial_data_augmentation/images/conf_matrix_cda_testset_m200.JPG)

## Conclusions 

This notebook presents a technique to deal with transfer-learning when the set of labelled images is too small to do an effective transfer learning using a pre-trained NN that has not originally being trained on the given labels.

The technique is tested on the Fashion-MNIST dataset, showing very promising results in terms of error rate reduction on a test set.

The reduction on error rate is higher when the number of training images is very low, and it is milder as the number of training images increases. 
