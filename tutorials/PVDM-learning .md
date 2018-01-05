# Preparing the data

Need labeled data, E.g:

__label__1 __label__2 原告 诉称 ： 2013年 1月 25日 ， 原告 和 被告 ...

__label__3 原告 诉称 ， 被告 ...

# Training PVDM

Learning PVDM on this data can now be achieved with a single command:

```
$ mkdir result
$ ./fasttext PVDM -input data/file -output result/model
```

```
playing with the parameters
$ ./fasttext PVDM -input data/file -output result/model -epoch 40
```

While fastText is running,  the progress and estimated time to completion is shown on your screen.  Once the program finishes, there should be three files in the result directory:

```
$ ls -l result
-rw-rw-r-- 1 uww uww 7138696 Dec  8 10:34 model.bin
-rw-rw-r-- 1 uww uww 1313903 Dec  8 10:34 model.labels.vec
-rw-rw-r-- 1 uww uww 7226102 Dec  8 10:34 model.vec
```

The `model.bin` file is a binary file that stores the whole fastText model and can be subsequently loaded.

The `model.labels.vec` file is a text file that contains the label vectors, one per line for each label:

```
$ head -n 3 result/model.labels.vec
1514 100
__label__894 0.59943 0.40732 -0.2452 -0.33805 0.61109 -0.057327 -0.096136 ...
__label__1297 0.22869 0.41098 -0.050275 -0.42004 0.42071 0.43567 -0.20067 ...
```

The first line is a header containing the number of labels and the dimensionality of the vectors. The subsequent lines are the label vectors for all labels. 

The `model.vec` file is a text file that contains the word vectors, one per line for each word in the vocabulary:

```
$ head -n 3 result/model.vec
7953 100
原告 -0.10363 -0.063669 0.032436 -0.040798 0.53749 0.00097867 0.10083 0.24829 ...
被告 0.14806 -0.70637 -0.83392 -0.38033 -0.49266 -0.41232 -2.2306 ...
```

The first line is a header containing the number of words and the dimensionality of the vectors. The subsequent lines are the word vectors for all words in the vocabulary, sorted by decreasing frequency.

### Advanced reader: the inference stage

The inference stage is the number of correct labels among the labels inferred by fastText. Let's take an example to make this more clear:

```
$ ./fasttext predictPVDM result/model.bin data/test.txt result/infer k
The argument k is optional, and is equal to 1 by default.
```
The `model.bin` file is just training saved.

The `test.txt` file is inferred. E.g:
原告 诉称 ， 被告 董** 于 2009年 5月 ...

While fastText is running,  the progress and estimated time to completion is shown on your screen.  Once the program finishes, there should be one file in the result directory:

```
$ ls -l result
-rw-rw-r-- 1 uww uww     964 Dec  8 10:45 infer.vec
-rw-rw-r-- 1 uww uww 7138696 Dec  8 10:34 model.bin
-rw-rw-r-- 1 uww uww 1313903 Dec  8 10:34 model.labels.vec
-rw-rw-r-- 1 uww uww 7226102 Dec  8 10:34 model.vec
```

The `infer.vec` file is a text file that contains the inferred label vector. This inferred label vector can be calculated similarly to the previously trained label vectors to predict similar content.


# Conclusion

In this tutorial, we gave a brief overview of how to use fastText to train PVDM. We had a light overview of some of the most important options to tune.
