# Quick transfer learning with fastai

This project shows how to quickly implement an image classifier with fastai library, based on Transfer Learning from a pre-trained deep neural network. 

### Models

I built 4 classifiers (one notebook for each) for different image recognition problems:
1. Happy vs angry dogs.
2. Taekwondo vs Judo matches.
3. Shopkins vs Trashies toys (daughter's idea).
4. Twelve different kinds of sushi: mackerel, eel, shrimp, sea urchin, salmon roe, fatty tuna, octopus, yellowtail, squid,
salmon, sweet egg, red tuna.

### Approach

1. Images were downloaded from google images, somewhere between 100 and 400 images per category (details about how to do this in fast.ai mooc).
2. Manually curated to remove duplicates and perform cropping when needed (time consuming!).
3. Data partitioned into training and validation (30%).
4. Transfer learning by tuning the last layer of resnet34 for 10 epochs (under 5 minutes). No hyper-parameter optimization (just fastai default values). 
5. At the end of the 10 epochs, performance via accuracy and confusion matrix were computed on the validation set.

### Data sizes and performances on validation

1. Dogs: 336 (train), 144 (validation), 92% accuracy. 
2. Martial arts: 493 (train), 211 (validation), 98% accuracy.
3. Toys: 264 (train), 112 (validation), 95% accuracy.
4. Sushi: 2049 (train), 877 (validation), 93% accuracy. This worked fairly well considering that there were 12 classes.

### Web app demo

I used Zeit to put the sushi classifier in a basic web app for demo purposes: https://sushiclassifier-xiylbmtwnr.now.sh/

The image classifier can handle images that contain sushi of one kind only, from the 12 listed above. 

The output of the app is the list with the 3 most likely kinds, and their associated probabilities.

Details about how to create the web app: in https://towardsdatascience.com/building-web-app-for-computer-vision-model-deploying-to-production-in-10-minutes-a-detailed-ec6ac52ec7e4 

In a future version I will aim to make it able to handle multiple kinds of sushi in a same image, as well as tagging them in the image. It should also give a "no known sushi" if the image contains no sushi, or a kind different from the 12 on which it was trained. And if I daydream, after automatically tagging each kind of sushi, it would allow the user to rate each piece 1-5, and based on collaborative filtering from all users, recommend sushi restaurants to the user :)
