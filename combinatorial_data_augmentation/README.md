# Combinatorial Data Augmentation

In this project I develop a data augmentation approach that provides a strong reduction in test error rate for binary classification of images from the Fashion MNIST dataset.

The technique, which I call _Combinatorial Data Augmentation_ (CDA), shows very promising results when very few labelled images are available even for transfer learning, e.g., 10 labelled images from each category. The notebook presents only the binary case, but the exact same idea can be applied to multi-class problems. 

The technique assumes that a pre-trained neural network is available, and that it has not been trained on the classes that the current problem aims to classify (otherwise, there is no problem to solve). In the notebook I use resnet34.

## How CDA works

Suppose we want to classify images from these two categories...[insert images] and we have only 12 images from each class, so 24 labelled images in total. We could leave 8 images for validation and use the other 16 for transfer learning on resnet34, tuning the weights of the last layer. That's going to be the benchmark, but it is unlikely to yield very accurate results due to the low number of examples.

What CDA does is to produce a large set of _collages_ from the 16 images used for training. These collages are simply 3x3 arrays of images taken randomly among the 16 available for training. [insert example].

Because there are 9=3x3 locations, and 16 images available, the number of different collages is $16^9>10^10$. We would obviously not consider all possible collages, but only a subset large enough, say around 50,000. The label of a collage is given by the class that occurs the most among the 9 images in it.

Once the desired number of collages is generated, a transfer learning from resnet34 is applied using them, and because the number of collages is now large, one can tune more than just the last layer of resnet34, which gives a neural network $N_{alt}$. 

Finally, one applies a transfer learning on $N_{alt}$, based on the 16 original training images, just as it was done for the benchmark, adjusting the weights in the last layer. 

The intuition is that because $N_{alt}$ has learned to classify the collages according to the majority class in them, and this has been done for thousands of images (potentially millions), $N_{alt}$ has learned already a lot of useful patterns related to the problem of interest. Therefore, a further transfer learning starting at $N_{alt}$, and based on the 16 original images, would likely do a better job at classifying the two original classes. 

## Dataset

The Fashion-MNIST dataset https://github.com/zalandoresearch/fashion-mnist contains images for 10 categories of clothing, with 6,000 training images and 1,000 testing images for each category, giving at total of 70,000 images.

The list of categories is:

tshirt (T-shirt/top)
trouser
pullover
dress
coat
sandal
shirt
sneaker
bag
boot (Ankle boot)

## Experiments

This project shows that for the 45 possible binary classification problems induced by the Fashion MNIST dataset (which has 10 classes, therefore 45 possible un-ordered pairs), the CDA approach achieves a much smaller error rate than the benchmark on a dataset.

In addition, two specific pairs, one "easy" and one "hard" to classify, are analyzed in more detail, by looking at how the error rate in the test set behaves as a function of $m=|X_t|$, the number of training images.

## Results

Both solutions, the benchmark and CDA are obtained, for different values of $m=|X_t|$, for the "easy" pair: _coat_ vs _boot_. 

[insert images]

The following graph shows the error rate on a test set having 1000 images for each class.

[insert graph]

The following graph shows the ratio between the error rate for CDA and the benchmark, which expresses the error rate of CDA as a percentage of the error rate of the benchmark. 

The same for the "hard" pair: _pullover_ vs _shirt_.



## Conclusions

This notebook presents a technique to deal with transfer-learning when the set of labelled images is too small to do an effective transfer learning using a pre-trained NN that has not originally being trained on the given labels.

The technique is tested on the Fashion-MNIST dataset, showing very promising results in terms of error rate reduction on a test set.

The reduction on error rate depends on the categories used (here only binary case is studied), as well as the subset of images randomly selected for each run of the experiment.

The experiments show that almost every time the CDA technique has a significantly better performance than the benchmark.
