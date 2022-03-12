[![Check code style](https://github.com/JetBrains-Research/Genegram/actions/workflows/lint.yml/badge.svg)](https://github.com/JetBrains-Research/Genegram/actions/workflows/lint.yml)
[![Check code style](https://github.com/JetBrains-Research/Genegram/actions/workflows/test.yml/badge.svg)](https://github.com/JetBrains-Research/Genegram/actions/workflows/test.yml)
---

# Genegram: RNA Secondary Structure Prediction by Combination of Formal Grammars and Neural Networks

## Description

Command Line Tool for Predicting RNA Secondary Structure Connectivity Table

## FASTA format

**⚠️ We use a slightly more strict FASTA format than the [standard](https://en.wikipedia.org/wiki/FASTA_format) ⚠️**

### Our format

```text
>RNA description
RNA sequence
...
>RNA description
RNA sequence
```

### Example

```text
>34551
GGCCUCCAAGCUGUGCCUUGGGUGGCC
>34552
CCUCCCUUACAAGGAGG
>34553
GGAGUGGCCGAAAGGCAUCUCC
>34735
GGCUCUCAGUGAGCC
```

## Requirements

### Hardware

* Genegram requires only a standard computer with around 16 GB RAM to support the in-memory operations for RNAs sequence length less than 500

### OS

* [`Ubuntu 20.04`](https://releases.ubuntu.com/20.04/) or later

### Software

* [`Python 3.8`](https://www.python.org/downloads/release/python-380/)
* [`Virtualenv`](https://virtualenv.pypa.io/en/latest/installation/)
* [`CUDA 11.2`](https://developer.nvidia.com/cuda-11.2.0-download-archive) *(Optional If using GPU)*
* [`cuDNN 8.1`](https://developer.nvidia.com/cudnn) *(Optional If using GPU)*

### Python packages

```text
tensorflow==2.7.0
pygraphblas==4.2.2
pyformlang==0.1.26
pillow==8.4.0
```

## Installation

### Package

We recommend that you use a virtual environment because Genegram has a strict requirements policy

1. `virtualenv -p python3.8 venv`
2. `source ./venv/bin/activate`
3. `pip install genegram`

### From sources

We recommend that you use a virtual environment because Genegram has a strict requirements policy

1. `git clone https://github.com/JetBrains-Research/Genegram.git`
2. `cd Genegram`
3. `virtualenv -p python3.8 venv`
4. `source ./venv/bin/activate`
5. `pip install .`

## Usage

After successfully installing the package, you have three options to use it:

1. `python -m genegram <arguments>`
2. `genegram arguments`
3. ```Python
   from genegram import process_fasta_group
   process_fasta_group(<arguments>)
   ```

### Arguments

Argument | Required | Description
:--- | :---: | :---
-i, --inp | True | Path to the [`FASTA`](http://genetics.bwh.harvard.edu/pph/FASTA.html) file
-o, --out | True | Path to the folder where the [`Connectivity Tables`](http://rna.urmc.rochester.edu/Text/File_Formats.html#CT) will be saved
-m, --model | False | Type of the model to be used: </br> `main` -- The default model, the best on average </br> `mps` -- Multiplet prediction model </br> `pks` -- Pseudoknots prediction model

## Examples

If you have installed Genegram from sources, you can run the following example (in the Genegram folder)

`genegram -i tests/data/seq.fasta -o EXAMPLE_FOLDER -m main`

## Information for Developers

### Code Style

We recommend you use a [pre-commit](https://pre-commit.com/#install) hook, which runs [black](https://github.com/psf/black) when you type git commit.

#### Install pre-commit

```shell
pipenv install --dev
pre-commit install
```

#### Use pre-commit

```shell
pre-commit run --all-files --color always --verbose
```
