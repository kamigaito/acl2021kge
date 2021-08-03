# ACL2021KGE

This is an implementation of our paper "Unified Interpretation of Softmax Cross-Entropy and Negative Sampling: With Case Study for Knowledge Graph Embedding" in ACL-IJCNLP2021:
```
@inproceedings{kamigaito-hayashi-2021-unified,
    title = "Unified Interpretation of Softmax Cross-Entropy and Negative Sampling: With Case Study for Knowledge Graph Embedding",
    author = "Kamigaito, Hidetaka  and
      Hayashi, Katsuhiko",
    booktitle = "Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)",
    month = aug,
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.acl-long.429",
    doi = "10.18653/v1/2021.acl-long.429",
    pages = "5517--5531",
    abstract = "In knowledge graph embedding, the theoretical relationship between the softmax cross-entropy and negative sampling loss functions has not been investigated. This makes it difficult to fairly compare the results of the two different loss functions. We attempted to solve this problem by using the Bregman divergence to provide a unified interpretation of the softmax cross-entropy and negative sampling loss functions. Under this interpretation, we can derive theoretical findings for fair comparison. Experimental results on the FB15k-237 and WN18RR datasets show that the theoretical findings are valid in practical settings.",
}
```
We used [LibKGE](https://github.com/uma-pi1/kge) for building this code.
We wrote the following instructions on the basis of original the `README.md` in [LibKGE](https://github.com/uma-pi1/kge).

## Quick start

```sh
# retrieve and install project in development mode
git clone https://github.com/kamigaito/acl2021kge
cd kge
pip install -e .

# download and preprocess datasets
cd data
sh download_all.sh
cd ..

# train an example model on toy dataset (you can omit '--job.device cpu' when you have a gpu)
kge start examples/toy-complex-train.yaml --job.device cpu

```

## Usage

### Train a model

We put configuration files used in our research on `./settings`.
`./settings/README.md` describes further details.

To begin training, run one of the following:

```sh
# Store the file as `config.yaml` in a new folder of your choice. Then initiate or resume
# the training job using:
kge resume <folder>

# Alternatively, store the configuration anywhere and use the start command
# to create a new folder
#   <kge-home>/local/experiments/<date>-<config-file-name>
# with that config and start training there.
kge start <config-file>

# In both cases, configuration options can be modified on the command line, too: e.g.,
kge start <config-file> config.yaml --job.device cuda:0 --train.optimizer Adam
```

Various checkpoints (including model parameters and configuration options) will
be created during training. These checkpoints can be used to resume training (or any other job type such as hyperparameter search jobs).

### Resume training

All of LibKGE's jobs can be interrupted (e.g., via `Ctrl-C`) and resumed (from one of its checkpoints). To resume a job, use:

```sh
kge resume <folder>

# Change the device when resuming
kge resume <folder> --job.device cuda:1
```

By default, the last checkpoint file is used. The filename of the checkpoint can be overwritten using ``--checkpoint``.


### Evaluate a trained model

To evaluate trained model, run the following:

```sh
# Evaluate a model on the validation split
kge valid <folder>

# Evaluate a model on the test split
kge test <folder>
```

By default, the checkpoint file named ``checkpoint_best.pt`` (which stores the best validation result so far) is used. The filename of the checkpoint can be overwritten using ``--checkpoint``.

### Help and other commands

```sh
# help on all commands
kge --help

# help on a specific command
kge dump --help
```
