# Sentiment_Analyses
Submitted Files for drug sentiment analyses. \
To load the model:
model= torch.load('.\model.pth')

You can run the other code cells to get the data and divide it into testing set and create dataloader, do not run the training function again it is marked in notebook as:
(Do not run this cell while testing- this is the training function)

The model weights are stored in the file: https://drive.google.com/file/d/1ZXiOHvAygC80tSkgRJpZRt3apsSLBMY6/view?usp=sharing

What model did you choose? And why? \
**Ans:**\
I did not had labelled data, so my initial thoughts were to choose a unsupervised learning model. But I did not had enough time to test multiple models. So, I have implemented BERT base model (uncased). BERT is a transformers model pretrained on a large corpus of English data in a self-supervised fashion and can then be fine-tuned on smaller task-specific datasets. Which made it suitable for our use case.

How did you tweak it to fit the use case?\
**Ans:** \
One-hidden-layer neural network classifier was added on top of BERT and fine-tuned the model BERT.

How did you build the dataset and how much?\
**Ans:**\
I initially wanted to get data using twitter API or instagram API but they did not work for me. So I did webscrapping on google to come up with dialogues from series related to drugs (Breaking bad and Narcos). I got 100 drug related negative sentences from these dialogues. I also extracted over 200 drug names/slang from a web page but finally used only 100 for training the model. I augmented the data set by translating the sentences to hindi and then translating them back to english. But this gave a few mistakes. So I instead augmented the sentences by using only synonyms. I got total of 200 negative drug related sentences. Further, I replaced each drug word with other drug word/slang from 100 word collection of drug names/slangs. In the image below, w is for word, and s is for sentence. So, to create 10000 sentences, 1 replaced odd index word with all odd index sentences and similarly for even indices.\
<img src= "https://github.com/drashtidave/Sentiment_Analyses/blob/main/data%20augmentation.JPG" width=250>\
I got total of 10000 negative sentiment sentenses like this. From the original 100 drug related negative sentences from series dialogues, I replaced the drug names/ slangs with nouns to make them positive sentiment. For example: instead of 'I'm here to buy meth' replacing meth with dosa becomes 'I'm here to buy dosa' which is positive sentiment. Some sentences did become funny, but served the purpose. From this, I got 3500 positive sentiment sentences. I took 1500 sentences as is from amazon reviews dataset found on kaggle which were all positive sentiment even if they were disliking products. Lastly, I took 25 sentences which have negation in them. For example: 'I want to quit meth'. Augmented these 25 to get 50 sentences in the same way as before. And then replaced drug names in each sentence with our collection of drug names/ slangs to get 5000 positive sentiment sentences. Thus I have a total of 20000 sentences, equally split between positive and negative sentiment. \
<img src="https://github.com/drashtidave/Sentiment_Analyses/blob/main/dataset%20collection%20pos_neg.JPG" width="500">

How many epochs did you train your model with?\
**Ans:**\
2 epoch, But The efficeincy on validation data was also above 99% after 1 epoch.

What is your accuracy and loss?\
**Ans:**\
Training loss is 0.004418
test accuracy is 99.95%

Why did you decide to submit your project with the above accuracy and loss?\
**Ans:**\
We can see from the graph for last answer that training loss for each batch is reducing at high rate innitially, but then the graph platues. Hence, this is a good place to stop the training. Maybe, after increasing the iterations to higher number, we can get a lower loss value, but the current model weights give great accuracy for our dataset. An accuracy of over 99% is great for language model. 

What are the results of predictions?\
Ans:
The following positive predictions are extracted from the model results:\
 ['when it comes to blue kisses and alcohol  just say no'\
 'no bomb, no beer, no poppers you smoke it up on your own time'\
 'I recently received my Amazon Fire TV after months of researching which streamin'\
 'my relation with slick superspeed is in history book now'\
 "Stress is dangerous How's the Batata Saung working out"\
 'our organization, within six calendar_month,will be out of the happy dust business'\
 ' Good Locha for money Call me ' 'coke are not good for health'\
 ' The bags of Bajri no rotlo smell potent as i weigh up their value based on the ideals of monetary gain'\
 ' So much weight it dragging me down Relieve me of this fragrant Amti bounty Delivery 6pm 1 am '] \
The following negative predictions are extracted from the model results:\
 ['been keeping an eye on that blue snow of yours'\
 'rolls royce vitamin  d tabs 210 each if you are referred by a vitamin  d'\
 'you act like gorillas after arctic blast'\
 'snow and Hooker, my snow, are the keys to success.'\
 'Lashkar-e-Taiba us snicker super acid off a bowie knife'\
 'the cartel is pickings methamphetamine shots'\
 'i ve get no coke on me will take it off the money you owe me and do it a bit cheap for you talk soon dude'\
 "it's a party semen on enjoy it with stum bler"\
 'the idea was to replace the gas with pikachu and send it'\
 'very good shot for money on this one']

How many iterations of testing did you go through?\
**Ans:** \
I had a batch size of 32, and for training data size of 14000, there were 437 iteration in 1 epoch. I had total 2 epochs.

Document the results for every iteration of training the model so we are aware of the progress you have made.\
**Ans:** \
Visible in code and from the following graph.\
<img src="https://github.com/drashtidave/Sentiment_Analyses/blob/main/training_graph.png" width="500">
