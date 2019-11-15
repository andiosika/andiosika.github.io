---
layout: post
title:      "Categorical Data "
date:       2019-11-15 13:15:45 -0500
permalink:  categorical_data
---


In our first project for the online Data Science program, we were asked to predict home values based on 21 features from a dataset provided to us.  Armed with my initial skills learned in the first module, I anxiously downloaded the dataset.   I began exploring the data – I noticed that some of the data was categorized as objects, some integers, some floats… All features ended up being numeric! Sweet.  This will be easy to analyze. Until I realized not all numbers are created equal.  
Numbers can mean different things: a 1 or a 0 can represent ‘True’ or ‘False’.  The number ‘4’ can represent a value, a geographic point, size, or a score.  When you read: 85018 it can represent eighty-five thousand, eighteen or a zip code – a label that represents a geographic area.  In this case, numbers don’t carry a value but they can still be used, as can other types of data that are not numeric.   They are considered categorical. Categorical data is that which values are assigned to a finite set of features – like in the case of zipcodes.
Yes… back to zipcodes.   In this project, I was stuck on this one.  It was numeric and ordinal… I thought since there’s a hierarchy to it had some sort of value.  However: 85018 + 85019 does not yield something that is predictive … or is it? Is there even a zipcode 170037?  Answer: Yes… but do two Arizona zip codes added together really equal Beijing?  Another post I guess… But,  this was when it made sense to me.  The number assigned to a geographic area represents a category – it’s a label.  How this category relates to other variables is how we could use it in a predictive way rather than the value it represents.  This happens after we label encode it – or assign it a numeric value that can be used as a relative value.
There are different ways one can go about label-encoding for predictive modeling.  
One way is to pass .cat.codes through your feature that assigns a numeric value to your numeric, text or even photographic category:

'0      feat2
1      feat1
2      feat1
3      feat0
4      feat2
5      feat1
6      feat1
dtype: category'

feature.cat.codes
OUTPUT:
0    2
1    1
2    1
3    0
4    2
5    1
6    1
7    0
8    0
9    2
dtype: int8  

See?  It's now an integer that relates back to the feature.

Another way is to use the scikitlearn’s  LabelEncoder:
First import, then encatonate, then call fit_transform  to feature you’re encoding.  

from sklearn.preprocessing import LabelEncoder
encode = LabelEncoder()
feature_encoded = encode.fit_transform(cat_feature)


feature_encoded
array([2, 1, 1, 0, 2, 1, 1, 0, 0, 2])


Or you can do this another way, by getting “dummy variables” from pandas:

pd.get_dummies(cat_origin)

	Val1	Val2	Val3
0	0	0	1
1	0	1	0
2	0	1	0
3	1	0	0
4	0	0	1
5	0	1	0
6	0	1	0
7	1	0	0
8	1	0	0
9	0	0	1

The advantage of using dummies is that, whatever algorithm you'll be using, your numerical values cannot be misinterpreted as being continuous. Going forward, it's important to know that for linear regression (and most other algorithms in scikit-learn), one-hot encoding is required when adding categorical variables in a regression model.

One thing to keep in mind when using dummies: it interferes with multicollinearity and something called “the dummy trap”.  This idea at first perplexed me – but basically you can predict any single origin dummy variable using the implied information from the others.  All categories that are being compared to each other are assigned a zero or a one sequentially.  By having all variables compared to each other will add more values than makes sense to interpret.  Fortunately, these issues can be avoided by simply dropping one of the dummy variables. You can do this by subsetting the dataframe manually or, more conveniently, by passing drop_first=True to get_dummies():

Once you have this down… keep going.  
Clean the data. Ask questions.  Use the data to build a model, make observations, predictions and suggestions based on your findings. Then use visualizations to communicate what you’ve discovered.






