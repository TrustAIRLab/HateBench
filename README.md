# HateBench

[![USENIX: 2025](https://img.shields.io/badge/USENIX-2025-red.svg)]()
[![arXiv: preprint](https://img.shields.io/badge/arXiv-preprint-orange.svg)]()
[![dataset: huggingface](https://img.shields.io/badge/dataset-huggingface-yellow)](https://huggingface.co/datasets/TrustAIRLab/HateBenchSet)
[![license](https://img.shields.io/badge/License-Apache_2.0-blue)](#license)

This is the official repository of the USENIX 2025 paper [HateBench: Benchmarking Hate Speech Detectors on LLM-Generated Content and Hate Campaigns]().

In this paper, we propose **HateBench**, a framework designed to benchmark hate speech detectors on LLM-generated content. 

**Disclaimer. This repo contains examples of hateful and abusive language. Reader discretion is recommended. This repo is intended for research purposes only. Any misuse is strictly prohibited.**

## Overview

Our artifact repository includes:

- HateBench, the framework designed to benchmark hate speech detectors on LLM-generated content. 
- HateBenchSet, the manually-annotated dataset, comprising 7,838 samples across 34 identity groups, generated by LLMs.
- Code for reproducing the LLM hate campaign, including both the adversarial hate campaign and stealthy hate campaign. 
- Scripts to generate the key result tables and figures from the paper, including: 
  - Table 3: Performance on LLM-generated samples.
  - Table 4: F1-score on LLM-generated and human-written samples.
  - Table 6: Performance of adversarial hate campaign
  - Table 8: Performance of model stealing attacks.
  - Table 9: Performance of stealthy hate campaign with black-box attacks.
  - Table 10: Performance of stealthy hate campaign with white-box gradient optimization. 

## HateBench

## HateBenchSet

`HateBenchSet` is provided on [Hugging Face](https://huggingface.co/datasets/TrustAIRLab/HateBenchSet/).

```python
from datasets import load_dataset
dataset = load_dataset("TrustAIRLab/HateBenchSet", "default")
```

Data structure:

| Column        | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| model         | Model used to generate response.                            |
| status        | Status of the model, i.e., `original` or `jailbreak`.       |
| status_prompt | Prompt used to set the model.                               |
| main_target   | The category of identity groups, e.g., race, religion, etc. |
| sub_target    | The identity group.                                         |
| target_name   | The complete name of the identity group.                    |
| pid           | Prompt id.                                                  |
| prompt        | The prompt.                                                 |
| text          | The sample generated by the model.                          |
| hate_label    | `1` denotes `Hate`, `0` refers to `Non-Hate`.               |

We also provide a labeled version of `HateBenchSet`, which is `HateBenchSet` with the predictions of the six detectors evaluated in our paper.


Specifically, for each detector, the predictions are recorded in the following columns:

* `{detector}`: the complete record returned by the detector.
* `{detector}_score`: the hate score of the sample.
* `{detector}_flagged`: whether the sample is predicted as hate or not.

```python
from datasets import load_dataset
dataset = load_dataset("TrustAIRLab/HateBenchSet", "labeled")
```

## LLM-Driven Hate Campaign

Given the ethical concerns, code are provided in [Zenodo](https://zenodo.org/records/14840447) with the request-access feature enabled.
We will manually review the applicants’ information to approve the application.

## Ethics & Disclosure

Our work relies on LLMs to generate samples, and all the manual annotations are performed by the authors of this study. Therefore our study is not considered human subjects research by our Institutional Review Board (IRB). Also, by doing annotations ourselves, we ensure that no human subjects were exposed to harmful information during our study. Since our work involves the assessment of LLM-driven hate campaigns, it is inevitable to disclose how attackers can evade a hate speech detector. We have taken great care to responsibly share our findings. We disclosed the paper and the labeled dataset to OpenAI, Google Jigsaw, and the developers of open-source detectors. In our disclosure letter, we explicitly highlighted the high attack success rates in the LLM-driven hate campaigns. We have received the acknowledgment from OpenAI and Google Jigsaw. 

**This repo is intended for research purposes only. Any misuse is strictly prohibited.**


## Citation

If you find this useful in your research, please consider citing:

```bibtex
@inproceedings{SWQBZZ25,
  author = {Xinyue Shen and Yixin Wu and Yiting Qu and Michael Backes and Savvas Zannettou and Yang Zhang},
  title = {{HateBench: Benchmarking Hate Speech Detectors on LLM-Generated Content and Hate Campaigns}},
  booktitle = {{USENIX Security Symposium (USENIX Security)}},
  publisher = {USENIX},
  year = {2025}
}
```
