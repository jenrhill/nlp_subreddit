# Project 3 - Web APIs & Classification

### Problem Statement 

The hosts of the My Favorite Murder podcast would like to know if it’s possible to predict if a piece of content was posted on the True Crime subreddit or on their subreddit. Natural Language Processing was used to convert the text to numeric values, then the data was tested on three model types: Logistic Regression, Naive Bayes, and Support Vector Machine. Success was measured by accuracy.

---

### Executive Summary

My approach was to first scrape the data from each subreddit and review what I was able to pull in. Then I dove into cleaning. I set all the characters to lowercase and I used Beautiful Soup to strip out any odd html tags. I used regex to remove punctuation. As part of this cleaning I tested various text normalization techniques to see if lemmatizing, two different stemmers, or none would work better. I found they all gave me similar results, but lemmatizing helped bring my training and test scores slightly closer together, which was helpful when trying to make my models less overfit. 

The next part in this cleaning process that I tested were stop words. I tried testing stripping the English stopwords, None, and using English plus a custom list. I had noticed a few things when pulling the most popular words. Murder, crime, and true showed up high on both subreddits. Also, urls that were shared in the selftext showed up as pieces (https, com, www). Plus there were few really popular conversational terms in the top that were not included in English (like and know) so I added them too. I found that the English+ stopwords option worked best with making my models have stronger test scores and be less overfit.  

For the models, I set up pipelines to test four baseline variations of logistic regression, naive bayes, and support vector machine. I wanted to test X being either just the title or the title & selftext. I couldn’t test selftext on its own because not every post has that available. I also wanted to test CountVectorizer vs TfidVectorizer. Once I tested all the cleaning related factors on my baselines, I moved on to testing parameters.

From here, I did the same sort of step by step with adding on features, in this case parameters. What I found was that the more parameters I added in to test, the worse my scores got and the differentiation between the train and test score increased. What I had to do was go back to the basics, and ended up honing in on max features as my sole parameter. Dropping the number of features helped the scores, but dropping too far would make the gap between train and test scores increase again. 

---

### Conclusion

My best model was able to predict placement of content on the True Crime subreddit vs. the My Favorite Murder subreddit with an accuracy of 86%, and that was well above the baseline accuracy score of 51.8%. That's why I would recommend the Naive Bayes model as the one to use here, with lemmatization, English plus a custom list for stopwords, and TfidVectorizer options. However, the caveat I would add is that Reddit content changes daily. What that means is that accuracy can and will change based on what content is available on any particular day you. The model will need to be adjusted accordingly with updating what stopwords are included and fine tuning the max feature value for TfidVectorizer.


---

### Source Documentation

- [r/TrueCrime](https://www.reddit.com/r/TrueCrime/)
- [r/myfavoritemurder](https://www.reddit.com/r/myfavoritemurder/)
- [True Crime Scraped Data](./datasets/true_crime_df.csv)
- [My Favorite Murder Scraped Data](./datasets/fav_murder_df.csv)
- [Combined Subreddits Data](./datasets/df_combined.csv)
- [Combined Subreddits Data with Feature Engineering](./datasets/clean_df_combined.csv)
