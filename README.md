# Cooking-CLIP
Context-aware CLIP Embedding for Zero-shot Recipe Generation

## Requirements

- Install PyTorch:
  ```
  pip install torch  # Choose a version that suits your GPU
  ```
- Install CLIP:
  ```
  pip install git+https://github.com/openai/CLIP.git
  ```
- Install clip-score bert-score  from [PyPI](https://pypi.org/project/clip-score/):
  ```
  pip install clip-score
  pip install bert-score
  ```

Or use the command to install all required packages in one line:
```shell
$ pip install -r ./requirements.txt


```
## Data
We obtained ASR sentences and corresponding temporal boundaries directly from [the Google Cloud API](https://cloud.google.com/speech-to-text/docs/automatic-punctuation), but they can also be obtained by applying an off-the-shelf punctuation model to the downloaded raw ASR data (as done in [this project](https://github.com/antoyang/just-ask) for instance).
Also note that spatially-pooled CLIP ViT-L/14 @ 224px features must be extracted at 1FPS (as done in [this project](https://github.com/antoyang/FrozenBiLM)) and added to the column name `image/clip_embeddings`.

## Train
An example command-line to train on YouCook2 with [config file](configs/youcook2.py) is

```shell
$ python -m main.py --config=youcook2.py 
```

## Evaluation

First generate the captions using the following command 
```
python predictions_runner.py  --checkpoint path_to_checkpoints.pt 
```
To compute the CLIP/Bert score between images/reference and texts, make sure that the image/reference and text data are contained in two separate folders, and each sample has the same name in both modalities. Run the following command:
```
python -m clip_score path/to/image path/to/text
python -m bert_score -r example/refs.txt -c example/hyps.txt --lang en
```



## Pretrained models
[cooking_clip](https://drive.google.com/file/d/1EFI0aujIWBr3dTC_a2hdoV4QJenAlEWU/view)


## Note
This repository is based on [CLIP](https://github.com/openai/CLIP), [DeCap](https://github.com/dhg-wei/DeCap) and [pycocotools](https://github.com/sks3i/pycocoevalcap) repositories.




