---
layout: post
title:      "Imbalanced Data "
date:       2020-04-25 17:59:43 +0000
permalink:  imbalanced_data
---


I've said before the world is an imperfect place.  Not all distributions are Gaussian, symmetrical and perfect in samples or populations.  In machine learning,  classification is a supervised learning appraoch in which the computer program learns from the data and make new observations or 'classifications' by using targets, or 'classes'.

For each sample,  classes are assigned.  For example, those who test positive for a disease are assigned a class of '1', those who test negative are assigned '0' .  Classes can be numeric or non-numeric, but for the sake of this example - numeric it is!  These classes each have a set of accompanying data.  To continue building on this example; the biological, behavioral and environmental data that are associated each are evaluated using an appropriate algorithm.  This is called training a model - the model looks at which factors more frequently align and when with a given class and used to predict future or unseen data.  This predictive modeling is used to inform future decision making.

What happens when the model is trained with many more cases of people testing negative than positive - let's say a ration of 100 to 1, 1,000 to 1,000,000 or 1?  Just like training anything else, the more training spent on learnsomething- the better the task is learned.  Too much training leads to 'overtraining' or bias.  Models that learn more of one thing will by nature predict more cases of this class.  

Imbalance happens often and there are ways it can be approached to help properly train a model.   One way is to try to obtain more samples.  In the real world, this is impractical due to financial and time constraints.  Alternatively we can take random samples of the data to create equal class sizes to help our model lean both classes equally , thereby generating unbiased predictions for new classifications.  A few of the most widely used strategies are offered below:

**Random Undersampling.** Back to our disease testing example; Let's say we have results where 300 cases tested negative so they fall into the '0' class, and 25 cases of postive tests.  We would randomly sample 25 cases from the negative class and use this for testging and training our model.  As you might guess, we would miss out on 275 cases where we could miss something in predicting accurately in future cases.  

**Randonm Oversampling**   A clustering algorithm based on similar or neighboring data is independently applied to each class to look for similarites. After this, each cluster is oversampled such that all clusters of the same class have an equal number of instances and all classes have the same size.  This presents a possiblity for overtraining the data as well since the samples are re-used, and in cases many times - thereby generating bias. However, we lose no data in this case.

**SMOTE or Synthetic Minority Oversampling Technique**  This strategy is executed to avoid overfitting which occurs when exact replicas of minority instances are added to the main dataset. A subset of data is taken from the minority class as an example then new synthetic similar instances are created. These synthetic instances are then added to the original dataset. The new dataset is used as a sample to train the classification models.   While again, no data is lost since the neighboring data is taken into account and overlap of information can occur or  'noise'.  

SMOTE does not consider the underlying distribution of the minority class and latent noises in the dataset. To improve the performance of SMOTE a modified method MSMOTE is used.

**MSMOTE** Modified smote applies the k nearest neighbors algorithm used in oversampling and divides the minority sample into three groups: *'safe'*, (those that can improve the performance) ,*'latent'*, (those that penalize performance) and *'border'* (scored inbetween 'safe' and 'latent') samples.  The flow is similar to SMOTE mentioned above but using the algorithm randomly selects a data point from the k nearest neighbors for the safe sample, selects the nearest neighbor from the border samples and does nothing for latent noise.

When faced with imbalanced data sets,there is no one single solution to improve the accuracy of the prediction model.  Each of these methodologies have their strengths and weaknesses and can help to initially balance the training data that is loaded into the model - and different methods should be tested to see what works best. In most cases, synthetic techniques like SMOTE and MSMOTE will outperform the conventional oversampling and undersampling methods.  Also within most ensenble training models used for classification, there are parameters to tune that take into account and generate balanced cases as well to maxmize the effects of pre-processing the training set.  These are for another day.  Until then, stay balanced my friends.
