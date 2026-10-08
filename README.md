# Sentiment-Analysis-of-Amazon-Product-Reviews
A natural language processing (NLP) project that analyses the sentiment of Amazon product reviews using spaCy and spaCyTextBlob. The project preprocesses customer reviews, calculates sentiment polarity, assigns Positive, Neutral, or Negative labels, and evaluates the results against Amazon star ratings.

This project was completed as part of an NLP Capstone Project using spaCy and spaCyTextBlob.

What's inside

File

Description

sentiment_analysis.ipynb

Jupyter Notebook containing the complete sentiment analysis workflow

sentiment_analysis_report.pdf

Detailed report covering the methodology, evaluation, findings, limitations, and improvements

Dataset

The project uses the Datafiniti Amazon Consumer Reviews of Amazon Products dataset from Kaggle.

28,332 product reviews

24 columns

Review text was taken from the reviews.text column

Star ratings were taken from the reviews.rating column

No missing review text was found

The dataset is heavily weighted towards positive reviews, with 90.2% of reviews receiving 4 or 5 stars.

Approach

1. Data preprocessing

The review text was cleaned before sentiment analysis:

Missing review text was removed

Text was converted to strings

Text was converted to lowercase

Whitespace was removed

spaCy was used for tokenisation

Stop words, punctuation, and whitespace were removed

2. Sentiment analysis

The cleaned reviews were processed using spaCyTextBlob to calculate sentiment polarity on a scale from -1 to +1.

Sentiment was assigned using the following thresholds:

Polarity

Sentiment

< -0.1

Negative

-0.1 to 0.1

Neutral

> 0.1

Positive

A neutral threshold of 0.1 was selected after comparing several different threshold values.

3. Evaluation

A random sample of 1,000 reviews was used to evaluate the sentiment predictions against the star-rating labels.

The star ratings were mapped as:

1–2 stars → Negative

3 stars → Neutral

4–5 stars → Positive

The evaluation included accuracy, precision, recall, and balanced recall.

Results

The sentiment analyser achieved 74.3% accuracy on the 1,000-review evaluation sample.

Metric

Result

Accuracy

74.3%

Positive Precision

93%

Positive Recall

80%

Negative Recall

16%

Neutral Recall

30%

Balanced Recall

42.0%

The results showed that the approach performed well when identifying clearly positive reviews, but struggled with negative and neutral sentiment.

The 93% positive precision indicates that predictions labelled as positive were usually correct. However, the low 16% negative recall shows that the model missed many genuinely negative reviews.

The dataset's strong positive class imbalance also means that accuracy alone does not provide a complete picture of model performance.

Key Findings

spaCyTextBlob was effective at identifying straightforward positive sentiment.

The model struggled with context-dependent phrases such as "less expensive" and "nothing special".

Removing stop words sometimes changed the sentiment polarity because words such as negation terms can carry important meaning.

Increasing the neutral threshold improved neutral recall but reduced overall accuracy.

spaCy's similarity() measure was useful for comparing semantic similarity, but it did not measure sentiment similarity.

The results demonstrate some of the limitations of lexicon-based sentiment analysis when compared with approaches that learn from labelled data.

Limitations

The project identified several limitations:

The sentiment analyser has limited contextual understanding.

Lexicon-based sentiment can misinterpret phrases and negation.

The dataset contains a strong class imbalance.

Star ratings are an imperfect substitute for manually labelled sentiment.

Only a sample of 1,000 reviews was used for evaluation.

The neutral threshold was selected using the same evaluation sample, which limits how confidently the result can be generalised.

Possible Improvements

Future versions of the project could:

Preserve important negation words such as not, no, and less during preprocessing.

Compare sentiment analysis using the original review text against the stop-word-removed version.

Train a supervised classification model using TF-IDF and Logistic Regression.

Use class weighting or other techniques to address class imbalance.

Evaluate the final approach on a separate held-out test set.

Explore transformer-based NLP models for improved contextual understanding.

Tech Stack

Python

pandas

NumPy

spaCy

spaCyTextBlob

Jupyter Notebook

NLP

How to Run

Clone the repository.

Install the required Python libraries:

pip install pandas numpy spacy spacytextblob jupyter

Download the required spaCy model:

python -m spacy download en_core_web_md

Open the notebook:

jupyter notebook

Open sentiment_analysis.ipynb and run the cells from beginning to end.

Project Focus

This project demonstrates practical experience with:

Natural Language Processing

Text preprocessing

Tokenisation

Sentiment analysis

Sentiment polarity

Model evaluation

Class imbalance

Precision and recall

spaCy pipelines

Basic semantic similarity

Critical evaluation of NLP results
