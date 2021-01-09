# COGS

This repository contains the dataset used in the paper "COGS: A Compositional Generalization Challenge Based on Semantic Interpretation", accepted to EMNLP 2020. 

## Dataset

The dataset can be found under `cogs/`. `dev` and `test` contain in-distribution examples and `gen` contains the generalization examples discussed in our paper. We used examples in `train` for our main experiment and `train_100` for the additional experiment in the appendix with increased number of exposure examples.


## Experiments

We used [OpenNMT](https://github.com/OpenNMT/OpenNMT-py) for our experiments. This repo contains the version of OpenNMT that we used. You can follow the instructions below to rerun our experiments.


### Preprocessing

0. Reformat the .tsv format dataset into format used by the OpenNMT preprocessing code:
    python reformat_data_for_opennmt.py --input_path path_to_data --output_path output_path

1. Run OpenNMT preprocess. output_path should be the same as the output of step 0, and opennmt_path should point to the src/OpenNMT directory in this repo.
    bash opennmt_preprocess.sh output_path opennmt_path
