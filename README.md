# NFL Wide Receiver Blocking Analytics

This repository contains the validation component of a six-person Bruin Sports
Analytics research project on wide receiver blocking effectiveness. The full
paper develops a quantitative framework from play-level and player-tracking
features; this notebook evaluates whether an interpretable decision tree can
separate above- and below-median blockers under the project's
volume-adjusted Blocking Effectiveness Score (BES).

## Result

Using a stratified 80/20 split and a depth-limited decision tree, the validation
notebook produced **84.13% test accuracy** on the project dataset. The checked-in
notebook preserves the confusion matrix, classification report, and learned
rules from that run.

## My contribution

I was responsible for the decision-tree validation: selecting the validation
features, defining the above-median classification target, evaluating the
model, and producing an interpretable tree for the team.

## Repository contents

- `BSAFINAL.ipynb` - decision-tree validation and visualization.
- `A Quantitative Framework for Assessing Wide Receiver Blocking Effectiveness Using Player Tracking Data.pdf`
  - final research paper.

## Reproducing the validation

The source player-tracking dataset is not redistributed in this repository.
Provide the prepared `final_BES.csv` file separately, then:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdir -p data
cp /path/to/final_BES.csv data/final_BES.csv
jupyter notebook BSAFINAL.ipynb
```

To use another location, set `BES_DATA_PATH` before running the notebook:

```bash
export BES_DATA_PATH=/path/to/final_BES.csv
```

The generated tree image is written to `artifacts/bes_tree.png` by default.

## Method summary

The validation uses four features:

- median yards generated after a block;
- normalized blocking volume;
- median skill-player downfield BES;
- yards generated per blocking frame.

The target is whether a player's volume-adjusted BES is above the dataset
median. The classifier uses `max_depth=4`, `min_samples_leaf=5`, balanced class
weights, and a fixed random seed.

## Data and attribution

This was collaborative research conducted through Bruin Sports Analytics.
The paper in this repository contains the complete methodology, authorship, and
research context. The notebook here represents my decision-tree validation
contribution rather than the full team pipeline.
