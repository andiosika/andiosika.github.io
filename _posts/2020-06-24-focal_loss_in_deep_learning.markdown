---
layout: post
title:      "Focal Loss in Deep Learning "
date:       2020-06-24 18:59:27 -0400
permalink:  focal_loss_in_deep_learning
---


When using machine learning to identify patterns in order predictions and your model yields  an accuracy rate of 99% you are feeling really confident .  Except... when in only 1% of the samples you've used to train your model reflects the one thing you're trying to classify... the target.  That 99% accuracy the model is touting is it's ability to identify the samples that are not the target.  Imbalance happens... and in this case.. despite your high accuracy... your model sucks.

So back to machines ....and how they learn.  Machines learning occurs by means of what's called a  loss function. It's a method of evaluating how well a specific algorithm models the given data. Predictions are made and compared to actual data points. The loss is the difference.  If predictions deviate too much from actual results, loss function would cough up a very large number and vice- versa... so the smaller the loss, the better the model.   'get it?  

Cross-entropy loss is also known as 'log loss'  but no one that I know calls it that.  The cross entropy is calculated by taking the negative log (see the logg loss reference?) of the difference between the actual and predicted values.   It's used in deep learning and measures the performance of a classification model whose output is a probability value between 0 and 1.  Like all loss functions, the farther the predictions are from the real values, the worse the model performs.  

In deep learning models, synapes (think like in a brain) connect neurons in multilayer perceptrons.  These synapses, informed through what's called backpropegation strengthen as they pick up on patterns in the data.  Imbalanced data complicates the matter, especially in the case of multinomial classifications (where there are multiple classes can be predicted from the model) where the model learns the data really well for the target where there is more to learn from and when there is very little to no data... these synapses don't really get formed. 

Enter [Focal Loss](https://focal-loss.readthedocs.io/en/latest/generated/focal_loss.BinaryFocalLoss.html):  
Focal Loss is used to resolve the category imbalance by downweighting easily identified normal data - or the data that the model has tons of.  It's calculated by transforming the cross-entropy (CE) loss function. It's dynamically scaled cross-entropy, where the scaling factor decays to zero as the confidence of the classification increases. Intuitively, this scaling factor can automatically downweight the contribution of normal examples during training, and model training focuses quickly on the hard examples where there's not as much data. 


There are two adjustable parameters for focal loss.

* The focusing parameter γ(gamma) smoothly adjusts the rate at which easy examples are down-weighted. When γ = 0, focal loss is equivalent to categorical cross-entropy, and as γ is increased the effect of the modulating factor is likewise increased (γ = 2 works best in most experiments).

* α(alpha): balances focal loss, yields slightly improved accuracy over the non-α-balanced form.

The equation is :

focal loss = α * loss * (1 - logit) ** γ 

the alpha is multiplied by the loss, then by the value of 1-the log raised to the power of gamma.

I discoved focal loss when working with a dataset with severely imbalanced target classes in a deep neural network.  Since the project was transforming and creating equal sized vectors from text language that was converted into numeric states, SMOTING was not a realisict option.  I have not had susscess with under or over sampling.  So when I ran into a case where I had a recall of 0 in EVERY other model, I was able to achieve a 39% recall - which isn't great, but in a case where the ratio was close to 1000:1 and yeilding a goose-egg, 39% showed promise... heck - it was a 39% increase! 

Further reading:

https://pypi.org/project/focal-loss/
