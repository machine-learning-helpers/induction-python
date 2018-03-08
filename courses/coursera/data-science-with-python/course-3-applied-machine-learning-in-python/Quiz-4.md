# References
* [Online quiz](https://www.coursera.org/learn/python-machine-learning/exam/J7A0M/module-4-quiz)

# Questions & Answers
## Item 1
Which of the following is an example of clustering?
1. Accumulate data into groups based on labels
2. Separate the data into distinct groups by similarity
3. Creating a new representation of the data with fewer features
4. Compress elongated clouds of data into more spherical representations

Answer: 2

## Item 2
Which of the following are advantages to using decision trees over other models? (Select all that apply)
1. Trees are easy to interpret and visualize
2. Trees often require less preprocessing of data
3. Trees are naturally resistant to overfitting
4. Decision trees can learn complex statistical models using a variety of kernel functions

Answer: 1, 2

## Item 3
What is the main reason that each tree of a random forest only looks at a random subset of the features when building each node?
1. To increase interpretability of the model
2. To learn which features are not strong predictors
3. To improve generalization by reducing correlation among the trees and making the model more robust to bias.
4. To reduce the computational complexity associated with training each of the trees needed for the random forest.

Answer: 3

## Item 4
Which of the following supervised machine learning methods are greatly affected by feature scaling? (Select all that apply)
1. KNN
2. Support Vector Machines
3. Naive Bayes
4. Decision Trees
5. Neural Networks

[x](0/1) Answer: 1
[x](0/1) Answer: 3, 5
[x](0/1) Answer: 2

## Item 5
Select which of the following statements are true.
1. For predicting future sales of a clothing line, Linear regression would be a better choice than a decision tree regressor.
2. For having an audience interpret the fitted model, a support vector machine would be a better choice than a decision tree.
3. For a model that won’t overfit a training set, Naive Bayes would be a better choice than a decision tree.
4. For a fitted model that doesn’t take up a lot of memory, KNN would be a better choice than logistic regression.

Answer: 1, 3

## Item 6
Match each of the prediction probabilities decision boundaries visualized below with the model that created them.
1. Neural Network; KNN (k=1); Decision Tree
2. KNN (k=1); Decision Tree; Neural Network
3. Neural Network; Decision Tree; KNN (k=1)
4. KNN (k=1); Neural Network; Decision Tree

Answer: 1 (KNN is diagram #2)

## Item 7
A decision tree of depth 2 is visualized below. Using the `value` attribute of each leaf, find the accuracy score for the tree of depth 2 and the accuracy score for a tree of depth 1.
What is the improvement in accuracy between the model of depth 1 and the model of depth 2? (i.e. accuracy2 - accuracy1)

[x](0/1) Answer: 0.5
[x](0/1) Answer: 0.2
[x](0/1) Answer: 0.8

## Item 8
For the autograded assignment in this module, you will create a classifier to predict whether a given blight ticket will be paid on time (See the module 4 assignment notebook for a more detailed description). Which of the following features should be removed from the training of the model to prevent data leakage? (Select all that apply)
1. ticket_issued_date - Date and time the ticket was issued
2. grafitti_status - Flag for graffiti violations
3. compliance_detail - More information on why each ticket was marked compliant or non-compliant
4. agency_name - Agency that issued the ticket
5. collection_status - Flag for payments in collections

[x](0/1) Answer: 4
[x](0/1) Answer: 1
[x](0/1) Answer: 1, 4

## Item 9
Which of the following might be good ways to help prevent a data leakage situation?
1. If time is a factor, remove any data related to the event of interest that doesn’t take place prior to the event.
2. Ensure that data is preprocessed outside of any cross validation folds.
3. Remove variables that a model in production wouldn’t have access to
4. Sanity check the model with an unseen validation set

[x](0/1) Answer: 2
[x](0/1) Answer: 3
[x](0/1) Answer: 2, 4

## Item 10
Question 10
Given the neural network below, find the correct outputs for the given values of x1 and x2.

The neurons that are shaded have an activation threshold, e.g. the neuron with >1? will be activated and output 1 if the input is greater than 1 and will output 0 otherwise.
1. x1 x2 output
    0  0  1
    0  1  0
    1  0  0
    1  1  1
2. x1 x2 output
    0  0  0
    0  1  0
    1  0  0
    1  1  1
3. x1 x2 output
    0  0  0
    0  1  1
    1  0  1
    1  1  0
4. x1 x2 output
    0  0  0
    0  1  1
    1  0  1
    1  1  1

Answer: 3

