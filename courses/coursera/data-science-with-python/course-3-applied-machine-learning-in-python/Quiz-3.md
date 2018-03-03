# References
* [Online quiz](https://www.coursera.org/learn/python-machine-learning/exam/Wxgra/module-3-quiz)
* [Confusion matrix on Wikipedia](https://en.wikipedia.org/wiki/Confusion_matrix)

## Formulas
$$
P = TP + FN
N = TN + FP
Precision = PPV = TP / (TP + FP)
Recall = Sensitivity = TPR = TP / P = TP / (TP + FN)
Accuracy = (TP + TN) / (P + N) = (TP + TN) / (TP + TN + FP + FN)
F1 = 2. (PPV . TPR) / (PPV + TPR) = 2 TP / (2TP + FP + FN)
$$

# Questions & Answers
## Item 1
A supervised learning model has been built to predict whether someone is infected with a new strain of a virus. The probability of any one person having the virus is 1%. Using accuracy as a metric, what would be a good choice for a baseline accuracy score that the new model would want to outperform?

Answer: 0.99 (99%)

## Item 2
Given the following confusion matrix:
|                        | Predicted Positive | Predicted Negative |
|------------------------|--------------------|--------------------|
| Condition Positive (P) |        TP = 96     |        FN =  4     |
| Condition Negative (N) |        FP =  8     |        TN = 19     |

Compute the accuracy to three decimal places.

Accuracy = (TP + TN) / (TP + TN + FP + FN) = (96 + 19) / (96 + 4 + 8 + 19) = 115 / 127 = 0.906

Answer: 0.906

## Item 3
Given the following confusion matrix:
|                        | Predicted Positive | Predicted Negative |
|------------------------|--------------------|--------------------|
| Condition Positive (P) |        TP = 96     |        FN =  4     |
| Condition Negative (N) |        FP =  8     |        TN = 19     |

Compute the precision to three decimal places.

Precision = TP / (TP + FP) = 96 / (96 + 8) = 96 / 104 = 0.923

Answer: 0.923

## Item 4
Given the following confusion matrix:
|                        | Predicted Positive | Predicted Negative |
|------------------------|--------------------|--------------------|
| Condition Positive (P) |        TP = 96     |        FN =  4     |
| Condition Negative (N) |        FP =  8     |        TN = 19     |

Compute the recall to three decimal places.

Recall = TP / (TP + FN) = 96 / (96 + 4) = 96 / 100 = 0.960

Answer: 0.960

## Item 5
Using the fitted model `m` create a precision-recall curve to answer the following question:
For the fitted model `m`, approximately what precision can we expect for a recall of 0.8?

(Use ``y_test`` and ``X_test`` to compute the precision-recall curve. If you wish to view a plot, you can use `plt.show()` )
```python
print(m)
y_scores_m = m.fit(X_train, y_train).decision_function(X_test)
precision, recall, thresholds = precision_recall_curve(y_test, y_scores_m)
plt.figure()
plt.xlim([0.0, 1.01])
plt.ylim([0.0, 1.01])
plt.plot(precision, recall, label='Precision-Recall Curve')
plt.xlabel('Precision', fontsize=16)
plt.ylabel('Recall', fontsize=16)
plt.axes().set_aspect('equal')
plt.show()

LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
          penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
          verbose=0, warm_start=False)
```

Answer: 0.6

## Item 6
Given the following models and AUC scores, match each model to its corresponding ROC curve.
* Model 1 test set AUC score: 0.91
* Model 2 test set AUC score: 0.50
* Model 3 test set AUC score: 0.56
<img src="readonly/Quiz-3-06.png" style="width: 1000px;"/>

1. Model 1: Roc 1 ; Model 2: Roc 2 ; Model 3: Roc 3
2. Model 1: Roc 1 ; Model 2: Roc 3 ; Model 3: Roc 2
3. Model 1: Roc 2 ; Model 2: Roc 3 ; Model 3: Roc 1
4. Model 1: Roc 3 ; Model 2: Roc 2 ; Model 3: Roc 1
5. Not enough information is given.

Answer: 2 (Model 1: Roc 1 ; Model 2: Roc 3 ; Model 3: Roc 2)

## Item 7
Given the following models and accuracy scores, match each model to its corresponding ROC curve.
* Model 1 test set accuracy: 0.91
* Model 2 test set accuracy: 0.79
* Model 3 test set accuracy: 0.72
<img src="readonly/Quiz-3-06.png" style="width: 1000px;"/>

1. Model 1: Roc 1 ; Model 2: Roc 2 ; Model 3: Roc 3
2. Model 1: Roc 1 ; Model 2: Roc 3 ; Model 3: Roc 2
3. Model 1: Roc 2 ; Model 2: Roc 3 ; Model 3: Roc 1
4. Model 1: Roc 3 ; Model 2: Roc 2 ; Model 3: Roc 1
5. Not enough information is given.

Answer: 5 (ROC 3 curve corresponds to a model with accuracy 0.50, and ROC 3 curve corresponds to a model with accuracy 0.56)

## Item 8
Using the fitted model `m` what is the macro precision score?

(Use ``y_test`` and ``X_test`` to compute the precision score.)
```python
print(m)
svm_predicted = m.predict(X_test)
precision = precision_score(y_test, svm_predicted, average = 'macro')
print ('Macro precision score: {:.3f}'.format(precision))

SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0,
  decision_function_shape=None, degree=3, gamma='auto', kernel='rbf',
  max_iter=-1, probability=False, random_state=None, shrinking=True,
  tol=0.001, verbose=False)
```

Answer: 0.805

## Item 9
Which of the following is true of the R-Squared metric? (Select all that apply)
1. A model that always predicts the mean of y would get a score of 0.0
2. The worst possible score is 0.0
3. The best possible score is 1.0
4. A model that always predicts the mean of y would get a negative score

Answer: 1, 3

## Item 10
In a future society, a machine is used to predict a crime before it occurs. If you were responsible for tuning this machine, what evaluation metric would you want to maximize to ensure no innocent people (people not about to commit a crime) are imprisoned (where crime is the positive label)?
1. Accuracy
2. Precision
3. Recall
4. F1
5. AUC

Answer: 2

## Item 11
Consider the machine from the previous question. If you were responsible for tuning this machine, what evaluation metric would you want to maximize to ensure all criminals (people about to commit a crime) are imprisoned (where crime is the positive label)?
1. Accuracy
2. Precision
3. Recall
4. F1
5. AUC

Answer: 3

## Item 12
A classifier is trained on an imbalanced multiclass dataset. After looking at the model’s precision scores, you find that the micro averaging is much smaller than the macro averaging score. Which of the following is most likely happening?
1. The model is probably misclassifying the frequent labels more than the infrequent labels.
2. The model is probably misclassifying the infrequent labels more than the frequent labels.

Answer: 1 (The model is probably misclassifying the frequent labels more than the infrequent labels)

## Item 13
Using the already defined RBF SVC model `m`, run a grid search on the parameters C and gamma, for values [0.01, 0.1, 1, 10]. The grid search should find the model that best optimizes for recall. How much better is the recall of this model than the precision? (Compute recall - precision to 3 decimal places)

(Use ``y_test`` and ``X_test`` to compute precision and recall.)
```python
print(m)

grid_values = {'C': [0.01, 0.1, 1, 10], 'gamma': [0.01, 0.1, 1, 10]}
grid_clf_rec = GridSearchCV(m, param_grid = grid_values, scoring = 'recall')
grid_clf_rec.fit(X_train, y_train)
y_decision_fn_scores_rec = grid_clf_rec.decision_function(X_test)
recall = grid_clf_rec.best_score_

svm = SVC(kernel='rbf', C=0.01, gamma=0.01).fit(X_train, y_train)
svm_predicted = svm.predict(X_test)
precision = precision_score(y_test, svm_predicted)

print('Grid best parameter (max. recall): ', grid_clf_rec.best_params_)
print('Grid best score (recall): ', recall)
print('Precision: {:.3f}; recall: {:.3f}'.format(precision, recall))
print('recall - precision: {:.3f}'.format(recall - precision))

SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0,
  decision_function_shape=None, degree=3, gamma='auto', kernel='rbf',
  max_iter=-1, probability=False, random_state=0, shrinking=True,
  tol=0.001, verbose=False)
```

Answer: 0.520

## Item 14
Using the already defined RBF SVC model `m`, run a grid search on the parameters C and gamma, for values [0.01, 0.1, 1, 10]. The grid search should find the model that best optimizes for precision. How much better is the precision of this model than the recall? (Compute precision - recall to 3 decimal places)

(Use ``y_test`` and ``X_test`` to compute precision and recall.)
```python
print(m)

grid_values = {'C': [0.01, 0.1, 1, 10], 'gamma': [0.01, 0.1, 1, 10]}
grid_clf_pre = GridSearchCV(m, param_grid = grid_values, scoring = 'precision')
grid_clf_pre.fit(X_train, y_train)
y_decision_fn_scores_pre = grid_clf_pre.decision_function(X_test)
precision = grid_clf_pre.best_score_

svm = SVC(kernel='rbf', C=10, gamma=1).fit(X_train, y_train)
svm_predicted = svm.predict(X_test)
recall = recall_score(y_test, svm_predicted)

print('Grid best parameter (max. precision): ', grid_clf_pre.best_params_)
print('Grid best score (precision): ', precision)
print('Precision: {:.3f}; recall: {:.3f}'.format(precision, recall))
print('precision - recall: {:.3f}'.format(precision - recall))

SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0,
  decision_function_shape=None, degree=3, gamma='auto', kernel='rbf',
  max_iter=-1, probability=False, random_state=0, shrinking=True,
  tol=0.001, verbose=False)
```

Answer: 0.158
