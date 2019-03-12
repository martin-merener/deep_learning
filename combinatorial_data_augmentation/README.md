# Combinatorial Data Augmentation

In this project I develop a data augmentation approach that shows a strong reduction of test error rate in binary classification of images from the Fashion MNIST dataset.

The technique, which I call Combinatorial Data Augmentation (CDA), is suitable when very few labelled images are available, even for transfer learning, e.g., 10 labelled images from each category. The notebook presents only binary case, but the exact same idea can be applied to multi-class problems. 

The technique assumes that a pre-trained neural network is available, and that of course it has not been trained on the classes that the current problem aims to classify (otherwise, there is nothing to solve). In the notebook I use resnet34.

## How CDA works

Suppose we want to classify images from these two categories...[insert images] and we have only 12 images from each class, so 24 labelled images in total. We could leave 8 images for validation, and use the other 16 for transfer learning on resnet34, tuning the weights of the last layer. That's going to be the benchmark.

What CDA does is to produce a large set of _collages_ from those 16 images used for training. These collages are simply 3x3 arrays of images taken randomly among the 16 available for training. [insert example].

Because there are 9=3x3 locations, and 16 images available, the number of different collages is $16^9>10^10$. We would obviously not consider all possible collages, but only a subset of them, say around 50,000. The label of a collage is given by the class that occurs the most amoung the 9 images in it.

Once the collages are created, a transfer learning from resnet34 is applied using them, and because the number of collages is now large, one can tune more than just the last layer of resnet34, which gives a neural network $N_{alt}$. 

Finally, one applies a transfer learning on $N_{alt}$, based on the 16 original training images, just as it was done for the benchmark, adjusting the weights in the last layer.

## Experiments

## Results

## Conclusions

