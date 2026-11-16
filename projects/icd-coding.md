# Clinical ICD Coding with a Small Language Model

## Project overview

This Machine Learning II course project evaluated whether
Qwen2.5-0.5B-Instruct could produce three-character ICD-10-AM codes from
clinical text under structured-output constraints.

## My contribution

- Built a Transformers batch-inference workflow that stored prompts,
  generation parameters, predictions, and parsed codes for each sample.
- Compared zero-shot prompting, rule-constrained output, implicit reasoning,
  one-shot examples, and alternative sampling parameters on a five-case
  development set.
- Ran a separate ten-case evaluation and performed case-by-case error analysis.
- Identified label confusion and example bias and proposed RAG, fine-tuning,
  and deterministic rule validation as follow-up improvements.

## Result and interpretation

The best development setup achieved 5/5 format compliance but only 1/5 correct
codes. The result is useful as a failure analysis rather than a deployment
claim: output formatting improved, while clinical coding accuracy remained
insufficient.

## Stack

Python · Hugging Face Transformers · Qwen2.5-0.5B-Instruct · Prompt evaluation
· Structured-output parsing · Error analysis

## Public boundary

The clinical text, prompts containing source records, and course evaluation
data are not published. This page is a project summary, not a clinical system.

[Back to portfolio](../README.md)
