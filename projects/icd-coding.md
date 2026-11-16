# Clinical ICD Coding with a Small Language Model

> Machine Learning II course project · September–December 2025 ·
> [中文](icd-coding.zh-CN.md)

## Project at a glance

| Item | Detail |
|---|---|
| Objective | Generate a three-character ICD-10-AM principal-diagnosis category from a synthetic hospital-course summary |
| Dataset | `starmpcc/Asclepius-Synthetic-Clinical-Notes` on Hugging Face |
| Dataset scale | 158,114 synthetic clinical-note records |
| Experiment subset | 5 fixed development cases and 10 independent test cases |
| Model | `Qwen/Qwen2.5-0.5B-Instruct` |
| Framework | PyTorch and Hugging Face Transformers |
| Output contract | Exactly one uppercase letter followed by two digits |

## End-to-end workflow

```mermaid
flowchart LR
    A[Filter dataset] --> B[Prompt V1–V5]
    B --> C[Generate & parse]
    C --> D[Development & test evaluation]
    D --> E[Error analysis]
    E --> F[RAG & fine-tuning plan]
```

## 1. Dataset preparation

The Asclepius dataset contains synthetic clinical notes and related tasks. The
assignment specified a fixed subset so every prompt version was tested on the
same cases:

| Split | Cases | Purpose |
|---|---:|---|
| Development | 5 | Prompt design and decoding experiments |
| Independent test | 10 | Final evaluation after prompt selection |

Filtering was performed with Hugging Face `Dataset.filter`, followed by a
conversion to pandas for experiment tracking. The comparison retained the
same cases across all five prompt versions.

## 2. Model and generation pipeline

The tokenizer and causal language model were loaded from
`Qwen/Qwen2.5-0.5B-Instruct`. Each experiment used a chat-style system message
and user message, then applied the model's chat template before tokenization.

The default generation path used:

```text
max_new_tokens = 8
do_sample = False
decoding = deterministic greedy generation
post-processing = strip → first 3 characters → uppercase
```

Only newly generated tokens were decoded, preventing the prompt text from
being mistaken for the answer.

## 3. Prompt engineering experiments

| Version | Design change | Development accuracy |
|---|---|---:|
| V1 | Simple coder role and direct three-character output request | 20% |
| V2 | Added ACS 0001 definition, excluded symptoms/procedures, strict format | 20% |
| V3 | Added internal reasoning instruction and reinforced ACS rules | 0% |
| V4 | One-shot example before the target case | 0% |
| V5 | Certified-coder role, underlying-condition step, strict one-code contract | 20% |

![Prompt version comparison](../assets/icd-prompt-comparison.svg)

The prompt iterations were controlled rather than cumulative guessing: each
version changed a specific instruction strategy while using the same
development cases and the same model.

## 4. Structured output handling

The experiment separated two questions:

1. **Can the model obey the output format?**
2. **Is the generated code clinically correct?**

This distinction matters because a syntactically valid code can still be the
wrong diagnosis category. Predictions were normalized to a three-character
category before exact comparison with the reference code.

## 5. Decoding-parameter experiment

Prompt V5 was also tested on three development cases with stochastic decoding:

```text
do_sample = True
temperature = 0.7
top_p = 0.9
```

Sampling changed the predicted categories but did not improve correctness. It
also made outputs less stable. Deterministic greedy decoding was therefore
retained for the final independent evaluation.

## 6. Independent test result

| Evaluation | Correct | Total | Accuracy |
|---|---:|---:|---:|
| Final test with Prompt V5 and greedy decoding | 0 | 10 | 0% |

The result is a useful negative finding rather than a deployment result. A
general 0.5B-parameter instruction model could follow portions of the output
contract, but prompting alone did not provide the specialist ICD-10-AM and ACS
knowledge needed for principal-diagnosis coding.

## 7. Error analysis

The predictions showed three recurring failure modes:

- **label-space confusion:** the model repeatedly returned familiar-looking
  categories without reliable mapping from the underlying condition;
- **example bias:** a one-shot example could steer the output family without
  teaching the actual coding rule;
- **reasoning–knowledge mismatch:** more detailed instructions changed the
  prompt but could not supply missing codebook knowledge.

```mermaid
flowchart LR
    A[Valid-looking output] --> B{Correct code?}
    B -->|No| C[Missing ICD knowledge]
    B -->|No| D[Principal diagnosis confusion]
    B -->|No| E[Prompt/example bias]
    C --> F[Retrieval or fine-tuning]
    D --> G[Rule-aware training data]
    E --> H[Broader and balanced examples]
```

## 8. Improvement plan

1. **Retrieval-augmented generation:** retrieve relevant ICD-10-AM categories
   and ACS guidance before generation.
2. **Supervised fine-tuning:** train on note-to-principal-code examples with
   balanced diagnostic families.
3. **Constrained candidate ranking:** generate or retrieve a small candidate
   set, then rank codes instead of free-form generation.
4. **Deterministic validation:** reject outputs that fail the category regex or
   do not exist in the code dictionary.
5. **Stronger evaluation:** use a larger locked test set, top-k accuracy,
   category-level confusion analysis, and confidence calibration.
6. **Human oversight:** retain qualified clinical coders for review; the model
   should support, not autonomously replace, coding decisions.

## Tools demonstrated

Python · PyTorch · Hugging Face Datasets · Transformers · Qwen2.5 · chat
templates · prompt ablation · decoding analysis · structured parsing · exact
match evaluation · clinical NLP error analysis

[Back to portfolio](../README.md)
