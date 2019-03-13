# deep_learning

## Project 1. Quick Transfer Learning. 
https://github.com/martin-merener/deep_learning/tree/master/quick_transfer_learning

Use fastai library (https://docs.fast.ai/), built on top of pytorch, for transfer learning. Build with it four classifiers for image recognition: three of them binary and one with 12 categories (12 different kinds of sushi). The purpose of the project is: 
(i) show how fastai can be easily used to build quick models with good accuracy; (ii) build a demo web app with Zeit using the sushi classifier, which provides estimations of the kind of sushi present in an uploaded image.

## Project 2. More Challenging Transfer Learning. 
https://github.com/martin-merener/deep_learning/tree/master/more_transfer_learning

The purpose of this project is to show how to effectively do transfer learning (using fastai library) to solve classification problems with challenging and realistic datasets. This is achieved by showing very successful classification performances across 4 different datasets (publicly available).
In the first case, working with a dataset of 57,000 images of fruits which are classified into 83 different categories. The second dataset consists of 10,000 images of skin lesions, classified into 7 types of skin-cancer diagnoses. Then, 5,800 Chest X-Ray images for a binary classification into Pneumonia or Normal. Finally, a dataset of nearly 85,000 images of retinas, for classification into 4 categories (normal, and 3 diseases).

## Project 3. Counting objects with a CNN.
https://github.com/martin-merener/deep_learning/tree/master/count_with_a_CNN

The goal of this project is to study whether a convolutional neural network can learn to count objects in images. Throughout an experiment with synthetic images, it is shown that a regression model obtained by transfer learning from resnet18, it is possible to achieve low error counting objects of interest. The focus of the project is to ensure that the task of learning how to count is challenging, which is achieved by creating a non-trivial set of images. It is also shown how the achieved performance generalizes well to images created with underlying parameter values beyond those used for training. 
The objects being counted in the images are small white horizontal rectangles, which are located randomly along with vertical white rectangles. The target label for the regression problem is the number of horizontal rectangles only, ranging between 5 and 45. The model achieves a mean absolute error of 1.5. The work includes a thorough analysis of the performance of the CNN and its ability to generalize on the Test set.

## Project 4. Combinatorial Data Augmentation.
https://github.com/martin-merener/deep_learning/tree/master/combinatorial_data_augmentation

In this project I develop a data augmentation approach that provides a strong reduction in test error rate for binary classification of images from the Fashion MNIST dataset. The technique, which I call _Combinatorial Data Augmentation (CDA)_, shows very promising results when very few labelled images are available even for transfer learning, e.g., 10 labelled images from each category. The accompanying notebook describes the technique in detail, as well as thorough numerical experiments performed with the purpose of comparing the new technique to a benchmark given by straightforward transfer learning. In almost every case, the new technique CDA outperforms the benchmark significantly, and often dramatically. The technique is based on _collages_ constructed on the original input images, which by their combinatorial nature allow to generate an exponential number of new images.
