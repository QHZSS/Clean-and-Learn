## Clean and Learn: Improving Robustness to Spurious Solutions in API Question Answering

## Introduction


The development of a Question Answering (QA) system for Application Programming Interface (API) documentation can greatly facilitate developers in API-related tasks.
However, when applying deep learning technology, API QA systems suffer from the spurious solution problem. That is, the answer can literally appear in multiple positions (i.e., start-end indices) in the API documentation, though only one of them (called golden
solution) correctly solves the question given its context. The other incorrect candidates
(called spurious solutions) hinder the neural network model to learn reasonable solutions
or correct answers. In this work, we propose Clean-and-Learn, an effective and robust
method for API question answering over documents. In order to reduce the spuriousness
of candidate solutions used for training, we design several scoring functions to rank the
candidate occurrences (clean). Only high-quality (top-k) candidate solutions are involved
for training. Then, we perform multi-task learning by weighing the losses computed from
the top-k occurrences (learn). We evaluate our method on the constructed ApiQaSet
dataset. The experiment results show that Clean-and-Learn achieves a ROUGE-L score
of 75.8 and an accuracy of 70.5% in API question answering, which significantly outperforms state-of-the-art approaches.

We  propose  a  novel  API  QA  method  named Clean-and-Learn, which aims to improve robustness to spurious solutions. Unlike traditional methods, Clean-and-Learnonly needs weak supervision to train the API QA model. First, it cleans the spurious candidate solutions from weakly supervised dataset though anumber of scoring functions. Hence, only high-quality (top-k) candidate solutionsare involved for training. Next, it learns a robust QA model via multi-task learningon the selected candidates.


We evaluate the effectiveness of the proposed Clean-and-Learn on ApiQaSet, a dataset that we created with 200 API QAs on the Java documentation. We compare Clean-and-Learn with the state-of-the-art API QA methods (OpenAPIBot [4] andAPIBot [2]) and general weakly supervised learning methods (BLANC [12], Single-Hop BERT [28] and Hard-EM [5]). The results show that Clean-and-Learn obtains an accuracy of 70.5% in API question answering, which significantly outperforms existing  rule  based  and  weakly  supervised  approaches  and  achieves  comparable results to that of fully supervised models.

## ApiQaSet

ApiQaSet consists of 200 API-related questions. The proportions of the three categories of questions are 41%, 40%, and 19%, respectively. We split dataset (70%/30%) into train/test dataset. Each record of our dataset is a question-answer-solution triple:
1. Question: the title, body and category of the question.
2. Answer: the textual answer of the question.
3. Solution: the start-end index of one occurrence of the answer.


## Getting Started

1. Rename the dev set to test.jsonl.gz

2. Run split_data.py in code/src/preprocessor as follows:

```bash
python split_data.py \
    --source ../../../data/naturalQ/train.jsonl.gz \
    --train_output train.jsonl \
    --dev_output dev.jsonl \
    --data_type mrqa
```

4. Compress train.jsonl and dev.jsonl with gzip (gzip train.jsonl; gzip dev.jsonl)

5. Locate these two files into data/naturalQ/ directory

6. Now you have train/dev/test set in data/naturalQ directory


### Train BLANC with Clean and Learn on ApiQaData

Run BLANC script in code/ as follows:

```bash
LABEL=trial_001 GEOP=0.99 WINS=3 LMB=0.8 bash run_blanc_naturalqa.sh
```

### Test BLANC

Indicate which checkpoint you want to test.

In this case, we test BLANC with trial_001 checkpoint.

```bash
LABEL=trial_001 GEOP=0.99 WINS=3 LMB=0.8 bash run_blanc_naturalqa_test.sh
```

## Code Reference

https://github.com/facebookresearch/SpanBERT
