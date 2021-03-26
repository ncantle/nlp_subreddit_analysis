SUBREDDIT NLP ANALYSIS
=
## r/Politics and r/Conservative Text Predictive Modeling

### PROBLEM STATEMENT
Using two subreddits based on U.S. politics, this project aims to use NLP to predict whether or not a news headline was published by a conservative-leaning or liberal-leaning news source. The two subreddits selected represent both sides of the political spectrum, but cover (roughly) the same news topics. This analysis hopes to understand the relationship between the words used in a headline and the political leaning of its source.

### DATASETS

- politics.csv : Contains scraped data for 200 days of posts on the r/Politics subreddit
- conservative.csv : Contains scraped data for 200 days of posts on the r/Conservative subreddit
- polcon.csv : Contains cleaned data compiled of politics.csv and conservative.csv for analysis

### SUMMARY AND CONCLUSIONS 

The two subreddits, r/Politics and r/Conservative, represent a collection of news articles from the left and right side of the spectrum in U.S. politics, respectively. These subreddits are useful, since each individual post is comprised solely of the title of a news article with a link to the article (no commentary or original ideas from the actual original poster). This analysis used a series of classification models to aim to predict the political leaning of a headline based on the text it contains.

The classification models used are :
- Logistic Regression
- k-Nearest Neighbors
- Random Forest
- Multinomial Naive Bayes
- Gradient Boosting

For each model, a GridSearch was fit through a selection of hyperparameters, and the text was vectorized with the TfidfVectorizer (except for one instance, where Multinomial Naive Bayes was run with both TfidfVectorizer and CountVectorizer) as I felt this Vectorizer would do a better job at handling the amount of overlap between the two subreddits.

The accuracy scores (on test data) for each model were as follows:

|model|accuracy|
|---|---|
|null model|0.55|
|k-Nearest Neighbors|0.577|
|g_boost|0.629|
|logistic regression|0.685|
|random_forest|0.686|
|multinomialNB|0.698|

Ultimately, MultinomialNB performed the best on this set of data. In addition to achieving the highest accuracy score on the test data and being less overfit than the other models, MultinomialNB achieved a .76 ROC-AUC score, which I found to be satisfactory considering the obvious overlap between the text of the two subreddits. I was unsure that any of these models would be able to achieve any significant increase in accuracy compared to the null model, so a near 15% increase in accuracy is more than acceptable.

I did some modeling on the side with some of the other data included in the original dataframe (like number of comments, score, and word count) and was unable to surpass these NLP models (while some came close). Future analysis may want to look more at the numerical statistics of Reddit posts, as this would be far less computationally-expensive and likely more interpretable. It would also allow for more feature engineering, which could be extremely useful when comparing extremely-similar subreddits. More creative approaches to tweaking hyperparameters (particularly in boost models) could achieve a higher accuracy. 
