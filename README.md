# DDI-recursive-NN

This is a code repository from the paper "Drug drug interaction extraction from the literature using a recursive neural network", https://doi.org/10.1371/journal.pone.0190926.

We upload the Recursive NN model, which is based on the tree-lstm implementation using the Tensorflow Fold https://github.com/tensorflow/fold/blob/master/tensorflow_fold/g3doc/sentiment.ipynb

## Requirements:  
&ensp;Tensorflow ver 1.1&ensp;&ensp;(we do not test the other versions, we found that tensorflow fold is known to be working best at tf version 1.0.0. You may change to the version 1.0.0)  
&ensp;Tensorflow Fold https://github.com/tensorflow/fold  
&ensp;python 3.4 or later  
&ensp;Usual libraries:  
&ensp;&ensp;gensim https://radimrehurek.com/gensim/install.html  
&ensp;&ensp;sklearn http://scikit-learn.org/stable/install.html  
&ensp;&ensp;numpy  
&ensp;&ensp;nltk  

## Data:  
&ensp;Our code use the preprocessed test and train data in the Demo/data folder. This is not the original data.  
&ensp;Word embedding is not included. visit : http://evexdb.org/pmresources/vec-space-models/

&ensp;For the original DDI'13 corpus, visit : http://labda.inf.uc3m.es/ddicorpus  
&ensp;&ensp;We do not own the original DDI'13 corpus, however, the data in the Demo/data folder is enough to run our code.

[//]: # (&ensp;We report the ids of the training set in the "TrainingSetIDs" file.)

## Training and Testing:  
&ensp;First, run the "saveWEUsedinDataOnly" code to reduce the size of the word embedding.  
&ensp;Second, run the "DDI_detection" code for the DDI detection single model classifier.
&ensp;Note : you may want to change the directory path for reserving logits.

&ensp;Potision Embedding implementation
&ensp;The relative distance value in the original position embedding has a range from -21 to 21. When the absolute distance value is greater than 5, same vector is given in units of 5. 
&ensp;In the preprocessed test data, the position embedding range is from 0 to 18. First, we merge the absolute distance values that share the same vectors, then the range is changed into -9 to 9. Secondly, we added 9 to the each distance value, because we do not want unnecessary negative values in the tree nodes.  
  
&ensp;We do not release code for other tasks because other tasks (e.g. "two-stage classification") require human hand. However, the other tasks are easy to implement.

## Data Format:  
&ensp;After preprocessing step, we separate each pairs into lines. Each line contains
+ pairID,
+ sentence,
+ Interaction,
+ DDI type(if negative, none),
+ the first target drug id,
+ the first target drug name,
+ the first target drug type,
+ the second target drug id,
+ the second target drug name,
+ the second target drug type,
+ parsed tree of a sentence,
+ and words in a sentence separated with comma.

Each element is separated with "\t". For example, the 14th instance in training set is presented below.

DDI-MedLine.d84.s5.p0 &ensp;&ensp; Synergism was observed when <Ddrug0>GL</Ddrug0> was combined with <Ddrug1>cefazolin</Ddrug1> against Bacillus subtilis and Klebsiella oxytoca.&ensp;&ensp;true&ensp;&ensp;effect&ensp;&ensp;Ddrug0&ensp;&ensp;GL&ensp;&ensp;drug_n&ensp;&ensp;Ddrug1&ensp;&ensp;cefazolin&ensp;&ensp;drug&ensp;&ensp;(1/0/9/9 (1/1/5/3 synergism) (1/0/9/9 (1/0/9/9 (1/1/6/3 was) (1/0/9/9 (1/1/7/3 observed) (1/0/9/9 (1/1/8/4 when) (1/0/9/9 (1/0/9/5 ddrug0) (1/0/10/9 (1/1/10/6 was) (1/0/11/9 (1/1/11/7 combined) (1/0/12/9 (1/1/12/8 with) (1/0/13/9 (1/0/13/9 ddrug1) (1/1/14/10 (1/1/14/10 against) (1/1/18/11 (1/1/18/11 (1/1/18/11 (1/1/18/11 bacillus) (1/1/18/12 subtilis)) (1/1/18/13 and)) (1/1/18/14 (1/1/18/14 klebsiella) (1/1/18/18 oxytoca)))))))))))) (1/1/17/18 .))&ensp;&ensp;synergism, was, observed, when, ddrug0, was, combined, with, ddrug1, against, bacillus, subtilis, and, klebsiella, oxytoca, .

Every node in a tree has the follwing input format.
* (label/Fsc/Fd1/Fd2 content)
The label is the answer label of a drug pair, and all the nodes of a tree share the same label as the root node. The model has two classes for detection and five classes for classification. The Fsc/Fd1/Fd2 are the subtree containment (context), position1, and position2 features of a node, respectively. A node in a tree could be a leaf or an internal node. The content in the node is an input word if it is a leaf node, and if the current node is not a leaf node, the contents consists of children nodes of the current node.
