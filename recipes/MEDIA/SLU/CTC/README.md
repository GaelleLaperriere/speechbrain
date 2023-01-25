# Media SLU with CTC + Seq2Seq models +/- Wav2Vec 2.0.
This folder contains scripts necessary to run an SLU experiment with the Media French dataset: [Media ASR (ELRA-S0272)](https://catalogue.elra.info/en-us/repository/browse/ELRA-S0272/), [Media SLU (ELRA-E0024)](https://catalogue.elra.info/en-us/repository/browse/ELRA-E0024/) both needed for the task. Please also download the 2 csv files given [here](https://drive.google.com/drive/u/1/folders/1z2zFZp3c0NYLFaUhhghhBakGcFdXVRyf) and place them in the `../../MEDIA` directory.

This recipe has been implemented following the paper of G. Laperrière, V. Pelloin, A. Caubriere, S. Mdhaffar, N. Camelin, S. Ghannay, B. Jabaian, Y. Estève, [The Spoken Language Understanding MEDIA Benchmark Dataset in the Era of Deep Learning: data updates, training and evaluation tools](https://aclanthology.org/2022.lrec-1.171).

Some results presented here are also part of the paper of G. Laperrière, V. Pelloin, M. Rouvier, T. Stafylakis, Y. Estève [On the Use of Semantically-Aligned Speech Representations for Spoken Language Understanding](https://arxiv.org/abs/2210.05291).

# How to run
Do not forget to process the dataset and change the `!PLACEHOLDER` in the yaml file.

```bash
python train.py hparams/{hparam_file}.yaml
python train_hf_wav2vec.py hparams/{hparam_file}.yaml
```

# Data preparation
It is important to note that Media initially offers audio files at 8kHz. Hence, audio files are upsampled on the fly within the preparation script to 16kHz.

# Results

| Media Release | hyperparams file | Test ChER | Test CER | Test CVER | Wav2Vec |
|:-------------:|:-------------------------:|:----:|:----:|:----:|:------------------------------------:|
| 2008-03-27 | train_relax.yaml | 53.2 | 73.3 | 80.9 | None |
| 2008-03-27 | train_with_wav2vec_relax.yaml | 7.9 | 21.8 | 34.1 | [LeBenchmark wav2vec2-FR-3K-large](https://huggingface.co/LeBenchmark/wav2vec2-FR-3K-large) |
| 2008-03-27 | train_full.yaml | 53.9 | 75.0 | 82.0 | None |
| 2008-03-27 | train_with_wav2vec_full.yaml | 8.2 | 26.1 | 37.5 | [LeBenchmark wav2vec2-FR-3K-large](https://huggingface.co/LeBenchmark/wav2vec2-FR-3K-large) |
| 2008-03-27 | see [paper](https://arxiv.org/abs/2210.05291) for modifications | 5.8 | 20.4 | 31.2 | [wav2vec2-xls-r-300m](https://huggingface.co/facebook/wav2vec2-xls-r-300m) |
| 2008-03-27 | see [paper](https://arxiv.org/abs/2210.05291) for modifications | 5.1 | 19.3 | 29.8 | [SAMU-XLSR](https://arxiv.org/pdf/2205.08180.pdf) |

The CVER is the one implemented in SpeechBrain for this recipe. It is strict (yield an error for a single false character), without the human rules added generally for MEDIA. Find more in the article linked above, as it corresponds to u-CVER.

# **About SpeechBrain**
- Website: https://speechbrain.github.io/
- Code: https://github.com/speechbrain/speechbrain/
- HuggingFace: https://huggingface.co/speechbrain/

# **Citing SpeechBrain**
Please, cite SpeechBrain if you use it for your research or business.

```bibtex
@misc{speechbrain,
  title={{SpeechBrain}: A General-Purpose Speech Toolkit},
  author={Mirco Ravanelli and Titouan Parcollet and Peter Plantinga and Aku Rouhe and Samuele Cornell and Loren Lugosch and Cem Subakan and Nauman Dawalatabad and Abdelwahab Heba and Jianyuan Zhong and Ju-Chieh Chou and Sung-Lin Yeh and Szu-Wei Fu and Chien-Feng Liao and Elena Rastorgueva and François Grondin and William Aris and Hwidong Na and Yan Gao and Renato De Mori and Yoshua Bengio},
  year={2021},
  eprint={2106.04624},
  archivePrefix={arXiv},
  primaryClass={eess.AS},
  note={arXiv:2106.04624}
}
```