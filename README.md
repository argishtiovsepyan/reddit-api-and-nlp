# **Subreddit Classifier:**
## "AskScience" or "ExplainLikeImFive"

<p align="center">
<img src= "images/Poster.jpg">
</p>

I am classifying Reddit posts as either scientific explanations from "AskScience" or simplified explanations from "explainlikeimfive" based on the language used in the posts. By discerning complex and layman questions, these models aim to enhance the user experience by facilitating access to information in users' preferred level of detail. This differentiation will benefit businesses by enabling personalized content delivery and improved customer support based on users' information needs and understanding.


| Column Name       | Type    | Description                                         |
|-------------------|---------|---------------------------------------------------- |
| time              | float64 | The timestamp of the post in a numerical format.    |
| title             | object  | The title of the post.                              |
| text              | object  | The text content of the post.                       |
| upvotes           | float64 | The upvote ratio received for the post.             |
| comments          | int64   | The number of comments received for the post.       |
| sub               | int64   | The subreddit ID.                                   |
| title_word_count  | int64   | The number of words in the title of the post.       |
| text_word_count   | int64   | The number of words in the text of the post.        |
| sentiment         | float64 | The sentiment score of the post content.            |
| title_tokens      | object  | The tokenized representation of words in the title. |
| text_tokens       | object  | The tokenized representation of words in the text.  |


#### Executive Summary

This project leverages the Python Reddit API Wrapper (PRAW) to extract a vast collection of Reddit posts, forming the basis for a machine learning model that distinguishes between complex (sourced from 'AskScience') and simple ('ELIF') questions. Thousands of posts were acquired, duplicates removed, and a master dataframe created for modeling purposes. The data obtained is well-balanced, eliminating the concern for class imbalance.

A number of pre-processing steps were carried out, including removing tags, replacing missing texts, and conducting sentiment analysis. Additionally, I performed tokenization, stemming, lemmatization, and stop-word removal on title and text columns to facilitate the model's predictions.

Initially, adding common words to the stop words list was considered. However, it was found that maintaining the full unedited post improved the model's performance, as it retained more contextual information vital for discerning between complex and layman questions.

A variety of machine learning models were explored, including Multinominal Naive Bayes, Random Forest, and Logistic Regression. Through hyperparameter tuning via GridSearchCV, Logistic Regression demonstrated superior performance, particularly with ridge-like regularization.

Key parameters identified were no limit on max features, a minimum document frequency of 1, maximum document frequency of 0.4, n-gram range of (1,3), no stop words, a moderate regularization strength of 1, and using the liblinear solver.

The final model significantly outperformed the baseline score of 0.5, achieving an impressive 0.92 ROC AUC score. This suggests a robust ability to balance true positives and false positives effectively, indicating excellent classification potential. The model's ability to discern user input complexity and respond appropriately can prove highly beneficial for businesses aiming to deliver personalized content and customer support.

For future iterations, there is scope to experiment with other models like KNN, SVM, Gradient Boosting, and Ada Boosting. Inclusion of additional features or combining the title and text columns may also enhance the understanding of full context and improve model performance.
