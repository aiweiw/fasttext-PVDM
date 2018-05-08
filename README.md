# fastText-PVDM

[fastText](https://fasttext.cc/) is a library for efficient learning of word representations and sentence classification.

I achieve PVDM (training and inference) based on fastText, mainly discussed as follows.

## Requirements

**fastText** builds on modern Mac OS and Linux distributions.
Since it uses C++11 features, it requires a compiler with good C++11 support.
These include :

* (gcc-4.6.3 or newer) or (clang-3.3 or newer)

Compilation is carried out using a Makefile, so you will need to have a working **make**.
For the word-similarity evaluation script you will need:

* python 2.6 or newer
* numpy & scipy

## Building fastText

In order to build `fastText`, use the following:

```
$ git clone https://github.com/aiweiw/fasttext-PVDM.git
$ cd fastText-PVDM
$ make
```

This will produce object files for all the classes as well as the main binary `fasttext`.
If you do not plan on using the default system-wide compiler, update the two macros defined at the beginning of the Makefile (CC and INCLUDES).

## Example use cases

This library has three main use cases: word representation learning, text classification and distributed memory
model of paragraph vectors[PVDM].
The PVDM was described in the paper [1](#distributed-representations-of-sentences-and-documents).

### Word representation learning

### Text classification

### PVDM

train, use:

$ ./fasttext PVDM -input train.txt -output model

where train.txt is a text file containing a training sentence per line along with the labels. By default, we assume that labels are words that are prefixed by the string __label__. This will output three files: model.bin, model.vec and labels.vec. Once the model was trained, you can obtain the k most likely labels for a piece of text.

infer, use:

$ ./fasttext predictPVDM model.bin test.txt output k

where test.txt contains a piece of text (Chinese text should be segmented) to get paragraph vectors. Doing so will output the k most likely labels' vectors into the file: output.vec. The argument k is optional, and equal to 1 by default. 

You can set parameters[-epoch 40, -dim 300, ...] to achieve better training and inference.

## Full documentation

Invoke a command without arguments to list available arguments and their default values:

```
$ ./fasttext PVDM
Empty input or output path.

The following arguments are mandatory:
  -input              training file path
  -output             output file path

  The following arguments are optional:
  -verbose            verbosity level [2]

  The following arguments for the dictionary are optional:
  -minCount           minimal number of word occurences [5]
  -minCountLabel      minimal number of label occurences [0]
  -wordNgrams         max length of word ngram [1]
  -bucket             number of buckets [2000000]
  -minn               min length of char ngram [3]
  -maxn               max length of char ngram [6]
  -t                  sampling threshold [0.0001]
  -label              labels prefix [__label__]

  The following arguments for training are optional:
  -lr                 learning rate [0.05]
  -lrUpdateRate       change the rate of updates for the learning rate [100]
  -dim                size of word vectors [100]
  -ws                 size of the context window [5]
  -epoch              number of epochs [5]
  -neg                number of negatives sampled [5]
  -loss               loss function {ns, hs} [ns]
  -thread             number of threads [12]
  -saveOutput         whether output params should be saved [0]
```

## References

Please cite [1](#distributed-representations-of-sentences-and-documents) if using for PVDM.

[1] Quoc V. Le, Tomas Mikolov, [*Distributed Representations of Sentences and Documents*](https://arxiv.org/abs/1405.4053)

## Contact

* Contact: [WeChat:loopal]

## License

fastText is BSD-licensed. I achieve PVDM based on fastText.

## 注

彩蛋: Reversal Skip-gram
