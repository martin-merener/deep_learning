# Counting objects with a CNN by regression

In this project I study the task of counting objects of interest in images, by training a CNN for regression using transfer learning (resnet18).

## Model

I build a regression model for the problem of counting the number of horizontal rectangles, which are mixed with vertical rectangles. The images, a total of 16,000, are synthetically created. 

## Approach

1. The dataset is synthetically generated with the purpose of making the learning task challenging and interesting.
2. Images are created using parameters such as: the number of horizontal rectangles (which is the label/target variable), the total number of rectangles, and their sizes.
3. These parameters have limited values to generate the training images, but additional values to generate the testing images, which allows to evaluate the capacity of the CNN to generalize beyond training. 
4. A detailed analysis of the performance on different subsets of the testing seet is performed, to assess the success of the task of counting objects by the trained CNN.

## Data sizes and performances on Validation and Test sets

Counting horizontal rectangles: 8,881 (train), 2,941 (validation), 7,855 (test). MAE: 1.4 (validation), 2.3 (test). Examples: ![alt text](https://github.com/martin-merener/deep_learning/blob/master/count_with_a_CNN/images/4_examples.JPG)


## Plots: actual vs predicted, actual vs error, rel-error histogram

##### Validation:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/count_with_a_CNN/images/assessment_valid.JPG)

##### Test (all):

![alt text](https://github.com/martin-merener/deep_learning/blob/master/count_with_a_CNN/images/assessment_test.JPG)

##### Test with parameter values as in training:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/count_with_a_CNN/images/assessment_test_known_vals_img_params.JPG)

##### Test with actual counts having values not seen in training:

![alt text](https://github.com/martin-merener/deep_learning/blob/master/count_with_a_CNN/images/assessment_test_unknown_vals_n_obj.JPG)

#### Conclusions (justification in notebook):

- A CNN trained to counting by regression on about 6,000 images having counts of the target object (horizontal rectangle) between 5 and 45, achieves a mean absolute error of 1.4 on Test images generated with the same parameter values that the training images were generated. On 50% of the images, the estimated count has a relative error below 5.5%, and in 95% of images a relative error below to 21.3%.
- The images are created synthetically, generating horizontal and vertical white rectangles in random positions over a black background. The number of horizontal rectangles is the target variable of the regression task, while the vertical rectangles are introduced to avoid the number of white pixels to be a proxy for the count of horizontal rectangles (which would be an easy task if the images contain only the targeted horizontal rectangles).
- The training images contain a number of rectangles between 5 and 45, but only 28 of those values. However, the missing values, as well as values from 0 to 5, and from 46 to 50, are instead quantities of horizontal rectangles on testing images. The CNN shows very good generalization ability on images with those unknown-at-training label values: the MAE in this case is 1.6.
- The CNN also generalizes well to unknown values for the total number of rectangles. That is, when images have a total number of rectangles above or below the total numbers provided on training, the CNN still predicts the total number of horizontal rectangles very well: MAE for this case is 1.4.
- The CNN however shows a limitation at generalizing the ability to count horizontal rectangles when the sizes of these are different than the varying sizes using for training. This seem to suggest that the number of white pixels influences the count estimation more than it should. However, a closer analysis shows that within the rectangle size range used for training, the count of horizontal rectangles is constant with respect to the size of the rectangles. It is outside of the training range that the count estimation shows a monotonically increasing relationship with the size of the rectangles.
