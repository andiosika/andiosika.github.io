---
layout: post
title:      "Statistical Hypothesis Testing Alert : Not all data is created normal. "
date:       2020-02-17 21:56:56 -0500
permalink:  statistics_hypothesis_testing_alert_not_all_data_is_created_nomal
---


Hypothesis testing is a vital part of statistics.  It essentially takes two statements and evaluates which the sample data best supports statistically.  The results determine if there is significance.  Real, measurable and quantifiable significance.

The basis of hypothesis testing has to do with comparing averages or means.   It allows us quantify the probability that our sample mean is unusual when compared to that of the population.   How unusal is in comparison is what tells us if we can reject the null hypothesis - or what is currently accepted as 'normal'.   

The ojective is simple enough - comparing two means.  However,  in our most recent project, I found that  this dataset was much like real life: not 'normal'.  I found that selection of which testing methodology to apply is crucial for an accurate result and that a null hypothesis can be falsely rejected, completely defeating the purpose of testing in the first place. 


Parametric tests are what are typically used in hypothesis testing and are described for the most part in what has been explained.   They compare the means of the sample group with that of the population.   However, they should only be implemented when the data being tested meets certain assumptions. Because parametric tests rely on the [central limit theory](http://http://sphweb.bumc.bu.edu/otlt/MPH-Modules/BS/BS704_Probability/BS704_Probability12.html) they require the following assumptions:

1. Data must be numeric
2. Data must be normally distributed
3. No Significant Outliers
4. In the case of more than two samples, they must have equal variance.


However, the world is an imperfect place.  Datasets are small, skewed, categorical or ordinal in nature.  They can be proven as such with tests like [D'Agostino-Pearson's normality test](https://en.wikipedia.org/wiki/D%27Agostino%27s_K-squared_test), or [Shapiro-Wilik Test](https://www.statisticshowto.datasciencecentral.com/shapiro-wilk-test/) for normality and [Levene's Test](https://www.statisticshowto.datasciencecentral.com/levene-test/) for equal variance.   Enter the non-parametric tests.  These tests find ways around the 'non-normal' data and provide a more accurate result in determining if the sample is unusual - significantly so. 

Reasons to use non-parametric tests:
1. Your data is skewed or better represented by the median
2. You have a small sample size
3. You have to keep your outliers - example, your sample size is too small. 
4. You have ordinal or categorical data.

Non parametric tests will use the median as one way to determine if the sample is unusual.  Below is a summary table that outlines at a high level the various test options.  The first row illustrates one-sample tests, the second - is for comparing two samples , and the third row - for three or more samples to be compared.

**Summary Table - Hypothesis Testing Functions:**
Parametric tests (means)|	Function|	Nonparametric tests (medians) | 	Function
|--- | --- | ---| ---|
1-sample t test	\ scipy.stats.ttest_1samp()	| 1-sample Wilcoxon	| scipy.stats.wilcoxon
2-sample t test	| scipy.stats.ttest_ind()	|Mann-Whitney U test|	scipy.stats.mannwhitneyu()|
One-Way ANOVA|	scipy.stats.f_oneway()	|Kruskal-Wallis|	scipy.stats.kruskal


Post-hoc testing like a [Cohen's d](http://https://www.socscistatistics.com/effectsize/default3.aspx) can further assess the effect size and I've found, prove additional efficacy of hypotheis testing.

In my series of testing, a preliminary visual examination using exploratory data analysis, illustrated the possiblity that I could  reject the null hypothesis.  Excited that I was on the right track, I continued my evaluation of the data which demonstrated to be not of equal variance.  I proceeded with a non-parametric test ( Kruskal-Wallis[](http://https://statistics.laerd.com/spss-tutorials/kruskal-wallis-h-test-using-spss-statistics.php) ) which returned a result that I could NOT reject the null hypothesis.  Shocked, and despite not meeting the assumptions, I defiantley ran a parametric test and - ha! I got my result I expected/wanted: reject the null hypothesis.  However, in post-hoc testing effect sizes and adjusted p-values proved the non-parametric test was the accurate assessment.  That a non-parametric test yeilded an accurate result.

Once again, I learned the lesson to let the data tell the story.  It doesn't lie.


