# **Subreddit Classifier:**
## "AskScience" or "ExplainLikeImFive"

<p align="center">
<img src= "images/Poster.jpg">
</p>

# **Introduction**
Given the numerous parallels observed between the discussions in the subreddits AskScience and ExplainLikeImFive, can the distinction between the two be reliably classified on unseen data? Furthermore, does this classification accuracy persist even when technical terms, such as specific scientific concepts and jargon commonly used in both subreddits, are excluded from the model? Reddit posts are classified as either scientific explanations from 'AskScience' or simplified explanations from 'ExplainLikeImFive' based on the language used in the posts. By discerning complex and layman questions, these models aim to enhance the user experience by facilitating access to information in users' preferred level of detail. This differentiation will benefit businesses by enabling personalized content delivery and improved customer support based on users' information needs and understanding.

# **Data Dictionary**

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

# **Collecting Data**
This project utilizes the Python Reddit API Wrapper (PRAW) to extract a comprehensive dataset of Reddit posts from the subreddits 'AskScience' and 'ExplainLikeImFive' (ELIF). The collection process involves retrieving posts over multiple days to ensure a diverse range of content. After acquiring thousands of posts, duplicates are systematically removed, resulting in a clean dataset for analysis. To ensure the dataset's integrity and balance, careful attention is paid to class distribution, mitigating concerns about class imbalance.

# **NLP and EDA**
Following data acquisition, a series of preprocessing steps are undertaken to prepare the text data for modeling. This includes removing tags, handling missing text entries, and performing sentiment analysis to gain insights into the emotional tone of the posts. Additionally, tokenization, stemming, lemmatization, and stop-word removal are applied to the title and text columns to streamline the data and improve the model's predictive performance. One notable consideration during preprocessing is the decision to retain the full, unedited post content rather than adding common words to the stop words list. This choice was based on the observation that maintaining contextual information enhances the model's ability to differentiate between complex and layman questions effectively.

<p align="center">
<img src= "images/Common Words Historgram.jpg">
</p>

Interestingly, there appears to be a preoccupation with time and water evident in both discussion boards. Initially, I intended to include common words in my stop words list. However, after careful consideration and preliminary testing, it appears that keeping the full, unedited post is yielding better results for my model. The objective here is to distinguish between complex and layman questions, and removing stop words is stripping away too much context.

# **Modeling**
A variety of machine learning models were explored, including Multinominal Naive Bayes, Random Forest, and Logistic Regression. Through hyperparameter tuning via GridSearchCV, Logistic Regression demonstrated superior performance, particularly with ridge-like regularization. Key parameters identified were no limit on max features, a minimum document frequency of 1, maximum document frequency of 0.4, n-gram range of (1,3), no stop words, a moderate regularization strength of 1, and using the liblinear solver.

The final model significantly outperformed the baseline score of 0.5, achieving an impressive accuracy score of 0.92. This suggests a robust ability to balance true positives and false positives effectively, indicating excellent classification potential. The model's ability to discern user input complexity and respond appropriately can prove highly beneficial for businesses aiming to deliver personalized content and customer support.

# **Future Work**
For subsequent iterations, there is scope to experiment with other models like KNN, SVM, Gradient Boosting, and Ada Boosting. Inclusion of additional features or combining the title and text columns may also enhance the understanding of full context and improve model performance.
