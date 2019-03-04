### Purpose

Run pretrained ELMo model to get single sentence perplexity.

### Installation

```
pip install tensorflow-gpu==1.2 h5py
python setup.py install
```

### Run

1. Data file format: each line in a file is a sentence to calculate perplexity. [demo](demodata/sents.txt)
2. Split data file into pieces, one sentence per piece.
```
split sents.txt -d -l 1 -a 4 cs
```
3. Run the evaluation script.
```
sh evaluate.sh
```
4. The perplexity score is shown in stdout:
```
...
5946: 129.57085
5947: 1412.2032
5948: 5172.711
5949: 2126.5542
...
```
Sentence line number followed by the perplxity (unnormalized by sentence length)

