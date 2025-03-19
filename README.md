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
