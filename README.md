# The EgoTempo Dataset
This repository contains the EgoTempo dataset for the CVPR 2025 paper [Omnia de EgoTempo: Benchmarking Temporal Understanding of Multi-Modal LLMs in Egocentric Videos](https://arxiv.org/pdf/2503.13646).

## News
- 2025.03.19: The EgoTempo dataset is released.
- 2025.02.26: Paper accepted to CVPR 2025.

## Overview

EgoTempo is a video question-answering benchmark to evaluate temporal
understanding capabilities of multi-modal LLMs. EgoTempo has the following
unique characteristic.

- An open-ended QA benchmark in the domain of egocentric video understanding.
- Questions demand a holistic view of the video. Answers cannot be derived from
a single frame or common sense knowledge.
- A well-defined question taxonomy, consisting of 10 different temporal
reasoning categories with an equal number of questions.
- A highly challenging benchmark for temporal reasoning. The best
closed source LLM achieve 40% accuracy, while the human performance is 63%.

## Dataset Description

EgoTempo contains 500 test examples. The question-answer pairs are generated
with Gemini public API followed by careful human curation. Each question belongs
to one of the 10 pre-defined categories e.g., action counting, future action
prediction, locating objects, etc. Each category has an equal number of
questions.

### Videos
EgoTempo is built on top of the videos from [Ego4D dataset](https://ego4d-data.org/).

### Annotations

The dataset is stored in a json file named `egotempo_openQA.json` with the
following format:

```json
{
  "info": {
    "date": "release date",
    "version": "current version"
  },
  "annotations": [  // List of dictionaries, one for each example.
    {
      "question_id": "27470817-f803-45b4-b9d4-e754cb3196bc_368.4019995568589_403.56079044314106_0",
      "clip_id": "27470817-f803-45b4-b9d4-e754cb3196bc_368.4019995568589_403.56079044314106",
      "question_type": "object-specific action",
      "question": "What does the person pick up before rubbing their hands together?",
      "answer": "The oil remover spray."
    },...
  ]
}
```

* `clip_id` is the string identifier of the video clip which is cropped from the
original long videos in Eg4D. The naming convention follows
{video_uid}_{start_timestamp}_{end_timestamp}, where {video_uid} is the original
video identifier in Ego4D, {start_timestamp} and {end_timestamp} indicate the
cropped temporal window.
* `question_id` is the string identifier of the question. The naming convention
follows {clip_id}_{question_index} because one video clip might be used in
multiple questions.

## Evaluation

EgoTempo is intended for zero-shot evaluation. The metric calculation requires
a LLM as the autorate, judging the open answer against the collected ground
truth. We will release the evaluation code soon.


# EgoTempo QA Benchmark Toolkit

This repository provides a full pipeline for working with QA benchmarks based on the [Ego4D](https://ego4d-data.org/) dataset. It includes tools for downloading videos, generating trimmed clips, running inference with Google's Gemini model, and evaluating prediction quality.

## 📦 What’s Included

### 1. Video Downloading and Trimming

We provide scripts to:

- **Download full Ego4D videos** using public links or access tokens.
- **Trim videos into clips** corresponding to the time intervals associated with specific question-answer (QA) pairs.

This is essential for efficiently processing the relevant visual content associated with each QA.

---

### 2. Inference using Gemini API

We include a complete inference pipeline using the **Google Gemini** large vision-language model to generate answers based on frames extracted from video clips.

- The provided implementation is tailored for a single model, but the codebase is **modular and scales well** as a template for adapting to **any QA dataset** derived from egocentric video.
- Questions are formatted into prompts, frames are converted to base64, and results are saved in JSON format.

---

### 3. Evaluation Code

We provide **evaluation scripts** to assess the correctness of generated answers, allowing you to:

- Compare Gemini’s answers to ground-truth answers.

---

## 🚀 Quickstart

All steps are integrated into a single Jupyter notebook (`gemini_eval.ipynb`) for ease of use:

1. **Download** the full Ego4D videos and **trim** them into clips based on QA timestamps.
2. **Run inference** using the Gemini API on the selected dataset.
3. **Evaluate the predictions** for correctness against ground truth answers.

You can run everything step-by-step in the provided notebook for full reproducibility.




## License

The EgoTempo dataset is released under the [CC-BY License](https://creativecommons.org/licenses/by/4.0/).

## Citation

If you use this dataset in your research, please cite:

```
@inproceedings{plizzari2024egptempo,
      title={Omnia de EgoTempo: Benchmarking Temporal Understanding of Multi-Modal LLMs in Egocentric Videos}, 
      author={Chiara Plizzari, Alessio Tonioni, Yongqin Xian, Ace Kulshrestha, Federico Tombari},
      booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
      year={2025},
}
```

## Contact
For questions or issues related to the dataset, please open an issue in this
repository or contact the authors.

This is not an officially supported Google product. This project is not
eligible for the [Google Open Source Software Vulnerability Rewards
Program](https://bughunters.google.com/open-source-security).
