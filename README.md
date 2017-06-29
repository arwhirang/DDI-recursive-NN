# DDI-recursive-NN

This is a code repository from the paper "Drug drug interaction extraction from literature using a recursive neural network", which is under review.

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

&ensp;The relative distance value in the original position embedding has a range from -21 to 21. When the absolute distance value is greater than 5, same vector is given in units of 5. 
&ensp;In the preprocessed test data, the position embedding range is from 0 to 18. First, we merge the absolute distance values that share the same vectors, then the range is changed into -9 to 9. Secondly, we added 9 to the each distance value, because we do not want unnecessary negative values in the tree nodes.


Data Format:  
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

DDI-MedLine.d84.s5.p0 &ensp;&ensp; Synergism was observed when <Ddrug0>GL</Ddrug0> was combined with <Ddrug1>cefazolin</Ddrug1> against Bacillus subtilis and Klebsiella oxytoca.&ensp;&ensp;true&ensp;&ensp;effect&ensp;&ensp;Ddrug0&ensp;&ensp;GL&ensp;&ensp;drug_n&ensp;&ensp;Ddrug1&ensp;&ensp;cefazolin&ensp;&ensp;drug&ensp;&ensp;(1/1/9/9 (1/1/5/3 synergism) (1/1/9/9 (1/1/9/9 (1/1/6/3 was) (1/1/9/9 (1/1/7/3 observed) (1/1/9/9 (1/1/8/4 when) (1/1/9/9 (1/0/9/5 Ddrug0) (1/1/10/9 (1/1/10/6 was) (1/1/11/9 (1/1/11/7 combined) (1/1/12/9 (1/1/12/8 with) (1/1/13/9 (1/0/13/9 Ddrug1) (1/1/14/10 (1/1/14/10 against) (1/1/18/11 (1/1/18/11 (1/1/18/11 (1/1/18/11 bacillus) (1/1/18/12 subtilis)) (1/1/18/13 and)) (1/1/18/14 (1/1/18/14 klebsiella) (1/1/18/18 oxytoca)))))))))))) (1/1/17/18 .)))&ensp;&ensp;synergism, was, observed, when, Ddrug1, was, combined, with, Ddrug1, against, bacillus, subtilis, and, klebsiella, oxytoca, .

