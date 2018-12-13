# Quick-Draw
## By Abel Tadesse, Richy Chen, Jason Yi

## Brief Description:
Quick, Draw! game was originally an experimental game released by Google to teach the general population about artificial intelligence. The game asks the user to draw a picture of an object or idea and uses a neural network artificial intelligence to guess what the sketch represents. Moreover, the network continues to guess as the user draws, even though the sketch is incomplete. The network uses such drawings to learn and increase its accuracy in the future.

## Kaggle Competition/The Problem:
To begin, the training data comes from the actual Google game itself. Consequently, they may be incomplete or may not even represent the label. As a result, the task is to build a better classifier using the noisy dataset. 

## Data:
We are given two datasets from Kaggle. The raw data (65.87 GB) is the exact input recorded from user drawing. The simplified data (7.37 GB) removes unnecessary information from the vector. Kaggle provides such an example. Imagine a straight line was recorded with 8 points. Then the simplified version removes 6 points to create a line with 2 points. Each csv file represents one "label" representing the drawing. Each row in the csv file represents a drawing or sketch with multiple strokes. Each stroke is represented by x,y, and t coordinates where t stands for time. Moreover, these are represented by nested arrays. 

INSERT IMAGE 

## Approach: RNN vs CNN:
The two most common type of neural network structures used were RNN and CNN. Our first choice was to implement an RNN. Consequently, we took a baseline model from Kevin Mader and decided to first see how well it performed. We discovered that there were many issues with the baseline model. First, the training took too long, the accuracy was too low, and the model was too complicated relative to its performance.
TALK MORE ABOUT RNN
![rnn_initial](https://user-images.githubusercontent.com/35898484/49917030-54e70600-fe52-11e8-868d-f5dbd7f3194a.PNG)
![rnn_final](https://user-images.githubusercontent.com/35898484/49917041-65977c00-fe52-11e8-8c7d-da7a964f3e7a.PNG)

INSERT IMAGE OF ARCITECT

We next attempted to compare the performance of our modified RNN to a CNN model. As a result, we similarly took a baseline model from JohnM and modified it with our own ideas. For the architecture of the model, we found that it was best to start with a 2D convolutional layer instead of a fully connected layer because it would otherwise lose spatial information. We also kept some of the original structure such as the implementation of max pooling to down sample the features and flatten to transform a tensor of any shape to a one dimensional tensor. Finally, we incorporated drop outs in between each dense layer that we added. The reason we added it after a dense layer instead of a convolutional layer was that a convolutional layer has less parameters than a dense layer. As a result, a convolutional layer has less of a need for regularization to prevent overfitting compared to a fully connected dense layer. When run on the Kaggle kernel, the final result of our implementation came out to be a validation accuracy of 65.63%, validation loss of 1.2015, and a top 3 validation accuracy of 85.17%. The results of the loss and accuracy are shown in the graph below.

![cnn](https://user-images.githubusercontent.com/35898484/49917050-70521100-fe52-11e8-996f-dc249dda0dfc.PNG)

INSERT IMAGE OF ARCHITECT

## Thoughts on difference between RNN and CNN
After comparing the results, we found that the CNN model resulted in a better accuracy compared to that of a RNN model. We began to think about the possible reasons why this was the case. In order to do so, we delved into the definitions of the models more deeply. We knew that the RNN was used to find patterns in sequential data. As a result, in this case, the RNN likely interpreted the drawing as sequences of 2D coordinates based on the individual strokes. The CNN on the other hand likely interpreted the drawing as a whole image with all the strokes at completion. Consequently, it would have interpreted the drawing as a 2D object. Understanding the differences in each model, we believed that one of the reasons the CNN performed better was the fact that each sketch depended on a variety of factors such as the nationality of the user, the individual person, and the speed of the sketch. Depending on the country or preference, many individuals have different starting points when they draw certain objects or letters. As a result, the model would need to be able to learn such differences. Consequently, when a RNN trains on a given data, it would need to account for the different ordering and speed of the individual strokes. Therefore, there may have been too many variations to generalize for the future data. However, intuitively, we believed that the CNN essentially "memorized" the image and therefore had better luck in generalizing for future data. 

INSERT IMAGE 

## Time log of RNN

## Time log of CNN
