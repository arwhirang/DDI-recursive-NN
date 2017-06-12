# DDI-recursive-NN

This is a code repository from the paper "Drug drug interaction extraction using recursive neural network", which is under review.

Note : We only upload the Recursive NN model, which is based on the tree-lstm implementation using the Tensorflow Fold https://github.com/tensorflow/fold/blob/master/tensorflow_fold/g3doc/sentiment.ipynb

Requirements:  
&ensp;Tensorflow ver 1.1&ensp;&ensp;(we do not test the other versions)  
&ensp;Tensorflow Fold https://github.com/tensorflow/fold  
&ensp;python 3.4 or later  
&ensp;Usual libraries:  
&ensp;&ensp;gensim https://radimrehurek.com/gensim/install.html  
&ensp;&ensp;sklearn http://scikit-learn.org/stable/install.html  
&ensp;&ensp;numpy  
&ensp;&ensp;nltk

Data:  
&ensp;Use the preprocessed test data in the Demo folder. For the whole DDI'13 corpus, visit : http://labda.inf.uc3m.es/ddicorpus  
&ensp;We report the ids of the training set in the "TrainingSetIDs" file.  

Data Format:  
&ensp;After preprocessing step, we separate each pairs into lines. Each line contains pairID, sentence, Interaction, DDI type(if negative, none), the first target drug id, the first target drug name, the first target drug type, the second target drug id, the second target drug name, the second target drug type, parsed tree of a sentence, and words in a sentence separated with comma. Each element is separated with "\t". For example, the 14th in training instance is presented below.

DDI-MedLine.d84.s5.p0&ensp;Synergism was observed when <DdrugFirst>GL</DdrugFirst> was combined with <DdrugSecond>cefazolin</DdrugSecond> against Bacillus subtilis and Klebsiella oxytoca.&ensp;true&ensp;effect&ensp;DdrugFirst&ensp;GL&ensp;drug_n&ensp;DdrugSecond&ensp;cefazolin&ensp;drug&ensp;(1/20/1/9/9 (1/20/1/5/3 synergism) (1/20/1/9/9 (1/20/1/9/9 (1/20/1/6/3 was) (1/20/1/9/9 (1/20/1/7/3 observed) (1/20/1/9/9 (1/20/1/8/4 when) (1/20/1/9/9 (1/1/0/9/5 DdrugFirst) (1/20/1/10/9 (1/20/1/10/6 was) (1/20/1/11/9 (1/20/1/11/7 combined) (1/20/1/12/9 (1/20/1/12/8 with) (1/20/1/13/9 (1/1/0/13/9 DdrugSecond) (1/20/1/14/10 (1/20/1/14/10 against) (1/20/1/18/11 (1/20/1/18/11 (1/20/1/18/11 (1/20/1/18/11 bacillus) (1/20/1/18/12 subtilis)) (1/20/1/18/13 and)) (1/20/1/18/14 (1/20/1/18/14 klebsiella) (1/20/1/18/18 oxytoca)))))))))))) (1/20/1/17/18 .)))&ensp;synergism, was, observed, when, DdrugFirst, was, combined, with, DdrugSecond, against, bacillus, subtilis, and, klebsiella, oxytoca, .

