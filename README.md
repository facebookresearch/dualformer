# Dualformer

Official code base for the paper titled Dualformer: Controllable Fast and Slow Thinking by Learning with Randomized Reasoning Traces. [ICLR 2025].

This repository contains code for accessing the generated datasets and trained models, re-producing the figures of the main paper, and the code used for running the presented experiments.

## Overview

All code is designed around storing and transforming datasets stored in a MongoDB instance.
The [`notebook`](./notebook) folder contains Jupyer notebooks with examples demonstrating how to access token dataset and prompting a trained Searchformer model.
This folder also contains notebooks that read data from MongoDB to generate all figures included in the main paper.

The `searchformer` module contains all code used in the presented experiments.
Please refer to the documentation in the folder [`doc`](./doc) for using this module to train models, evaluate them, and generate training datasets.

## Setup and installation

This code base uses `python=3.10`.
To run python code and the included Jupyer notebooks, a virtual environment can be created using the included `requirements.txt` file.
For example, this virtual environment can be created with

```
$ python3.10 -m venv venv
$ source venv/bin/activate
(venv) $ pip install -r requirements.txt 
```

For the code to run correctly, a MongoDB instance needs to be setup.
This code base is designed to work with [MongoDB Community Edition](https://www.mongodb.com/try/download/community) and connects by default directly to `mongodb://localhost:27017/mongo` without any user authentication setup.
For example, to explore the included token datasets and checkpoints, a MonogDB instance could be installed locally in a laptop and this code base can be used to access a MongoDB instance running on `localhost`.
To direct the `searchformer` module to connect to a different MongoDB instance, the default MongoDB URI can be overwritten by setting the environment variable

```
export MONGODB_URI=mongodb://localhost:27017/mongo
```

before running any python code.
The code segment used for connecting to MongoDB can be found in `searchformer.utils` in function `mongodb_client`.

To import the released datasets the command line tool [`mongorestore`](https://www.mongodb.com/docs/database-tools/mongorestore/) is used.
Instructions for downloading and installing MongoDB Database Tools can be found [here](https://www.mongodb.com/docs/database-tools/).

**As a convention, all commands are run from this repository's root directory and not from any sub-directory. The root directory is the directory that contains this README file.**

For example, a correct setup of the python environment can be tested by running the following from the repositories root directory: 

```
$ python -m searchformer.train --help
Usage: python -m searchformer.train [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  bulk-drop-run           Drop multiple training runs.
  bulk-export-checkpoint  Bulk export of all checkpoints into current...
  bulk-import-checkpoint  Bulk import checkpoints from directory.
  drop-run                Drop individual training run.
  export-checkpoint       Export a checkpoint stored in MongoDB to a file.
  import-checkpoint       Import a checkpoint into MongoDB from file.
  list-all                List all training runs.
  list-all-checkpoints    List all stored checkpoints.
  single                  Start single DDP training run.
  sweep                   Start single DDP training run with provided...
```


## License
See the [LICENSE](./LICENSE) file for details about the license under which this code is made available.

## Citation
If you find this repository useful in your research, please consider giving a star :star: and a citation
```
@inproceedings{su2025dualformer,
  title={Dualformer: Controllable fast and slow thinking by learning with randomized reasoning traces},
  author={Su, DiJia and Sukhbaatar, Sainbayar and Rabbat, Michael and Tian, Yuandong and Zheng, Qinqing},
  booktitle={Proceedings of the International Conference on Learning Representations (ICLR)},
  year={2025},
  address={Location of the conference, if known},
  publisher={Publisher, if known},
  note={arXiv preprint arXiv:2410.09918}
}
```
