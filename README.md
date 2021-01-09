# COGS

This repository contains the dataset used in the paper "COGS: A Compositional Generalization Challenge Based on Semantic Interpretation", accepted to EMNLP 2020. 

## Dataset

The dataset can be found under `cogs/`. `dev` and `test` contain in-distribution examples and `gen` contains the generalization examples discussed in our paper. We used examples in `train` for our main experiment and `train_100` for the additional experiment in the appendix with increased number of exposure examples.


## Experiments

We used [OpenNMT](https://github.com/OpenNMT/OpenNMT-py) for our experiments. This repo contains the version of OpenNMT that we used. You can follow the instructions below to rerun our experiments.


### Preprocessing

1. Reformat the .tsv format dataset into format used by the OpenNMT preprocessing code:
    python reformat_data_for_opennmt.py --input_path path_to_data --output_path output_path

2. Run OpenNMT preprocess. output_path should be the same as the output of step 0, and opennmt_path should point to the src/OpenNMT directory in this repo.
    bash opennmt_preprocess.sh output_path opennmt_path


### Training and inference

See scripts named `run_x.sh` under `scripts/`, where x is one of `transformer`, `lstm_uni`, `lstm_bi`. Run with the same commandline arguments as the preprocessing step:
    bash run_transformer.sh output_path opennmt_path

Please refer to the individual script files for the hyperparameter settings for each model and random seed.

After running the script, the predictions of the model for in-distribution dev/test sets and out-of-distribution generalization set will be saved under `$opennmt_path/pred/`.
