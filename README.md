# COGS

This repository contains the dataset used in the paper [COGS: A Compositional Generalization Challenge Based on Semantic Interpretation](https://www.aclweb.org/anthology/2020.emnlp-main.731/), accepted to EMNLP 2020. 

## **Changelog**
2022/09/13: Fixed semantic roles of 50 examples in the generalization set.
Affected subset is `obj_pp_to_sub_pp` only, where roles of animate subjects of unaccusative verbs were being marked as agent instead of theme.

Example:
```
The researcher in a room froze -> 
* researcher ( x _ 1 ) ; researcher . nmod . in ( x _ 1 , x _ 4 ) AND room ( x _ 4 ) AND freeze . theme ( x _ 5 , x _ 1 )

```
(h/t to Andrew Drozdov for flagging!)

## Dataset

The dataset can be found under `data/`. `dev` and `test` contain in-distribution examples and `gen` contains the generalization examples discussed in our paper. We used examples in `train` for our main experiment and `train_100` for the additional experiment in the appendix with increased number of exposure examples.

### Types of generalization
The final column in `gen.tsv` contains information about the particular generalization case described in the paper (see Table 7 for a full list). 
You can use `data/gen_cases_to_paper_sections.json` to map the column values to a more informative description of the generalization tested, plus a link to the relevant paper section.

**We encourage reporting generalization performance by case as well as the aggregate performance on the full generalization set. In particular, lexical vs. structural divide seems important.**
`cp_recursion`, `pp_recursion`, and `obj_pp_to_subj_pp` correspond to structural generalization and the rest, lexical generalization. 

## Experiments

We used [OpenNMT](https://github.com/OpenNMT/OpenNMT-py) for our experiments. This repo contains the version of OpenNMT that we used. You can follow the instructions below to rerun our experiments.


### Preprocessing

First, reformat the .tsv format dataset into format used by the OpenNMT preprocessing code:

    python reformat_data_for_opennmt.py --input_path path_to_data --output_path output_path

Second, run OpenNMT preprocess. output_path should be the same as the output of the previous step, and opennmt_path should point to the src/OpenNMT directory in this repo.

    bash opennmt_preprocess.sh output_path opennmt_path


### Training and inference

See scripts named `run_x.sh` under `scripts/`, where x is one of `transformer`, `lstm_uni`, `lstm_bi`. Run with the same commandline arguments as the preprocessing step:

    bash run_transformer.sh output_path opennmt_path

Please refer to the individual script files for the hyperparameter settings for each model and random seed.

After running the script, the predictions of the model for in-distribution dev/test sets and out-of-distribution generalization set will be saved under `$OPENNMT_PATH/pred/` as a .tsv file. It will be a tab-delimited file with 3 columns: source, target, model_prediction.
