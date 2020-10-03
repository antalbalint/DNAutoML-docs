.. DNAutoML documentation master file, created by
   sphinx-quickstart on Fri Oct  2 18:27:37 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to DNAutoML's documentation!
====================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

Introduction
============

DNAutoML is an automated machine learning to for DNA sequence anaylsis. It encapsulates data acquisition and processing, DNN network design and training.ß

Installation
============

To run DNAutoML the following software is needed:

* `Git <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_

* `Python 3.6 with Conda <https://docs.conda.io/projects/conda/en/latest/user-guide/install/>`_

* For GPU usage: `CuDNN <https://developer.nvidia.com/cudnn>`_

For specific installation details for these third-party software, please refer to the installation information provided in the links above.

Obtaining the source code
-------------------------

The Python code for DNAutoML can be obtained with the following command:

   ``git checkout https://github.com/SynBioFoundry/DNAutoML.git``

To install the required Python pacakges run

   ``cd DNAutoML``

   ``pip install -r requirements.txt``

Configuration
=============

The core of each DNAutoML project is a configuration file. Each file will define the data types, the intended usage (e. g. classification, regression), the runtime environment and the I/O related parameters.

A DNAutoML config file can consists of the following sections:

   | *[PROJECT]*
   | name = Name of the project
   | path = Path to the working directory.
   | mode = {1 - from ML dataset, 2 - from raw data, 3 - from entrez, 4 - }
   | task = {1 - classification, 2 - regression}

   | *[ML]*
   | environment = {GPU, CPU} default: CPU
   | gpus = comma-separated list of gpus to be used(e.g. gpu:0, gpu:1, ...) (default: all available)
   | epochs = number of epochs (default: 100)
   | n_folds = number of cross-validation folds (default: 1)
   | max_iter = maximum number of parameter settings to be evaluated during DNN design (default: 100)
   | batch_size = batch size (default: 256)

   | *[EXISTING SOURCE]*
   | ml_data_path = path to training files
   | raw_data_path = path to raw data files
   | raw_data_format = {fasta, genbank}
   | raw_data_extension = extension of the raw data files (e.g. fna)
   | model_path = where to store the trained model

   | *[FROM_ENTREZ]*
   | organism = Name of the organism
   | genetic_part = {gene, promoter, terminator, intergenics} - one or multiple genetic parts can be listed. If one genetic part, the second class will be randomly selected background
   | length = Length of the DNA fragments in bps (defaut: 100)

Usage
=====

The generate a new DNN using DNAutoML, use the following command:

   | ``python -m dnautoml DNAutoML.py [-h] {generate, evaluate, predict}``
   | ``-config CONFIG_PATH [-json JSON_MODEL_PATH] [-weights H5_WEIGHTS_PATH] [-predict TEST_DATA]``

   * ``-h``: help

   * ``{generate,evaluate, predict}``: the usage mode. If

      * *generate*: a completely new DNN will be generated using the configuration file provided. If the JSON model is provided, the DNN design step will be skipped.

      * *evaluate*: generate evaluation report on an already generated DNN.

      * *predict*: use the generated DNN on test data

   *  ``-config``: path to the config file (required)

   *  ``-json``: path to the JSON model (optional for generate, required for evaluate and predict)

   * ``-weights``: path to model weights in H5 format (optional for generate, required for evaluate and predict)

Automated DNN design
--------------------

Generation from existing training data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Citation
========
Balint Antal, D. Bejamin Gordon: Automating Deep Learning for DNA Analysis

Licence
=======

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
