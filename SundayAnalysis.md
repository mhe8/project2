Project 2: predictive models
================
Min He
July 2, 2020 (updated 2020-07-03)

# Project report for Sunday

## Introduction about the data

This dataset summarizes a heterogeneous set of features about articles
published by Mashable in a period of two years. The goal is to predict
the number of shares in social networks (popularity).
[source](https://archive.ics.uci.edu/ml/datasets/Online+News+Popularity).
In this project, I will try to use the logistic regression and bagging
to classify whether the shares exceeds 1400 or not.

It includes the following columns:

0.  url: URL of the article (non-predictive)
1.  timedelta: Days between the article publication and the dataset
    acquisition (non-predictive)
2.  n\_tokens\_title: Number of words in the title
3.  n\_tokens\_content: Number of words in the content
4.  n\_unique\_tokens: Rate of unique words in the content
5.  n\_non\_stop\_words: Rate of non-stop words in the content
6.  n\_non\_stop\_unique\_tokens: Rate of unique non-stop words in the
    content
7.  num\_hrefs: Number of links
8.  num\_self\_hrefs: Number of links to other articles published by
    Mashable
9.  num\_imgs: Number of images
10. num\_videos: Number of videos
11. average\_token\_length: Average length of the words in the content
12. num\_keywords: Number of keywords in the metadata
13. data\_channel\_is\_lifestyle: Is data channel ‘Lifestyle’?
14. data\_channel\_is\_entertainment: Is data channel ‘Entertainment’?
15. data\_channel\_is\_bus: Is data channel ‘Business’?
16. data\_channel\_is\_socmed: Is data channel ‘Social Media’?
17. data\_channel\_is\_tech: Is data channel ‘Tech’?
18. data\_channel\_is\_world: Is data channel ‘World’?
19. kw\_min\_min: Worst keyword (min. shares)
20. kw\_max\_min: Worst keyword (max. shares)
21. kw\_avg\_min: Worst keyword (avg. shares)
22. kw\_min\_max: Best keyword (min. shares)
23. kw\_max\_max: Best keyword (max. shares)
24. kw\_avg\_max: Best keyword (avg. shares)
25. kw\_min\_avg: Avg. keyword (min. shares)
26. kw\_max\_avg: Avg. keyword (max. shares)
27. kw\_avg\_avg: Avg. keyword (avg. shares)
28. self\_reference\_min\_shares: Min. shares of referenced articles in
    Mashable
29. self\_reference\_max\_shares: Max. shares of referenced articles in
    Mashable
30. self\_reference\_avg\_sharess: Avg. shares of referenced articles in
    Mashable
31. weekday\_is\_monday: Was the article published on a Monday?
32. weekday\_is\_tuesday: Was the article published on a Tuesday?
33. weekday\_is\_wednesday: Was the article published on a Wednesday?
34. weekday\_is\_thursday: Was the article published on a Thursday?
35. weekday\_is\_friday: Was the article published on a Friday?
36. weekday\_is\_saturday: Was the article published on a Saturday?
37. weekday\_is\_sunday: Was the article published on a Sunday?
38. is\_weekend: Was the article published on the weekend?
39. LDA\_00: Closeness to LDA topic 0
40. LDA\_01: Closeness to LDA topic 1
41. LDA\_02: Closeness to LDA topic 2
42. LDA\_03: Closeness to LDA topic 3
43. LDA\_04: Closeness to LDA topic 4
44. global\_subjectivity: Text subjectivity
45. global\_sentiment\_polarity: Text sentiment polarity
46. global\_rate\_positive\_words: Rate of positive words in the content
47. global\_rate\_negative\_words: Rate of negative words in the content
48. rate\_positive\_words: Rate of positive words among non-neutral
    tokens
49. rate\_negative\_words: Rate of negative words among non-neutral
    tokens
50. avg\_positive\_polarity: Avg. polarity of positive words
51. min\_positive\_polarity: Min. polarity of positive words
52. max\_positive\_polarity: Max. polarity of positive words
53. avg\_negative\_polarity: Avg. polarity of negative words
54. min\_negative\_polarity: Min. polarity of negative words
55. max\_negative\_polarity: Max. polarity of negative words
56. title\_subjectivity: Title subjectivity
57. title\_sentiment\_polarity: Title polarity
58. abs\_title\_subjectivity: Absolute subjectivity level
59. abs\_title\_sentiment\_polarity: Absolute polarity level
60. shares: Number of shares in social media (this is the dependent
    variable)

## Read in the news popularity data

## Data preprocessing

  - Combine the weekday flags into one variable `news_day`, e.g.: when
    `weekday_is_monday`=1, set the `news_day`=‘Monday’
  - Combine the topic channels into one variable `data_channel`, e.g.:
    when `data_channel_is_lifestyle`=1, set the
    `data_channel`=‘lifestyle’
  - Dividing the shares into two groups (\< 1400 and ≥ 1400)

### Variables

  - Those non-predictive variables (url and timedelta) won’t be included
    in the model.
  - As in each model, we only use a subset of data (e.g.: Monday only),
    the weekday\_is\_monday, weekday\_is\_tuesday … will be combined
  - Basically, the vairables can be classified into the following
    classes
      - number of tokens (in title, content, keywords, stops, non-stops)
      - number of media in the article ( images, videos)
      - words characteristics (polarity, subjectivity, polarity,
        negative, positive, sentiment)
      - reference characteristics (shares of referenced, href)

## Clearing data

  - Remove the unused/non-predictive variables
  - Remove outliers (e.g.: n\_tokens\_content\<=0)
  - Subset the records to the day defined by the argument

## Divide dataset into training v.s. testing datasets

  - Set random seeds so that the results can be replicated
  - Break the dataset into 70% for training v.s. 30% for testing

## Data summary and exploratory analysis

### Boxplot for some of the key variables to identify the outliers

![](SundayAnalysis_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

### Scatterplot of the shares v.s. some othe key variables to identify the linear relationship (although we are using logistic linear regression, but the scatterplot is still useful to identify the patterns)

![](SundayAnalysis_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

### Histogram for key variables, it’s a good way to check the distribution (whether it’s normal distribution or not)

![](SundayAnalysis_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->![](SundayAnalysis_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

## Train the predictive model by using logistic regression

  - Use both direction (forwards and backwards) stepwise methods to pick
    up the predict variables
  - AIC is used as the criterion to pick the best combination of predict
    variables
  - AIC estimates the relative amount of information lost by a given
    model: the less information a model loses, the higher the quality of
    that model. (excerpted from [linked
    wiki](https://en.wikipedia.org/wiki/Akaike_information_criterion))

## Predict the value for test dataset with the trained logistic model

  - If the predicted response is larger than 0.5, then it’s
    shares\>=1400
  - Calculate/print the confusion matrix

<!-- end list -->

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction FALSE TRUE
    ##      FALSE    76   72
    ##      TRUE    156  494
    ##                                           
    ##                Accuracy : 0.7143          
    ##                  95% CI : (0.6816, 0.7454)
    ##     No Information Rate : 0.7093          
    ##     P-Value [Acc > NIR] : 0.3944          
    ##                                           
    ##                   Kappa : 0.2243          
    ##                                           
    ##  Mcnemar's Test P-Value : 3.867e-08       
    ##                                           
    ##             Sensitivity : 0.32759         
    ##             Specificity : 0.87279         
    ##          Pos Pred Value : 0.51351         
    ##          Neg Pred Value : 0.76000         
    ##              Prevalence : 0.29073         
    ##          Detection Rate : 0.09524         
    ##    Detection Prevalence : 0.18546         
    ##       Balanced Accuracy : 0.60019         
    ##                                           
    ##        'Positive' Class : FALSE           
    ## 

## Train the predictive model by using random forest

  - Set number of trees to be 200

## Predict the value for test dataset with the trained bagging model

  - If the predicted response is larger than 0.5, then it’s
    shares\>=1400
  - Calculate/print the confusion matrix

<!-- end list -->

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction FALSE TRUE
    ##      FALSE    73   70
    ##      TRUE    159  496
    ##                                           
    ##                Accuracy : 0.713           
    ##                  95% CI : (0.6803, 0.7442)
    ##     No Information Rate : 0.7093          
    ##     P-Value [Acc > NIR] : 0.4248          
    ##                                           
    ##                   Kappa : 0.2154          
    ##                                           
    ##  Mcnemar's Test P-Value : 6.056e-09       
    ##                                           
    ##             Sensitivity : 0.31466         
    ##             Specificity : 0.87633         
    ##          Pos Pred Value : 0.51049         
    ##          Neg Pred Value : 0.75725         
    ##              Prevalence : 0.29073         
    ##          Detection Rate : 0.09148         
    ##    Detection Prevalence : 0.17920         
    ##       Balanced Accuracy : 0.59549         
    ##                                           
    ##        'Positive' Class : FALSE           
    ## 

## Conclusion

The bagging methods are using classification trees.

  - Create a bootstrap sample (same size as actual sample)
  - Train tree on this sample
  - Repeat B = 1000 times
  - The voting method will be applied to pick which class it will
    belong.

The results obtained from the bagging and logistic regression show
similar accuracy, and it’s about 63% of accuracy for Monday only data.
