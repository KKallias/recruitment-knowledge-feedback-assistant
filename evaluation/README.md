# Evaluation Plan

> **Status:** Planned. No measured results are claimed yet.

The next phase of the project is to evaluate retrieval and answer quality rather than treating a successful workflow execution as proof of quality.

## Planned test set

Create approximately 25 labelled questions against fictional recruitment-policy documents. Each question should have a known supporting source/chunk so retrieval can be checked against expected evidence.

## Retrieval checks

For each question, record whether the supporting evidence appears in:

- Top 3 retrieved chunks
- Top 5 retrieved chunks

A later experiment will compare at least one alternative recursive chunking configuration.

## Answer checks

Review generated answers for:

- faithfulness to retrieved evidence
- citation correctness once citations are implemented
- correct abstention when the knowledge base does not contain enough evidence

## Adversarial check

Place an instruction inside a fictional source document and verify that it is treated as document content rather than as an instruction that can override the workflow's system behaviour.

## Results

Results will be added here only after the tests have been run. This repository intentionally does not present planned evaluation as completed evidence.
