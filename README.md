# Linpeng Yang

Machine learning and health data science graduate with hands-on experience in
medical image segmentation, clinical language-model evaluation, tabular
classification, high-performance computing, and reproducible research
workflows.

[中文版本](README.zh-CN.md)

## Focus

- Medical AI and health data science
- Machine learning evaluation and error analysis
- PyTorch, scikit-learn, Transformers, and nnU-Net
- Reproducible experiments on Linux and NCI Gadi HPC
- Evidence-bounded reporting and patient-data-aware publication

## Featured projects

| Project | What I worked on | Public evidence |
|---|---|---|
| [Intracranial haemorrhage segmentation](projects/ich-segmentation.md) | Five-fold comparison of 2D, standard three-slice 2.5D, and 3D nnU-Net on 192 head CT cases | [Code and validated aggregate results](https://github.com/Kandasorat/bhsd-nnunet) |
| [Clinical ICD coding with a small language model](projects/icd-coding.md) | Structured-output prompting and error analysis with Qwen2.5-0.5B-Instruct | Public project summary; clinical text is not published |
| [Breast tumour classification](projects/breast-tumour-classification.md) | Data cleaning, stratified evaluation, and regularized logistic-regression tuning | Public project summary; coursework data is not published |
| [Marine microbial abundance analysis](projects/marine-microbial-analysis.md) | Plate-count and fluorescence-microscopy comparison across environmental samples | Public project summary |
| [Stimuli-responsive marine polysaccharide nanocarrier](projects/nanocarrier-research.md) | Undergraduate project leadership and wet-lab validation | Public project summary |

## Selected results

- Completed a patient-aligned, five-fold multiclass ICH segmentation benchmark
  with 576 out-of-fold predictions. Native foreground mean Dice was 0.271 for
  2D, 0.258 for standard three-slice 2.5D, and 0.307 for 3D. The public report
  retains the recall, small-lesion, and compute trade-offs behind those values.
- Built a reproducible V100 efficiency comparison covering 15 method-fold
  tasks and 576 whole-case timing records.
- Evaluated prompt variants for small-model ICD coding, then used independent
  test errors to identify label confusion and example bias and propose RAG,
  fine-tuning, and rule-validation improvements.
- Trained and tuned a logistic-regression classifier on 569 cleaned FNA
  samples; the held-out test result was 97.37% accuracy with 0.93 malignant
  recall.

## Technical toolkit

**Programming and ML:** Python, PyTorch, scikit-learn, Transformers, pandas,
NumPy, nnU-Net

**Methods:** classification, medical image segmentation, cross-validation,
regularized logistic regression, GridSearchCV, prompt evaluation, error
analysis, experiment tracking

**Research infrastructure:** Git, Linux, Jupyter, NCI Gadi, PBS job workflows

## Education

- MSc Health Data Science, UNSW Sydney, 2024–2026
- BSc Biotechnology, Ocean University of China, 2017–2022

## Publication and data boundary

This portfolio contains aggregate results and project descriptions only. It
does not publish patient images, clinical text, identifiers, model checkpoints,
coursework datasets, laboratory raw data, internal storage paths, or scheduler
records. Projects without a public repository are labelled as summaries rather
than presented as open-source implementations.
