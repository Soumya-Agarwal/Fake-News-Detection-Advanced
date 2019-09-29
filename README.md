STEPS

    1. Data Preprocessing
    2. Modelling for Multiclass
    3. Modelling for Binary

MODELS

    1. Made tfidf features and trained random forest (giving best results despite the fact that   		grid search has not been performed due to resource and time constraints.)
      
    2. Made word embeddings and trained parallel Bi LSTMs for 20 epochs
       (Increasing number of epochs can increase the learning)
            
    3. Made word embeddings and traind Siamese Network for 20 epochs

For detailed classification report, refer code.

RESULTS

Results from the research paper provided in the mail show that 70% on binary and 36% on multiclass has been obtained.  
Through my first approach, I improved on this and got 73% and 41% respectively which will further improve with more tuned parameters and heavy resources.
Also, great improvement in classifying the 4th and 5th  label with precision 63% and 61% respectively, which is quite better than the 33% and 41% mentioned in the research paper.
Through my next approaches i.e. the Deep Learning models, similar results are obtained as shown above which are expected to increase if number of epochs are increased.

METHODOLGY

1. Data Preprocessing:
    • Added a feature called emotion of statement.
    • Removed forbidden words from justifications.
    • Removed non alphanumeric characters from categorical columns.
    • Multiclasses have been combined and binary classes are formed as separate column.
    • Data beyond 98.5 percentile has been labeled as other.
    • Null Numerical columns to be replaced with mean of the column.
    • Outlier values (beyond 3 std) again to be replaced with mean or median. 
    • All the Na values have been taken care of.
    • All the categorical columns have been one hot encoded.
	Detailed reasons and function definitions have been provided in the code.

      2. Model tf-idf-RF:
    • Tf-idf vector has been fit on train data and then val and test have been converted.
    •  Tf-idf features have been added to the metadata.
    • Random Forest has been used for training, with 200 trees. Grid search is not used due to time and resource constraints. 

3. Model BiLSTM with word embeddings
    • Glove with 50 dimensional embedding has been used for word to vec.  
    • Embedding layer of statement and justification along with metadata is concatenated and passed through dense layers and an output layer of 1 and 6 neurons respectively is taken for binary and muticlass classification.
    • Separate Time Distributed layers are applied on the embedding of statement and justification to get output separately by timesteps before concatenation.
      
4. Model Siamese with word embeddings
    • Glove with 50 dimensional embedding has been used for word to vec.  
    • Embedding layer of statement and justification along with metadata is concatenated with manhattan distance between the two embeddings and then passed through dense layers and an output layer of 1 and 6 neurons respectively is taken for binary and muticlass classification.
    • Unlike the above model, same BiDirectional LSTM is used for the statement and justification embedding.
    • This works better than normal LSTM as the difference between the embeddings is also taken into account.


LIBRARIES USED

All the requirements for the code are there in the requirements folder. One can directly install those files and get all the requiremnts satisified.
Web Sources: pandas documentation
		keras documentation and other library documentations
		Research paper provided in the mail
		Stack Overflow

SCOPE

    • XGBoost can also give good results in place of Random Forest. I also tried SVM as mentioned in the paper but due to resource constraints, the grid search could not be trained.
    • Increasing the embedding dimension shall further improve the accuracy.
    • The main aspect is to learn the relation between statement and justification and for that level of contradiction between the statement and justification will really help. Lower the contradiction, more the chances of being true.
    •  This contradiction can be calculated by extracting common trigrams or so and see how many coccur. It will help us know the similarity of facts and claims in statement and justification.
