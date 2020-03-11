# Use ELMo as a Language Model

## Purpose

Run pretrained ELMo model to get single sentence perplexity.

Modified from [Allenai bilm-tf](https://github.com/allenai/bilm-tf)

## Installation

```bash
pip install tensorflow-gpu==1.2 h5py
python setup.py install
```

## Run Evaluation

1. Data file format: each line in a file is a sentence to calculate perplexity. [data](data/sents.txt)

2. Split data file into pieces, one sentence per piece.

```bash
cd data
split sents.txt -d -l 1 -a 4 cs
```

3. Run the evaluation script.

```bash
sh evaluate.sh
```

4. The perplexity score is shown in stdout

```text
...
5946: 129.57085
5947: 1412.2032
5948: 5172.711
5949: 2126.5542
...
```

Sentence line number followed by the perplxity (unnormalized by sentence length)

## Finetune

To finetune the ELMo on additional corpus, first downlaod the pretrained model to `models/`

The tensorflow checkpoint is available by downloading these files:

[vocabulary](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/vocab-2016-09-10.txt)
[checkpoint](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/2x4096_512_2048cnn_2xhighway_tf_checkpoint/checkpoint)
[options](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/2x4096_512_2048cnn_2xhighway_tf_checkpoint/options.json)
[1](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/2x4096_512_2048cnn_2xhighway_tf_checkpoint/model.ckpt-935588.data-00000-of-00001)
[2](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/2x4096_512_2048cnn_2xhighway_tf_checkpoint/model.ckpt-935588.index)
[3](https://s3-us-west-2.amazonaws.com/allennlp/models/elmo/2x4096_512_2048cnn_2xhighway_tf_checkpoint/model.ckpt-935588.meta)

<pre>
|
|--models
    |--vocab-2016-09-10.txt
    |--checkpoint
            |--checkpoint
            |--options.json
            |--model.ckpt-935588.meta
            |--model.ckpt-935588.index
            |--model.ckpt-935588.data-00000-of-00001
</pre>

Then use the following script.

```bash
sh finetune.sh
```

After finetuning the model, you can run the evaluation again to see the finetune effect.
