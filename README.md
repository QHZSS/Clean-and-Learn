## Clean and Learn: Weakly-Supervised Learning for API Question Answering


## Abstract

The development of a QA system for API documentation can greatly facilitate developers in API related tasks. Existing API QA systemsare trained with weakly-supervised tasks. That is, the golden an-swer can literally appear in multiple positions (i.e., start-end in-dices) in the documentation, though only one of them correctly solve the question given its context. The other incorrect candidates(called spurious answers) can hinder the model to correctly learn the golden answer.In this work, we perform an empirical study on the weakly supervised problem in API QA systems. We collect ApiQaData, a set of 200 API questions about Java from StackOverflow and find that the golden answers are often literally correlated to the original question. Based on the empirical findings, we propose Clean and Learn, a novel API QA approach based on weakly-supervised learning. To alleviate the impact of multiple occurrences of the golden answer, we design several scoring functions to rank the candidate occurrences (clean). Only high quality (top-𝑘) candidate answers are involved for training. Then, we perform multi-task learning by weighing the losses computed from the top-k occurrences (learn).We evaluate our approach on the constructed ApiQaData dataset.The results show that Clean and Learn outperforms state-of-the-art approaches, and can answer 141 out of 200 API-related questions in ApiQaData


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
