# Sentiment_Analysis
Sentiment Analysis of the IMDB large movie dataset. The dataset is highly polarized with 50000 movie review. The primary task is to classify the reviews into negative(ratings 0 to 4) and positive (ratings 7-10) using machine learning techniques.
IMDB Large Movie Dataset Sentiment Analysis Classification:

This dataset was used as a mini-project for the class of Data Science-II (NLP)

GITHUB: 



The dataset is collected from the website:
http://ai.stanford.edu/~amaas/data/sentiment/

*However, the 'movie_data.csv' file, which is made available by the author of 'Machine Learning Pyhton' was found on his Github here:
https://github.com/rasbt/python-machine-learning-book/blob/master/code/ch08/ch08.ipynb

FLOWCHART:
1. Import all the necessary libraries for the notebook to run. 
1. Import the '.csv' file in jupyter notebook.
2. Apply pre-processing techniques learnt in class to the dataframe.
3. Apply different vectorization techniques to convert data into suitable format for applying machine learning algorithms.
4. Apply different machine learning algorithms and validate it against the test set to check the veracity of results.
5. Print confusion matrix and metrics (precision,recall, F-1) to identify how the model performed.

Since the importing csv file is done using standard 'pd.read_csv' command, we will start with the pre-processing.



1. PRE_PROCESSING:

The dataset contains 50000 rows and 2 columns. The first column is the review made for each movie and the 
second columns is the actual review_rating given to that movie. The reviews contains strings with punctuations,
uppercase letters, numeric values,etc. To get rid of all of these, the functions 'remove_punc' is used. This 
funtion is then applied to all rows.

The second step is to tokenize all words. By tokenizing, we can seperately count (for Bag of words and vectorization)
each word. This is done using the 'tokenize' function. This function is then applied for all rows.

The third step is to remove the unnecessary words (pronouns, articles, etc) from the tokenized strings. This is
obtained using the 'stopwords' function. It is then applied to all rows. (import the stopwords before using it)

The Fourth step is to find lemma's of all words. This would enable the machine learning algorithms to run a bit
quicker than it would. Finding and combining lemmas would result in lowering the columns generated by vectorization.
This is applied using the 'lemmatizing' function and then applied to all rows.

The 'stemmers' are not currently used in the notebook, primarily because some words were losing their value. I may
refine it later and commit on git.

The data is ready for further processing.


2. VECTORIZATION:

There are 2 types of vectorization techniques used:

2.1: COUNT_VECTORIZATION (BAG OF WORDS):

The count vectorization counts the number of distinct words in the corpus. Most values are zeroes since there are
very few distinct words.


2.2: TERM FREQUENCY- INVERSE DOCUMENT FREQUENCY (TF_IDF):

This vectorization technique counts the frequency along with occurences. The algorithm gives importance to the
most unqiue words from the corpus and creates a sparse matrix.



3. ALGORITHMS:

3.1: NAIVE BAYES (BERNOULLI, MULTINOMIAL)
3.2: LOGISTIC REGRESSION 
3.3: SUPPORT VECTOR MACHINES (SVM) (LINEAR, RBF, POLY, SIGMOID)
3.4: RANDOM FOREST
3.5: GRADIENTBOOST
3.6: MAXIMUM_ENTROPY 


3.1: NAIVE BAYES:

Naive Bayes is one of the primary naive classifiers used for classification purposes. 
It gives the probability of word occuring given the probability of other occuring words. There are 3 types of
naive bayes based on data; Gaussian, Multinomial and Bernoulli.
I started with multinomial but later realized, it cannot be directly applied to this data. I then applied bernoulli
and realized, I cannot use count_vectorizer with bernoulli as count vectorizer counts the number of occurunces 
of words while bernoulli will count 1 if word is present and 0 if word is not present. So they cannot be applied
together. However, the Bernoulli classifier is able to accept the count_vect dataframe as any count more than 0 is
counted as 1 and 0 as 0. Therefore, it does not show any error. However, we should avoid using them together.

I also had trouble converting sparse matrix to dense using the _todense() function. That should further be able
to reduce the dimesnsions on tfidf and count vectorizers.

** The following is the list and types of classifiers used:

3.1.1: BERNOULLI NB + Count_Vectorizer:
for Alpha = 0,0.7, 5


3.1.2: MULTINOMIAL NB + Count_Vectorizer:
FOR ALPHA = 0, 1.6, 2

3.1.1 BERNOULLI NB + + TF_IDF:
for Alpha = 5

3.1.2: MULTINOMIAL NB + TF_IDF:
for Alpha = 2, 0.3


4.1: Support Vector Machines:
The support vector machines are another classifier widely used for natural language processing. SVM's creates
a hyperplane/s to classify data with accuracy controlled by the cost function, alpha, gamma and other parameters.
There are 4 types of solvers used with linear giving the best f1 score. This is probably because the data
is polarized.

** I tried to visualize the data on another book to see if the classification makes sense. I couldn't get it
to work though. This would have enabled me to use appropriate SVM classifier and make distinct classification.

The 'Radial Bias Function' AKA rbf solver is used and I tried to play with the cost functions to get better
F-1 scores and accuracy. However, since it takes long to implement, I havent uploaded that in the code.

The 'poly' and 'sigmoid' functions are also used since the data is binary to see if we could get better F1.


5.1: Random Forest:
The random forest classifier fits a number of decision tress classifiers on various samples of the imdb 
train dataset and averages the output reducing the bias and variance. The input to this classifier is 
the 'tfidf' train set.
However with such a high accuracy, it is leading me to believe, that the model may overfit with low bias and
high variance becuase I have used may trees. 

6.1: Gradient Boost:
The gradient boosting method is widely used. The learning parameter alpha is set to 1 and n_params is set
to 50. But we can see it is not giving enough accuracy. I ran out of time to run it for n_params =1000 and 
it had shown F1 score of 83%.

7.1: Maximum Entropy Model:
This is similar to logistic model. However, I was not able to run it.





















