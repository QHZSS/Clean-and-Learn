## Clean and Learn: Improving Robustness to Spurious Solutions in API Question Answering

## Introduction

API documentation is a technical content deliverable, containing instructions about how to effectively learn and use APIs. However, each page of the general API documentation contains a large amount of content. When developers have questions about a certain API, they may have to flip through many pages before reaching the desired page. A promising attempt to solve this problem is to build a neural question answering (QA) system for API documentations.

However, spurious solutions pose a major challenge for robust API question answering over documents. There may exist multiple positions (i.e., start-end indices) in the API documentation that coincidentally derive the correct answer, and typically only one of them (called golden solution) correctly solves the question given its context. The other incorrect candidates (called spurious solutions) hinder the neural network model to learn the reasonable solutions or correct answers. Labeling the golden solution for each question is costly and laborious. This further leads to the limited availability of datasets for training API QA models. In this weakly supervised setting where golden solutions are not always available, both strong supervision and/or information retrieval (e.g., google search) approaches are suboptimal.

We  develop  a  weakly-supervised  API  QA  method  named Clean-and-Learn, which aims to improve robustness to spurious solutions. Unlike traditional methods, Clean-and-Learn only needs weak supervision to train the API QA model. First, it cleans the spurious candidate solutions from weakly supervised dataset though anumber of scoring functions. Hence, only high-quality (top-k) candidate solutions are involved for training. Next, it learns a robust QA model via multi-task learning on the selected candidates.


We evaluate the effectiveness of the proposed Clean-and-Learn on APIQASet, a dataset that we created with 200 API QAs on the Java documentation. We compare Clean-and-Learn with the state-of-the-art API QA methods (OpenAPIBot and APIBot) and general weakly supervised learning methods (BLANC , Single-Hop BERT  and Hard-EM). The results show that Clean-and-Learn obtains an accuracy of 70.5% in API question answering, which significantly outperforms existing  rule  based  and  weakly  supervised  approaches  and  achieves  comparable results to that of fully supervised models.



### Train BLANC with Clean and Learn

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
