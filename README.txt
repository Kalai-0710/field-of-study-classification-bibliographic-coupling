CS5500 MSc Dissertation - Code and Data
Classifying Scientific Papers by Field of Study:
A Comparison of Text-Based, Citation-Based and Hybrid Approaches
under Varying Text Availability

Student ID: 2513007


CONTENTS

notebooks/                  Jupyter notebooks, run in numerical order
data/raw/                   The 20 Web of Science export files
data/processed/dataset.csv  Final dataset of 8,192 publications
results/                    Output files referenced in Chapters 4 and 5


REQUIREMENTS

Python 3.12

    pip install -r requirements.txt


HOW TO RUN

The notebooks use relative paths and assume this directory structure:

    Dissertation/
        Datasets/raw/
        Datasets/processed/
        Python code/          <- notebooks go here
        Results/

Run in this order:

    01_parse_wos          Parses the raw Web of Science exports
    02_build_dataset      Assigns labels, removes duplicates, writes dataset.csv
    03_check_dataset      Dataset validation and coupling network statistics
    05_experiment         Text-availability experiments and score-level hybrid
    06_error_analysis     Error, multi-label and per-field analysis
    07_model_comparison   Model comparison, pruning and uncertainty analysis

Notebook 05 takes several minutes because the full experiment is repeated
across five random splits.


NOTE ON NOTEBOOK 04

04_features_models is an earlier prototype used during development. It
trains on the training set only and does not apply the at-least-one-label
rule, so its results differ from those reported. Its results are superseded
by notebooks 05 to 07 and are not reported in the dissertation.


SETTINGS USED

Text model:      TF-IDF (1-2 grams, min_df=2, max_features=50000) with
                 binary relevance and linear SVM, C = 2.0
Citation model:  Bibliographic-coupling kNN, k = 20, threshold = 0.35
Hybrid:          Score-level combination, w = 0.35, threshold = 1.0
Split:           60% train / 20% validation / 20% test, random_state = 42


DATA SOURCE

Records were retrieved from the Web of Science Core Collection using the
Web of Science Categories search field, restricted to articles published
in English between 2020 and 2024, sorted by times cited, with the 1,000
most-cited records exported per field in two batches of 500.
