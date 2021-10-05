# The Submission for SIMMC 2.0 Challenge 2021
- [challenge website](https://github.com/facebookresearch/simmc2)

## Requirements
- python 3.8.8
- pytorch 1.8.1
- [transformers 4.8.2](https://huggingface.co/transformers/v4.8.1/)
- [apex](https://github.com/NVIDIA/apex) for multi-gpu
- nltk

## Preprocessing

1. Download Data

Download the [data](https://github.com/facebookresearch/simmc2/tree/master/data) provided by the challenge organizer and put it in the data folder.

2. Image saving

Preprocess the image files in advance. The preprocessed result has the image name as the key and visual as the value.
```bash
python3 image_preprocessor.py
python3 image_preprocessor_final.py
```
The result(.pickle) is saved in res folder.

## Step 1 (ITM)

First, the model is post-trained by image-to-text matching. Here, image is each object and text is the visual metadata of the image.
Code is provided in the [ITM folder](https://github.com/rungjoo/simmc2.0/tree/master/ITM).

## Step 2 (BTM)
Second, pretraining is performed to use background reprsentation of image in subtasks. Similar to [ITM](https://github.com/rungjoo/simmc2.0/tree/master/ITM), it is trained to match image and text, and the image is the background of the dialog and the text is the entire context of the dialog. Code is provided in the [BTM folder](https://github.com/rungjoo/simmc2.0/tree/master/BTM).

## Step 3

This is the learning process for each subtask. You can train the model in each folder (sub1, sub2, sub4).

## DevTest Results

**Subtask #1: Multimodal Disambiguation**
| Test Method | Accuracy |
| :------: | :-------: |
| GPT2 from Challenge organizer | 73.9 |
| Ours | 92.28 |

**Subtask #2: Multimodal Coreference Resolution**
| Test Method | Object F1 |
| :------: | :-------: |
| GPT2 from Challenge organizer | 0.366 |
| Ours | 0.56 |

**Subtask #4: Multimodal Dialog Response Generation**

**Generation** 
| Baseline |      BLEU |
| :------: | :-------: |
| GPT2 from Challenge organizer | 0.192 |
| MTN-SIMMC2 from Challenge organizer | 0.217 |
| Ours | 0.285 |