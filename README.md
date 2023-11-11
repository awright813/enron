# Analysis of the Enron Corpus
<img align="left" width="150" height="175" src="https://github.com/awright813/enron/blob/master/misc/logo.png">
A slightly-nosy deep-dive into the subtleties of corporate communication in a crisis.

## Data
[Enron Dataset and Context](https://www.cs.cmu.edu/~enron/)  
[Searchable Database of Enron Corpus](http://www.enron-mail.com)  
[Download Dataset](https://academictorrents.com/details/4697a6e1e7841602651b087d84f904d43590d4ff)  


## Sentiment Analysis
Approximately 1,000 Enron emails were manually annotated with the document sentiment and then used to fine-tune a pre-trained BERT model for sentiment classification. These annotated emails were then passed through a Term Frequency - Inverse Document Frequency (TF-IDF) vectorizer and used to train a Naive Bayes classifier to establish a baseline for performance. This classifier achieved a micro-average ROC-AUC of 0.75 and an accuracy of 57.26%.

The training documents were then tokenized using the appropriate BERT tokenizer and converted to PyTorch tensors of token ids and attention masks for input into the pre-trained BERT model. To boost the training speed and save memory, the PyTorch DataLoader class was utilized to create an iterator for the dataset. 

A custom BERT Classifier class and training loop was constructed around the bert-base-uncased pre-trained model. 5 training epochs were run with accuracy trailing off after the 5th epoch. The BERT Classifier achieved a micro-average ROC-AUC of 0.86 and an accuracy of 69.23%, representing a nearly 12% increase in accuracy over the Naive Bayes Classifier.

This model was then used to predict the sentiment for an additional 144,000 Enron e-mails. The predicted email sentiment was then aggregated by day using the sum of positive e-mails (value of +1) and negative emails (value of -1) to analyze the broad changes in the sentiment of emails sent and received by Enron employees over time. As seen in the chart to the right in a 14-day Moving Average of the email sentiment, the emails got progressively more negative in aggregate as the Enron scandal unfolded and the company’s stock price collapsed. October and November of 2001 were the height of the scandal, and that is clearly reflected in employee email sentiment.

[BERT documentation](https://huggingface.co/bert-base-uncased)

## Model Performance
### Naive Bayes Classifier vs Fine-Tuned BERT Classifier
<p float="left">
  <img src="https://github.com/awright813/enron/blob/master/misc/naive_bayes_ROC.png" width="500" />
  <img src="https://github.com/awright813/enron/blob/master/misc/BERT_ROC.png" width="500" /> 
</p>

## Email Sentiment Over Time
<img src="https://github.com/awright813/enron/blob/master/misc/stock_sentiment.png" width="1000" />
