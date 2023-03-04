# Sentiment_Analyses
Submitted Files for drug sentiment analyses.
To load the model:
from transformers import AutoModelForSequenceClassification
AutoModelForSequenceClassification.from_pretrained("./model")

You can run the other code cells to get the data and divide it into testing set and create dataloader, do not run the training function again it is marked in notebook as:
(Do not run this cell while testing- this is the training function)

What model did you choose? And why?
Ans:
I did not had labelled data, so my initial thoughts were to choose a unsupervised learning model. But I did not had enough time to test multiple models. So, I have implemented BERT base model (uncased). BERT is a transformers model pretrained on a large corpus of English data in a self-supervised fashion and can then be fine-tuned on smaller task-specific datasets. Which made it suitable for our use case.

How did you tweak it to fit the use case?
Ans: 
One-hidden-layer neural network classifier was added on top of BERT and fine-tuned the model BERT.

How did you build the dataset and how much?
Ans:
I initially wanted to get data using twitter API or instagram API but they did not work for me. So I did webscrapping on google to come up with dialogues from series related to drugs (Breaking bad and Narcos). I got 100 drug related negative sentences from these dialogues. I also extracted over 200 drug names/slang from a web page but finally used only 100 for training the model. I augmented the data set by translating the sentences to hindi and then translating them back to english. But this gave a few mistakes. So I instead augmented the sentences by using only synonyms. I got total of 200 negative drug replated sentences. Further, I replaced each drug word with other drug word/slang from 100 word collection of drug names/slangs. I got total of 10000 negative sentiment sentenses like this. From the original 100 drug related negative sentences from series dialogues, I replaced the drug names/ slangs with nouns to make them positive sentiment. For example: instead of 'I'm here to buy meth' replacing meth with dosa becomes 'I'm here to buy dosa' which is positive sentiment. Some sentences did become funny, but served the purpose. From this, I got 3500 positive sentiment sentences. I took 1500 sentences as is from amazon reviews dataset found on kaggle which were all positive sentiment even if they were disliking products. Lastly, I took 25 sentences which have negation in them. For example: 'I want to quit meth'. Augmented these 25 to get 50 sentences in the same way as before. And then replaced drug names in each sentence with our collection of drug names/ slangs to get 5000 positive sentiment sentences. Thus I have a total of 20000 sentences, equally split between positive and negative sentiment.

How many epochs did you train your model with?
Ans:
1 epoch to save time. But number of epochs could be increased to improve the efficeincy.

What is your accuracy and loss?
Ans:

Why did you decide to submit your project with the above accuracy and loss?
Ans:
It is decent accuracy and loss given our dataset. 

What are the results of predictions?
Ans:

How many iterations of testing did you go through?
Ans:

Document the results for every iteration of training the model so we are aware of the progress you have made.
Ans: 
Visible in code.
