# Sentiment-Analysis-of-Amazon-Product-Reviews
A natural language processing project that analyses Amazon product reviews and classifies them as Positive, Neutral, or Negative using spaCy and spaCyTextBlob.

The project uses the Datafiniti Amazon Consumer Reviews dataset and applies text preprocessing, polarity scoring, sentiment classification, review similarity analysis, and evaluation against customer star ratings.

This project was completed as part of an NLP Capstone Project.

What's inside

File

Description

sentiment_analysis.ipynb

Full notebook: data loading, preprocessing, sentiment functions, demonstrations, evaluation and analysis

sentiment_analysis_report.pdf

Report documenting the methodology, results, limitations and possible improvements

The dataset CSV is not included in this repository. It should be placed in the same folder as the notebook.

Dataset

The project uses the Datafiniti Amazon Consumer Reviews of Amazon Products dataset, May 2019 version, from Kaggle.

The dataset contains 28,332 Amazon product reviews and 24 columns. The project uses:

reviews.text — the customer review used as the input to the sentiment analysis.

reviews.rating — the customer's 1–5 star rating, used as a reference label when evaluating the sentiment predictions.

The dataset is heavily imbalanced towards positive reviews:

Rating

Reviews

1

965

2

616

3

1,206

4

5,648

5

19,897

Overall, 90.2% of the reviews have 4 or 5 stars, while only 5.6% have 1 or 2 stars. This imbalance is important when interpreting the model's evaluation results.

Approach

Data loading: loaded the Amazon reviews CSV with pandas and checked the dataset dimensions, columns and missing review text.

Preprocessing: converted reviews to strings, converted them to lowercase and removed leading/trailing whitespace. spaCy was then used to tokenise the text and remove stop words, punctuation and whitespace tokens.

Sentiment scoring: passed the cleaned reviews through the spaCy en_core_web_md model with the spaCyTextBlob component. Each review receives a polarity score from -1 to +1.

Sentiment classification: converted polarity scores into three sentiment categories:

Positive: polarity > 0.1

Neutral: -0.1 ≤ polarity ≤ 0.1

Negative: polarity < -0.1

Sample testing: tested the sentiment function on both existing dataset reviews and six manually written reviews with known sentiment.

Star-rating evaluation: randomly selected 1,000 reviews using random_state=42, converted their star ratings into Positive, Neutral and Negative labels, and compared those labels with the model predictions.

Neutral-band comparison: tested neutral bands from 0.0 to 0.3 to determine how changing the threshold affected accuracy and per-class recall.

Review similarity: used spaCy's similarity() function to compare the semantic similarity between different reviews.

Results

The model achieved the following results on the 1,000-review evaluation sample:

Metric

Value

Test sample

1,000 reviews

Accuracy

74.3%

Majority-class baseline

90.0%

Balanced recall

42.0%

Negative recall

16%

Neutral recall

30%

Positive recall

80%

Negative precision

28%

Neutral precision

8%

Positive precision

93%

The model performs particularly well when predicting Positive reviews, achieving 93% precision. However, it struggles to identify negative and neutral reviews.

The model's 74.3% accuracy is also below the 90.0% majority-class baseline, demonstrating why accuracy alone is not a reliable measure for this imbalanced dataset.

Neutral-band comparison

Different polarity thresholds were tested:

Neutral Band

Accuracy

Negative Recall

Neutral Recall

Positive Recall

Balanced Recall

0.0

78.3%

24%

12%

85%

40.3%

0.05

76.7%

20%

18%

83%

40.4%

0.1

74.3%

16%

30%

80%

42.0%

0.2

69.1%

10%

50%

73%

44.5%

0.3

59.2%

4%

64%

62%

43.3%

A neutral band of 0.1 was selected as a compromise between accuracy, negative recall and neutral recall. A band of 0.2 produced the highest balanced recall, but at the cost of lower overall accuracy and weaker negative recall.

Key takeaways

The approach is fast and simple. It does not require training a machine-learning model or creating a training dataset.

Positive reviews are handled reasonably well, particularly when they contain clear sentiment words such as "great", "terrible" or "happy".

Context is a major limitation. The lexicon-based approach can struggle with phrases such as "less expensive" and "nothing special".

Stop-word removal can affect sentiment. Words such as not, no and less can carry important sentiment information but may be removed during preprocessing.

Class imbalance has a significant effect on the results. The model performs much better on the majority Positive class than on Negative and Neutral reviews.

Similarity does not equal sentiment. Two reviews can be semantically similar even when their sentiment differs.

For example, a negative review compared with a positive review still produced a similarity score of 0.867, showing that spaCy similarity is measuring vocabulary and topic similarity rather than sentiment.

Strengths and limitations

Strengths

Simple and fast sentiment analysis pipeline.

No model training is required.

Polarity scores are easy to interpret.

Modular preprocessing, scoring and classification functions.

Works relatively well for clearly positive reviews.

Includes both manual testing and larger-scale evaluation.

Limitations

The lexicon-based approach has limited understanding of context and negation.

Removing stop words can remove important words such as not, no and less.

Negative and Neutral classes have poor recall.

Overall accuracy is below the majority-class baseline.

The star rating is only an approximate proxy for actual sentiment.

The evaluation contains relatively few Negative and Neutral examples.

The neutral-band setting was tuned and evaluated on the same sample.

spaCy similarity measures semantic/topic similarity rather than sentiment.

Possible improvements

Preserve important negation words such as not during preprocessing.

Compare the cleaned-text approach against scoring the original unprocessed reviews.

Train a supervised classifier using TF-IDF features and logistic regression.

Experiment with class weighting to address the imbalance between Positive, Neutral and Negative reviews.

Investigate transformer-based NLP models for improved contextual understanding.

Use a separate validation/held-out dataset when selecting the neutral-band threshold.

Use more representative sentiment labels instead of relying solely on star ratings.

Tech stack

Python · pandas · spaCy · spaCyTextBlob · NumPy · Jupyter Notebook · NLP

How to run

Clone the repository.

Install the required Python packages:

pip install pandas spacy spacytextblob

Download the spaCy English model:

python -m spacy download en_core_web_md

Place the Datafiniti Amazon reviews CSV in the same folder as the notebook.

The notebook expects the dataset to be named:

Datafiniti_Amazon_Consumer_Reviews_of_Amazon_Products_May19.csv

Open the notebook:

jupyter notebook sentiment_analysis.ipynb

Run all cells in order.

The notebook loads the dataset, preprocesses the reviews, calculates sentiment polarity, assigns sentiment labels, evaluates the predictions against star ratings and compares different neutral-band thresholds.
